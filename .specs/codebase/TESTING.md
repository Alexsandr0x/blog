# Testing

## Current State

There are **no automated tests** in this repository.

## What Exists

- Hugo build (`hugo --minify`) is the only validation gate — it fails on template errors or broken shortcodes
- GitHub Actions CI runs the build on every push to `main`, which acts as a smoke test

## Recommended Testing Approach

For a Hugo static blog, meaningful verification is:

1. **Local build**: `hugo server -D` — run locally and visually inspect pages
2. **Build gate**: `hugo --minify` exits non-zero on broken templates/content
3. **Link checking**: a tool like `muffet` or `htmltest` on the `./public/` output to catch broken internal links
4. **HTML validation**: `html-proofer` or similar on `./public/`

## Notes for Feature Work

- No test commands to run before PRs
- All verification is manual + CI build success
- When adding new content/templates, test with `hugo server` locally first
