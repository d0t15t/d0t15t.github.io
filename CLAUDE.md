# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page static portfolio site for Isaac Bigsby Trogdon, hosted at `d0t15t.github.io`. There is no build step, no package manager, and no JavaScript framework — the entire site is hand-authored `www/index.html` plus one `www/style.css`. Content edits mean editing `www/index.html` directly.

## Directory layout

All servable site files live under `www/` — `index.html`, `style.css`, `robots.txt`, `sitemap.xml`, `llms.txt`, `humans.txt`, `site.webmanifest`, `assets/`. Repo-root files (`README.md`, `CLAUDE.md`, `.github/`) are project scaffolding, not part of the deployed site. Any new page or asset for the live site goes inside `www/`.

## Local development

No build step means "running" the site is just serving `www/` and opening a browser:

```
python3 -m http.server 8080 --directory www
```

Open `http://localhost:8080`. This serves exactly what ships to GitHub Pages — no transformation — so it's the fastest way to sanity-check a change. For auto-refresh on save while iterating on markup/CSS, use `npx live-server www --port=8080` instead (via `npx` so no dependency gets added to the repo).

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which uploads `./www` (not the repo root) and deploys it to GitHub Pages via `actions/deploy-pages`. There is no build/compile step — whatever is committed under `www/` is what ships.

## Architecture notes

- `www/index.html` is the entire site: hero section, then `<section>` blocks for Projects, Open Source, Timeline, Philosophy, and Contact, anchored by in-page nav links (`#projects`, `#opensource`, `#timeline`, `#contact`). Keep new sections consistent with this single-file, semantic-HTML structure rather than introducing a templating system.
- `www/index.html` embeds JSON-LD (`schema.org/ProfilePage`) in a `<script type="application/ld+json">` block. If bio details (name, job title, skills in `knowsAbout`) change in the visible content, update this block too so it stays in sync.
- `www/style.css` is intentionally tiny (single line, no preprocessor). Follow its existing terse, single-line style rather than reformatting into multi-line/BEM conventions.
- SEO/crawler files under `www/` — `robots.txt`, `sitemap.xml`, `llms.txt`, `humans.txt`, `site.webmanifest` — are minimal and manually maintained. `sitemap.xml` currently has no `<url>` entries; add one if additional pages are ever introduced.
- `www/assets/` exists but is currently empty.
