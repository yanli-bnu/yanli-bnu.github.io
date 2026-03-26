# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Install dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll serve
# or use the convenience script:
bash run.sh

# Build for production
bundle exec jekyll build
```

The site auto-deploys to GitHub Pages on push to `master` via `.github/workflows/jekyll.yml`.

## Architecture

This is a **single-page Jekyll site** (Jekyll 4.1). Almost all content lives in `index.html` — the nav links (`/#research`, `/#publications`, `/#team`, `/#links`) are anchor links to sections on that page, not separate pages.

**Data-driven sections** — Publications and team members are stored in YAML and rendered via Liquid loops:
- `_data/publications.yml` — grouped by `category`, each entry has `authors`, `year`, `title`, `journal`, `url`. Bold authors use `**Name**` markdown syntax, processed with `| markdownify | remove: '<p>' | remove: '</p>'`.
- `_data/team.yml` — two keys: `current` and `alumni`, each a list with `name`, `role`, and optional `note`.

**Layout** — `_layouts/default.html` is the only active layout. `_layouts/news.html` and `_layouts/post.html` exist but are unused/legacy.

**Styling** — `css/main.css` uses CSS custom properties (gold/navy theme). Fonts loaded from Google Fonts (Playfair Display + Inter).

**`_includes/google_analytics.html`** exists but is not included anywhere — it is dead code.

## Content Updates

- **Add a publication**: append an entry under the appropriate `category` in `_data/publications.yml`
- **Update team**: edit `_data/team.yml`
- **Edit bio/research/links**: edit `index.html` directly (those sections are hardcoded HTML, not data-driven)
