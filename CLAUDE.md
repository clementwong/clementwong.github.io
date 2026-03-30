# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

**al-folio** — a Jekyll-based academic portfolio theme. The repo is both the theme template and a live site. Key features: publications (BibTeX/jekyll-scholar), CV, blog posts, projects, and Jupyter notebook embedding.

## Essential Commands

### Local Development

```bash
# Start dev server (recommended)
docker compose pull && docker compose up
# Site at http://localhost:8080

# Rebuild after Dockerfile/dependency changes
docker compose up --build

# Stop and free port 8080
docker compose down
```

### Pre-Commit (mandatory before every commit)

```bash
# 1. Format code
npm install --save-dev prettier @shopify/prettier-plugin-liquid  # first time only
npx prettier . --write

# 2. Verify the build
docker compose up --build
# Visit http://localhost:8080 — check navigation, pages, images, dark mode
```

Prettier formatting is enforced by CI (`prettier.yml`) and will fail PRs if skipped.

## Architecture & Key Files

### Configuration

- **`_config.yml`** — primary config: `url`, `baseurl`, feature flags (`enabled: true/false`), author info. `url` + `baseurl` must be set correctly together or CSS/assets won't load.
- **`_data/`** — YAML data: `socials.yml`, `cv.yml`, `coauthors.yml`, `repositories.yml`, `venues.yml`
- **`_bibliography/papers.bib`** — BibTeX source for the publications page (processed by jekyll-scholar)

### Content Directories

- `_posts/` — blog posts, filename format `YYYY-MM-DD-title.md`
- `_pages/` — static pages (about, cv, publications, projects, teaching)
- `_projects/` — project showcase entries
- `_news/` — news/announcements
- `_teachings/` — course entries

### Templates & Styling

- `_layouts/` — page layouts (`about.liquid`, `post.liquid`, `bib.liquid`, `distill.liquid`, `cv.liquid`)
- `_includes/` — reusable Liquid components
- `_sass/` — SCSS stylesheets
- `_scripts/` — JavaScript

### CI/CD

- **`deploy.yml`** — builds with `JEKYLL_ENV=production`, runs purgecss, deploys to `gh-pages` branch
- **`prettier.yml`** — formatting gate; fails PRs on unformatted code

## Critical Config Rules

- **Personal site:** `url: https://username.github.io` + `baseurl:` (empty)
- **Project site:** `url: https://username.github.io` + `baseurl: /repo-name/`
- Quote YAML strings containing `:`, `&`, or `#`: `title: "My: Cool Site"`

## Common Pitfalls

| Problem | Cause | Fix |
|---|---|---|
| No CSS/styling after deploy | Wrong `url`/`baseurl` | Fix both values in `_config.yml`, clear browser cache |
| "Zero vectors cannot be normalized" | Empty blog post content | Add meaningful content, or set `related_posts: false` in frontmatter |
| Port 8080 in use | Existing container | `docker compose down` |
| PR fails prettier check | Code not formatted | `npx prettier . --write` before committing |

## Instruction Files by File Type

| File Type | Instruction File |
|---|---|
| Markdown (`_posts/`, `_pages/`) | `.github/instructions/markdown-content.instructions.md` |
| YAML config | `.github/instructions/yaml-configuration.instructions.md` |
| BibTeX | `.github/instructions/bibtex-bibliography.instructions.md` |
| Liquid templates | `.github/instructions/liquid-templates.instructions.md` |
| JavaScript | `.github/instructions/javascript-scripts.instructions.md` |
