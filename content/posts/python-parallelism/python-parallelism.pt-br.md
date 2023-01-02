---
title: "Basico de Concorrência e Paralelismo em Python"
translationKey: "python-concurrent"
date: 2022-12-28
description: "Uma tentativa de explicar concorrência e paralelização com cachorros"
---

Esse foi um conteúdo básico elaborado para a tribo de sistemas multi-robóticos da equipe de robótica [Project Neon]() em agosto de 2022. O conteúdo é aberto a membros mas eu preferi fazer uma síntese com algumas correções nesta publicação.
 
Tornei o conteúdo mais agnóstico removendo as referências de robótica móvel. Espero que essa tentativa de tornar os conceitos de concorrência e paralelismo fáceis de entender seja efetivo para alguém!


## O que é Paralelização?

**Paralelização**, programação paralela, ou computação paralela é a **forma de resolver comandos dentro de um ambiente computacional ao mesmo tempo**.

Esse procedimento é muito útil em diversos segmentos da computação que precisam ter alto desempenho ou simplesmente fazer várias coisas ao mesmo tempo.

Por exemplo, o seu computador, neste momento desempenha várias ações paralelas: ele está gerenciando pacotes de rede que chegam para seu navegador, quando você escuta música ao mesmo tempo que joga um jogo, ambos softwares estão desempenhando papéis totalmente diferentes porém paralelos.

**Quando estamos programando um código simples, não é diferente**, às vezes queremos que nosso código faça mais de uma coisa ao mesmo tempo, mas com a programação estruturada como conhecemos não é possível.

{{< figure src="/images/python-parallelism/serial-vs-parallel.png" caption="Comunicação Serial e Paralela em redes é um ótimo **paralelo** para nossa discussão.">}}

Usualmente programamos de forma **serial**, ou seja, os comandos têm uma ordem lógica, bem estruturada e um por vez. Quando você aplica vários comandos *print* no python ou em qualquer linguagem você tem a certeza que eles irão sempre rodar na mesma ordem.

Agora, quando aplicamos uma estratégia paralela, podemos fazer comandos rodando ao mesmo tempo de forma independente.


## Paralelização vs Concorrência

Para entender na prática o uso de paralelização, é preciso entender dois conceitos importantíssimos: **Paralelização** e **Concorrência**. Aqui, iremos tornar a palavra paralelização mais restrita a uma definição clara enquanto teremos um novo conceito que é a concorrência.
 
Concorrência diz respeito a processos que executam disputando um mesmo recurso, esse recurso pode ser a memória do computador por exemplo. Dessa concorrência pode ocorrer de forma que esses processos se revezam no consumo desse recurso.
 
{{< figure src="/images/python-parallelism/concurrent-model.png">}}
 
Note que no exemplo concorrente, temos duas tarefas, A e B, ambas rodam ao mesmo tempo, porém, para uma ser processada, a outra deve parar, fazendo com que o tempo total para executar as duas tarefas ao mesmo tempo seja A + B.
 
Paralelização já diz respeito a processos que executam de forma simultânea e independente. Podendo ou não compartilhar recursos.
 
{{< figure src="/images/python-parallelism/parallel-model.png">}}
 
Já no paralelo, a execução pode ser ao mesmo tempo, no caso da imagem, rodando em CPUs diferentes. Sempre que dois processamentos forem independentes, por definição, se pode usar paralelização. Sempre que dois processamentos compartilham de algum recurso e precisam se dividir no uso dele, podemos usar a concorrência.


## Alimentando Cachorros

Para fixar essa noção, podemos usar um conceito lúdico da disputa de dois cachorros tentando comer 1 pote de ração.
 
{{< figure src="/images/python-parallelism/parallel-dogs-2.png">}}
 
Considerando os dois cachorrinhos como processos e o pote de ração como o recurso a ser disputado, a solução aqui é o caminho serial do cachorro C1 comer primeiro até que sua fome seja saciada e só depois o C2 tem a sua chance de comer.
 
Não é necessário ter experiência cuidando de animais para entender que esse caminho tem vários problemas, e não é diferente na orquestração de processos. Se o recurso for tempo, C1 pode demorar demais e não dar oportunidade para C2, se a quantidade de petiscos no pote for limitada C2 pode passar fome.
 
{{< figure src="/images/python-parallelism/parallel-dogs-3.png">}}
 
Numa alternativa concorrente, podemos colocar os cachorrinhos C1 e C2 comerem de forma intervalada, sendo regidos por alguma regra, como tempo (cada um como por 1 min e depois dá acesso ao recurso para o outro por exemplo).
 
Se a regra for bem pensada evitamos problemas de escassez de recursos como tempo.
 
{{< figure src="/images/python-parallelism/parallel-dogs-4.png">}}
 
Por fim, temos a solução paralela, onde ambos processos se alimentam de forma independente, porém do mesmo recurso.

## Mão na Massa: Cachorros no Python!

Agora que entendemos o que é concorrência e o que é paralelismo vamos fixar de uma vez por todas praticando esses conceitos com Python!
 
Para isso, vamos primeiro bolar uma classe que irá representar nossos cachorrinhos:
 
{{< gist Alexsandr0x bd7b86b51fd4faccff23793249a6d893 dog.py>}}
 
Com esse código podemos inicializar diferentes cachorros de forma que eles se alimentem de uma variável `pot`. Essa variável será uma lista que terá recursos finitos. Note que o `food_necessary` é definido como 10, ou seja, para que nosso cachorro esteja saciado, ele precisará comer pelo menos 10 petiscos.
 
Para entender esse código antes de observar ele nas ocasiões serial, concorrente e paralela vamos entender o que acontece quando colocamos para o cachorro se alimentar.
 
{{< gist Alexsandr0x bd7b86b51fd4faccff23793249a6d893 simple_use_dog.py >}}
 
Esse código nos dará o seguinte resultado:
 
{{< figure src="/images/python-parallelism/dog_example.gif">}}
 
Dessa forma, sabemos o comportamento quando o cão está sozinho, 10 petiscos para se alimentar, e 10 no pote, bem simples.
 
Note que temos uma regra onde abaixo de 50% o cachorro pode morrer de fome! então se tivermos dois cachorros e 10 petiscos temos exatamente o necessário para alimentá-los porém na programação serial essa lógica ira sempre matar o segundo cachorro!
 
Agora, se tivermos dois cachorros em um código serial...
 
{{< gist Alexsandr0x bd7b86b51fd4faccff23793249a6d893 double_dog.py>}}
 
{{< figure src="/images/python-parallelism/double_dog_example.gif">}}
 


## Python Threads como solução concorrente
 
Uma solução para o caso dos dois doguinhos que disputam comida é que eles comam usando uma estratégia concorrente. Uma das soluções concorrentes do Python é o módulo `Thread`. Nele, podemos criar métodos que serão executados de forma concorrente e gerenciados pelo python entre as suas trocas. Não teremos exatamente o controle de quando um cachorro para de comer, mas o que o Python irá fazer é sempre que usamos um comando de parada de thread, como o `time.sleep`, ele irá verificar se existe outra thread apta a trabalhar enquanto a outra fica dormindo.
 
Para isso, precisamos fazer esse while que criamos ser um método, que chamaremos de `task`. O objeto `Thread`  irá receber como parâmetro esse método, e também receberá os argumentos da função no argumento posicional `args`.
 
{{< gist Alexsandr0x bd7b86b51fd4faccff23793249a6d893 thread_dogs.py>}}
 
E com isso temos...
 
{{< figure src="/images/python-parallelism/thread_dogs.gif">}}
 
*Perfectly balanced, as all things should be...*
 
É importante dizer que o exemplo alcançou exatamente 50% com as duas threads se intercalando perfeitamente, mas nem sempre sera assim, ainda mais numa aplicação complexa em que o Python estará gerenciando tantas outras threads que estarão disputando recursos. Mas esse pequeno exemplo já mostra um caso onde a concorrência é benéfica.
 
## E a solução paralela?
 
Eu havia bolado uma explicação paralela para esse conteúdo quando o criei, hoje não estou totalmente satisfeito com ele, a abordagem paralela exige alguns conceitos complexos como compartilhamento de memória e condições de corrida que talvez caibam em outro lugar...
 
Quem sabe um dia revisito esse conteúdo numa parte 2 desse texto...
 
## Referências
 
Esse texto foi baseado no meu próprio conteúdo para uma aula que preparei focado em calouros da equipe de robótica da Universidade Federal do ABC. Que por sua vez teve como base principalmente ***Luciano Ramalho** - Python Fluente* e ***Shaw, A** - CPython internals: your guide to the Python 3 interpreter*.