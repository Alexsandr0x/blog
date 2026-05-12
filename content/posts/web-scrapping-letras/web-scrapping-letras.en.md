---
title: "Requests + BeautifulSoup for web data capture!"
translationKey: "web-scrapping-letras"
date: 2018-09-01
description: "A simple tutorial introducing web scraping with BeautifulSoup"
---

In the job market or in personal projects, it's common to need to build your own database on a given topic before performing some analysis. This can happen with any kind of website that doesn't provide an open API.

So we can learn simple data scraping concepts using Python by simulating one of these problems. Let's suppose the following scenario:

Suppose you want to understand characteristics of a certain singer or band — any information you could use to compare two different musicians. We can compare them by genre, Spotify plays, or YouTube views. But if we want to go deeper and understand the lyrics of these musicians — to analyze sentiment or word similarity between artists — we need to build a database with those lyrics. And that's exactly what we're going to do!

__At the end of this post we'll have a script that, given a musician, returns all of their song lyrics!__

OK! So we need a data source to capture these lyrics. For some international artists there are APIs that provide this data — which you can __[see here](https://www.programmableweb.com/category/lyrics/apis?category=20278)__ — but there's a lack of Brazilian musicians and, since we want to practice web scraping, we'll force ourselves to capture this data from a website in a more "raw" way. The chosen site is __[Letras.com](https://www.letras.com)__.

To do this, let's try to understand our capture target. If we access, for example, the page of some artist and analyze the HTML, we'll be able to notice patterns that can be interesting to us.

Let's access the page of the musician [Rincon Sapência](https://www.letras.com/rincon-sapiencia/) as an example. Right away we see the musician's name, most played songs, and __all songs__ — a list on the page with, as the name says, all songs by that artist. Now we just need to analyze the HTML. Inspecting that section of the page:

{{< figure src="/images/web-scrapping-letras/letras_todas_as_musicas.png">}}

We find a structure similar to this:

```html
<div class="cnt-list--alp">
	<ul class="cnt-list"> 
		<li><a id="A" href="/rincon-sapiencia/a-coisa-ta-preta/">A Coisa Tá Preta</a></li>
		<li><a href="/rincon-sapiencia/a-noite-e-nossa/">A Noite é Nossa</a></li>
		<li><a href="/rincon-sapiencia/a-volta-pra-casa/">A Volta pra Casa</a></li>
		<li><a href="/rincon-sapiencia/afro-rep/">Afro Rep</a></li>
		<li><a href="/rincon-sapiencia/amores-as-escuras/">Amores às Escuras</a></li>
		<li><a href="/rincon-sapiencia/andar-com-fe/">Andar Com Fé</a></li>
		<li><a href="/rincon-sapiencia/rea-de-conforto/">Área de Conforto</a></li>
	</ul>
</div>
```

From this HTML block we already understand that, once on the musician's page, we can get the __song name__ and a __link__ for each song. That will be our first task.

Now let's do in Python exactly what we did here: access a musician's page and list their songs.

Since the first thing we'll do is __access a page__, we need to use Python's __requests__ library — a GET request with the URL we want should be enough:

```python
import requests

def get_all_musics(musician):
	all_musics = []
	
	# URL we'll scrape — in this case, the base Letras URL + the musician name
	url = "https://www.letras.com/{}".format(musician)
	
	# Web request to our built URL — returns an HTTP result
	response = requests.get(url)

	# From that result, we can get its content — a list of bytes representing our HTML
	html = response.content

	return all_musics
```

As things stand, the code still returns only an empty list. We still need to populate `all_musics` with the content of the HTML elements we observed.

Since we already have the HTML, we just need to work with it. We'll use the __[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)__ library. It will make it easy to filter elements by id and class without needing to learn CSS selectors or XPath (I'll reserve a post just for that).

To install it, use pip:

```bash
pip install beautifulsoup4
```

Now let's transform our request content into an object that can be filtered to find the song URL and name.

```python
import requests
from bs4 import BeautifulSoup

def get_all_musics(musician):
	all_musics = []
	
	# URL we'll scrape
	url = "https://www.letras.com/{}".format(musician)
	
	# Web request to our built URL
	response = requests.get(url)

	# Get the raw HTML content
	html = response.content

	# Parse into an object we can work with
	soup = BeautifulSoup(html, 'html.parser')

	# Capture the div element with class 'cnt-list--alp'
	all_songs = soup.find('div', {'class': 'cnt-list--alp'})

	# From the element stored in all_songs, search its children for 'li' tags
	song_list = all_songs.find_all('li')

	return all_musics
```

We're still not returning anything, but if we return `song_list` we'll get something like this:

```
[
	<li><a href="/rincon-sapiencia/a-coisa-ta-preta/" id="A">A Coisa Tá Preta</a></li>,
	 <li><a href="/rincon-sapiencia/a-noite-e-nossa/">A Noite é Nossa</a></li>,
	 <li><a href="/rincon-sapiencia/a-volta-pra-casa/">A Volta pra Casa</a></li>,
	 <li><a href="/rincon-sapiencia/afro-rep/">Afro Rep</a></li>,
	 <li><a href="/rincon-sapiencia/amores-as-escuras/">Amores às Escuras</a></li>,
	 <li><a href="/rincon-sapiencia/andar-com-fe/">Andar Com Fé</a></li>,
	 <li><a href="/rincon-sapiencia/rea-de-conforto/">Área de Conforto</a></li>,
	 <li><a href="/rincon-sapiencia/autentico-x-excentrico-x-incomparavel/">Autêntico X Excêntrico X Incomparável</a></li>,
	 <li><a href="/rincon-sapiencia/batidao/" id="B">Batidão</a></li>,
	 <li><a href="/rincon-sapiencia/bencao/">Benção (part. William Magalhães)</a></li>,
	 <li><a href="/rincon-sapiencia/coisas-de-brasil/" id="C">Coisas de Brasil</a></li>,
	 [...]
```

This is a list with all the songs on that page. Now we just need to extract the URL and song name. We'll continue using BeautifulSoup and add the following lines to the previous code:

```python
	for song_elem in song_list:
		# Note that href is inside the 'a' tag, inside our captured 'li'
		link = song_elem.find('a')['href']
		name = song_elem.find('a').text
		# Concatenate with the base URL
		link = 'https://www.letras.com' + link

		song = {
			"url": link,
			"name": name
		}

		all_musics.append(song)
```

Now `all_musics` contains a dictionary with the name and link of each song! With just a few lines of code we've already done something interesting, but that's not our final goal yet. Our next step is to take this list and, for each song, capture the lyrics by accessing the URL.

{{< figure src="/images/web-scrapping-letras/letras_letra_da_musica.png">}}

Inspecting the element that holds the lyrics, we get this:

```html
<div class="cnt-letra p402_premium" style="font-size: 19px;">
	<article>
		<p>Salve!
		<br>OK!<br>
		Rincon Sapiência, também conhecido como Manicongo, certo?
		...
```

So we can write a script similar to the previous one, but now filtering by the class `cnt-letra` and getting all the text content within it:

```python
def get_lyric_from_url(url):
	response = requests.get(url)
	soup = BeautifulSoup(response.content, 'lxml')
	lyric = soup.find('div', 'cnt-letra').getText(separator=' ')

	return lyric
```

If we run `get_lyric_from_url` for any Letras.com song URL, we'll already have the lyrics as a string.

Now we have a method that captures all songs by a given musician and another that captures the lyrics for a given URL. To keep this post from getting too long, I'll stop here. I still plan to use this code for a post on natural language processing and data visualization — but that's for the future.

Here's the final code for all of our work, with the bonus of generating a JSON file storing everything that was captured!

```python
import json
import requests
from bs4 import BeautifulSoup

def get_all_musics(musician):
	all_musics = []
	
	url = "https://www.letras.com/{}".format(musician)
	response = requests.get(url)
	html = response.content
	soup = BeautifulSoup(html, 'html.parser')
	all_songs = soup.find('div', {'class': 'cnt-list--alp'})
	song_list = all_songs.find_all('li')

	for song_elem in song_list:
		link = song_elem.find('a')['href']
		name = song_elem.find('a').text
		link = 'https://www.letras.com' + link

		song = {
			"url": link,
			"name": name
		}

		all_musics.append(song)

	return all_musics

def get_lyric_from_url(url):
	response = requests.get(url)
	soup = BeautifulSoup(response.content, 'lxml')
	lyric = soup.find('div', 'cnt-letra').getText(separator=' ')

	return lyric

musician_code = 'rincon-sapiencia'

songs = get_all_musics(musician_code)

for song in songs:
	lyric = get_lyric_from_url(song['url'])
	song['lyric'] = lyric

with open('songs_{}.json'.format(musician_code), 'w') as file_o:
	file_o.write(json.dumps(songs))
```
