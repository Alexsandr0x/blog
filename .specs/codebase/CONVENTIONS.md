# Conventions

## File Naming

- Post directories: `kebab-case/` (e.g. `python-parallelism/`)
- Post files: `<slug>.<lang>.md` (e.g. `python-parallelism.pt-br.md`)
- About pages: `index.<lang>.md` within a directory
- Section indexes: `_index.md`

## Front Matter

Posts use YAML front matter (`---` delimiters):
```yaml
---
title: "Post Title"
translationKey: "slug-for-linking-translations"
date: 2022-12-28
description: "Short description shown in the aside sidebar"
---
```

Section indexes and about pages use TOML front matter (`+++` delimiters):
```toml
+++
title = "Posts"
translationKey = "posts"
tags = ["posts", "en"]
aliases = ["/pt-br/posts/"]
+++
```

## Translation Linking
- `translationKey` must match across language variants to link them in the language switcher
- English and pt-br variants share the same key

## Shortcodes Used

- `{{< figure src="/images/..." caption="..." >}}` — images with optional captions
- `{{< gist <user> <gist-id> <filename> >}}` — embeds GitHub Gist files inline

## Static Assets

- Images go in `static/images/<post-slug>/`
- Referenced as `/images/<post-slug>/file.ext` (no `/static/` prefix)

## Menu Items

Defined in `config.toml` under `[[menu.main]]` with fields:
- `identifier` (unique string ID)
- `name` (display label)
- `url` (relative path)
- `weight` (sort order, ascending)

## Content Languages
- Language suffix in filename determines Hugo routing: `.pt-br.md` → default, `.en.md` → `/en/`
- `defaultContentLanguage = 'pt-br'` means pt-br content serves at root paths
