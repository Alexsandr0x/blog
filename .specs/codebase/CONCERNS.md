# Concerns

## High Priority

### ~~1. Sidebar about section is broken/invisible~~ ✅ FIXED (2026-05-12)
- Added `[params.about]` (title, description) and `[[params.socialLinks]]` for LinkedIn and GitHub

### ~~2. `config.toml` typo: `indentifier` instead of `identifier`~~ ✅ FIXED (2026-05-12)
- Also fixed `baseURL` from `http://` to `https://`

### ~~3. Hugo version is 2+ years outdated~~ ✅ FIXED (2026-05-12)
- Updated from 0.108.0 → 0.161.1; removed separate Dart Sass step (built into extended since 0.114.0)

### ~~4. GitHub Actions versions are stale~~ ✅ FIXED (2026-05-12)
- checkout@v3→v6.0.2, configure-pages@v2→v6.0.0, upload-pages-artifact@v1→v5.0.0, deploy-pages@v1→v5.0.0

## Medium Priority

### 5. Lessons section is empty
- `content/lessons/_index.md` exists but has zero lesson content
- Menu item "Lessons" leads to an empty page — confusing for visitors
- **Options**: Add content, hide from menu, or remove section

### 6. No English translations for posts
- Both posts exist only in pt-br
- English `About` page exists but posts aren't translated
- Language switcher will show `en` link on posts that leads to a 404 or blank
- **Fix**: Either add English translations or hide the language switcher on posts without translations

### 7. Posts section is sparse
- Only 2 posts: one from 2018, one from 2022
- `web-scrapping-letras` post (2018) uses an old Letras.com HTML structure that may be outdated
- The `python-parallelism` post explicitly mentions a "Part 2" that never came

### 8. No SEO metadata
- `<head>` only has title + description (from `[params.about]`, which isn't configured)
- Missing: Open Graph tags, Twitter Card tags, canonical URL, author meta
- **Fix**: Override `head.html` partial in site-level `layouts/` to add OG/Twitter tags

## Low Priority

### 9. Academicons loaded but unused
- `academicons.min.css` is loaded on every page but no academic icons are used
- Small performance cost (extra CDN request)
- **Fix**: Remove if no academic profile links are planned

### 10. No favicon
- No `static/favicon.ico` or `<link rel="icon">` in head
- Browsers show a blank tab icon
- **Fix**: Add a favicon to `static/`

### 11. No syntax highlighting configuration
- Hugo has built-in Chroma syntax highlighting via `markup.highlight` config
- Not configured — uses defaults (no line numbers, default style)
- Posts with code blocks would benefit from explicit configuration

### 12. `.gitmodules` path mismatch
- `.gitmodules` declares `path = risotto` but the actual path is `themes/risotto`
- This works only because the theme files are already committed/present
- A fresh clone with `git submodule update --init` would fail or place files incorrectly
- **Fix**: Correct the path in `.gitmodules` to `themes/risotto` (or re-add the submodule correctly)
