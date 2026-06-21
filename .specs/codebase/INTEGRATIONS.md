# Integrations

## Deployment
- **GitHub Pages** — static hosting, free, served from the `gh-pages` environment
- **GitHub Actions** — CI/CD pipeline defined in `.github/workflows/hugo.yml`

## CDN Dependencies (loaded in every page)
- **Font Awesome 6.1.2** — icons in social links sidebar (`https://cdnjs.cloudflare.com`)
- **Academicons 1.9.1** — academic icons, loaded but not visibly used in current config

## Content Embeds (used in posts)
- **GitHub Gist** — `{{< gist >}}` shortcode embeds code snippets inline
  - Used in `python-parallelism` post (multiple gists from user `Alexsandr0x`)
  - Loads Gist JS from `gist.github.com` at runtime

## NOT Integrated (but theme supports)
- **Social links** — `[params.socialLinks]` config exists in theme but not set in `config.toml`
- **About sidebar** — `[params.about]` block (title, description, logo) not configured
- **Analytics** — no tracking (Google Analytics, Plausible, etc.)
- **Comments** — no comment system (Disqus, Giscus, etc.)
- **Search** — no search functionality
- **RSS** — Hugo auto-generates `/index.xml` but not exposed in UI
- **Sitemap** — Hugo auto-generates `sitemap.xml`

## External Links in Content
- `https://github.com/project-neon` — robotics team
- `https://nucleodetecnologia.com.br/` — MTST teaching experience
- `https://www.sirius.education/` — Sirius Education teaching experience
- `https://www.letras.com` — referenced in web scraping post
