# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page static portfolio site for Isaac Bigsby Trogdon, hosted at `d0t15t.github.io`. There is no build step, no package manager, and no JavaScript framework — the entire site is hand-authored `www/index.html` plus one `www/style.css`. Content edits mean editing `www/index.html` directly.

## Directory layout

All servable site files live under `www/` — `index.html`, `style.css`, `robots.txt`, `sitemap.xml`, `llms.txt`, `humans.txt`, `site.webmanifest`, `assets/`. Repo-root files (`README.md`, `CLAUDE.md`, `.github/`) are project scaffolding, not part of the deployed site. Any new page or asset for the live site goes inside `www/`.

## Deployment

Pushing to `master` triggers `.github/workflows/static.yml`, which uploads `./www` (not the repo root) and deploys it to GitHub Pages via `actions/deploy-pages`. There is no build/compile step — whatever is committed under `www/` is what ships. Verify changes by opening `www/index.html` in a browser; there's no local dev server or test suite.

## Architecture notes

- `www/index.html` is the entire site: hero section, then `<section>` blocks for Projects, Open Source, Timeline, Philosophy, and Contact, anchored by in-page nav links (`#projects`, `#opensource`, `#timeline`, `#contact`). Keep new sections consistent with this single-file, semantic-HTML structure rather than introducing a templating system.
- `www/index.html` embeds JSON-LD (`schema.org/ProfilePage`) in a `<script type="application/ld+json">` block. If bio details (name, job title, skills in `knowsAbout`) change in the visible content, update this block too so it stays in sync.
- `www/style.css` is intentionally tiny (single line, no preprocessor). Follow its existing terse, single-line style rather than reformatting into multi-line/BEM conventions.
- SEO/crawler files under `www/` — `robots.txt`, `sitemap.xml`, `llms.txt`, `humans.txt`, `site.webmanifest` — are minimal and manually maintained. `sitemap.xml` currently has no `<url>` entries; add one if additional pages are ever introduced.
- `www/assets/` exists but is currently empty.
