# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

@AGENTS.md

## This Site

This is **Clement Wong's personal academic website**, built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme.

- **Live URL:** https://clementwong.github.io/al-folio
- **`url`** in `_config.yml`: `https://clementwong.github.io`
- **`baseurl`** in `_config.yml`: `/al-folio` (project site, not root)

> The `scholar:` section in `_config.yml` still has the default `last_name: [Einstein]` placeholder — update it to `last_name: [Wong]` / `first_name: [Clement]` when personalizing the bibliography.

## Key Architecture

This is a **Jekyll static site** — there is no backend. All content is rendered at build time.

| Concern                          | Where to edit                               |
| -------------------------------- | ------------------------------------------- |
| Site identity, features, plugins | `_config.yml`                               |
| About/bio page                   | `_pages/about.md`                           |
| Publications                     | `_bibliography/papers.bib`                  |
| CV data                          | `_data/cv.yml` or `assets/json/resume.json` |
| Social links                     | `_data/socials.yml`                         |
| Co-author display names          | `_data/coauthors.yml`                       |
| Blog posts                       | `_posts/YYYY-MM-DD-title.md`                |
| News items                       | `_news/`                                    |
| Projects                         | `_projects/`                                |
| Styling overrides                | `_sass/` (SCSS)                             |
| Reusable UI components           | `_includes/` (Liquid)                       |
| Page templates                   | `_layouts/` (Liquid)                        |

## Before Committing

1. Run `npx prettier . --write` (install once: `npm install --save-dev prettier @shopify/prettier-plugin-liquid`)
2. Verify the build locally with `docker compose up --build` and visit http://localhost:8080
