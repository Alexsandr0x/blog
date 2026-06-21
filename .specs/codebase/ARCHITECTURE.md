# Architecture

## Page Layout (CSS Grid)

```
┌─────────────────────────────────────┐
│              HEADER                 │  logo + nav (About, Posts, Lessons)
├──────────────────────┬──────────────┤
│                      │    ASIDE     │  about section + social links
│       BODY           │  (15rem col) │
│   (main content)     ├──────────────┤
│                      │  aside block │  post metadata (description, author, date)
├──────────────────────┴──────────────┤
│              FOOTER                 │  copyright + powered by
└─────────────────────────────────────┘
```

Responsive: single-column on mobile, 2-column (body + aside) above 45rem.

## Hugo Content Organization

```
content/
├── about/
│   ├── index.en.md          # English about page
│   └── index.pt-br.md       # Portuguese about page
├── homepage/
│   └── index.md             # Headless bundle (no output), used by theme's about partial
├── lessons/
│   └── _index.md            # Section index only — NO lesson content yet
└── posts/
    ├── _index.md            # Section index (bilingual aliases)
    ├── python-parallelism/
    │   └── python-parallelism.pt-br.md   # pt-br only
    └── web-scrapping-letras/
        └── web-scrapping-letras.pt-br.md # pt-br only
```

## Theme Layout Templates

```
themes/risotto/layouts/
├── _default/
│   ├── baseof.html    # Base template: head + header + body + aside + footer
│   ├── list.html      # Section/taxonomy list pages
│   ├── single.html    # Individual post/page template
│   └── li.html        # List item partial
├── post/
│   └── list.html      # Override list for "post" content type
├── partials/
│   ├── head.html      # <head>: title, meta, CSS links
│   ├── header.html    # Logo + nav menu
│   ├── about.html     # Sidebar: logo, title, description, social links
│   ├── footer.html    # Copyright + attribution
│   └── lang.html      # Language switcher
└── index.html         # Homepage
```

## CSS Architecture

```
static/css/
├── risotto.css         # Entry point: @import chain
├── colours.css         # CSS vars: --bg, --fg, --link, --hover, etc. (mapped from palette vars)
├── layout.css          # Page grid
├── header.css          # Header + nav
├── logo.css            # Logo styling
├── about.css           # Sidebar about section
├── footer.css          # Footer
├── typography.css      # Font settings, prose styles
├── custom.css          # Empty — override point for site-level customization
└── palettes/
    ├── base16-dark.css  # Default palette
    ├── base16-light.css
    ├── gruvbox-dark.css
    └── gruvbox-light.css
```

## Data Flow: Build → Deploy

1. Push to `main`
2. GitHub Actions installs Hugo 0.108.0 extended + Dart Sass
3. Checks out repo with `submodules: recursive` (fetches risotto theme)
4. Runs `hugo --minify --baseURL <pages-url>`
5. Uploads `./public/` as Pages artifact
6. Deploys artifact to GitHub Pages

## Multilingual Routing

- Default language: `pt-br` → URLs at `/posts/`, `/about/`
- English: `/en/posts/`, `/en/about/`
- Language switcher: `partials/lang.html`
- Posts currently have **no English translations** (only pt-br files exist)
