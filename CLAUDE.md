# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal site for dreamformula.com: a single hand-written static page. There is no build step, package manager, test suite, or linter. The repo name and early history refer to Sculpin (a PHP static site generator), but that was removed. The untracked `.sass-cache/` is left over from that setup and is not used.

The site is hosted on GitHub Pages and deployed from the root of the `main` branch, so every committed file is public. `CNAME` sets the custom domain. `.nojekyll` turns off Jekyll; without it, Pages drops `.well-known/` and may render `index.md` over `index.html`. Don't delete either file.

To preview locally, serve the repo root with any static server, e.g. `python3 -m http.server` and open http://localhost:8000/.

## Structure

- `index.html` — the page. Plain HTML with all metadata inline: OpenGraph/Twitter cards, a schema.org `Person` JSON-LD block, geo meta tags, and `rel="me"` profile links.
- `index.css` — all styles. It uses CSS custom properties on `:root` for colors and the three font stacks (`--serif`, `--sans`, `--fixed`). Class names are BEM-ish with a prefix: `site--*`, `post--*`, `l-*` for layout. The full-width colored bands between sections are `site--breaker site--breaker_{blue,green,red,yellow}`.
- `index.md` — a Markdown copy of the page content, linked from `index.html` as `rel="alternate" type="text/markdown"`.
- `llms.txt`, `humans.txt`, `robots.txt`, `sitemap.xml`, `.well-known/security.txt` — machine-readable site files.
- `talks.csv` — full speaking history (`Date,Event,City/Virtual,Type,Title/Topic,Link/Notes,URL`). The page lists only selected highlights.
- `assets/` — favicon and the 1200×630 social card used by the OG/Twitter image tags.

## Keeping content in sync

The same content is duplicated by hand across several files. When you edit page content, update every copy:

- Prose, section headings, and "Selected highlights/work" lists: `index.html` **and** `index.md`.
- Profile links (Drupal.org, GitHub, LinkedIn, Bluesky): `index.html` (both the visible list and the JSON-LD `sameAs` array), `index.md`, and `llms.txt`.
- Site description/tagline: `<meta name="description">`, `og:description`, `twitter:description`, and the summary in `llms.txt`.
- New public files or URLs: add them to `sitemap.xml` and, where relevant, to the "Site Files" list in `index.md` and "Primary Sources" in `llms.txt`.
- New talks: add a row to `talks.csv`. Change the page's highlights list only if the talk should be featured.
