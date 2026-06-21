# Structure

```
blog/
├── .github/
│   └── workflows/
│       └── hugo.yml              # CI/CD: build + deploy to GitHub Pages
├── .gitmodules                   # Theme submodule: risotto → themes/risotto/
├── .hugo_build.lock              # Hugo build lock file
├── archetypes/
│   └── default.md                # Default front matter for `hugo new` commands
├── config.toml                   # Main Hugo config: baseURL, languages, menu, params
├── content/
│   ├── about/
│   │   ├── index.en.md           # About page (English)
│   │   └── index.pt-br.md        # About page (Portuguese)
│   ├── homepage/
│   │   └── index.md              # Headless bundle for homepage aside content
│   ├── lessons/
│   │   └── _index.md             # Lessons section — EMPTY (no posts)
│   └── posts/
│       ├── _index.md             # Posts section index
│       ├── python-parallelism/
│       │   └── python-parallelism.pt-br.md   # Post: Python concurrency (2022-12-28)
│       └── web-scrapping-letras/
│           └── web-scrapping-letras.pt-br.md # Post: Web scraping (2018-09-01)
├── static/
│   └── images/
│       ├── python-parallelism/   # 8 assets (PNGs + GIFs)
│       └── web-scrapping-letras/ # 2 assets (PNGs)
└── themes/
    └── risotto/                  # Git submodule (joeroe/risotto)
        ├── layouts/              # Hugo templates
        ├── static/css/           # Theme CSS (palettes, components)
        ├── exampleSite/          # Theme demo — not used by this blog
        └── theme.toml            # Theme metadata
```

## Content Inventory

| Section  | Posts | Languages     | Status         |
|----------|-------|---------------|----------------|
| posts    | 2     | pt-br only    | Active (sparse)|
| lessons  | 0     | —             | Empty          |
| about    | 1     | pt-br + en    | Complete       |

## Post Inventory

| Slug                    | Title                                            | Date       | Lang   |
|-------------------------|--------------------------------------------------|------------|--------|
| python-parallelism      | Basico de Concorrência e Paralelismo em Python   | 2022-12-28 | pt-br  |
| web-scrapping-letras    | Requests + BeautifulSoup para captura de dados web | 2018-09-01 | pt-br  |
