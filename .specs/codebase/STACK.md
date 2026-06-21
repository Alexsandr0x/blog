# Stack

## Static Site Generator
- **Hugo** `0.108.0` (extended) — declared in `.github/workflows/hugo.yml`
  - ⚠️ outdated: released Dec 2022; current is 0.147+
  - Uses `hugo --minify` for production builds

## Theme
- **Risotto** — minimalist, terminal-ricing aesthetic (dark mode, responsive CSS grid)
  - Linked as a **git submodule** at `themes/risotto/`
  - Source: `https://github.com/joeroe/risotto`
  - MIT licensed
  - No JavaScript — pure HTML + CSS
  - CSS custom properties for theming; palette loaded at runtime via `css/palettes/*.css`

## Deployment
- **GitHub Pages** via **GitHub Actions** (`hugo.yml`)
  - Trigger: push to `main`
  - Build → upload artifact → deploy
  - Actions used: `checkout@v3`, `configure-pages@v2`, `upload-pages-artifact@v1`, `deploy-pages@v1`
  - ⚠️ All action versions are old (v3/v2/v1)

## Languages / Content
- Hugo multilingual mode: `pt-br` (default, weight 1) + `en` (weight 2)
- Content written in **Markdown** with TOML or YAML front matter
- Shortcodes used: `figure`, `gist`

## Fonts & Icons (CDN)
- **Font Awesome 6.1.2** (CDN, integrity hash)
- **Academicons 1.9.1** (CDN, integrity hash)

## Domain
- `alexsandro.dev` — set as `baseURL` in `config.toml`
