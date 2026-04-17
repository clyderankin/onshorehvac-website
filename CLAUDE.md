# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Marketing website for **Onshore Mechanical, Inc.**, a commercial HVAC/electrical/refrigeration contractor in Huntington Beach, CA. Built with Hugo using a custom theme called "onshore".

## Commands

- **Dev server:** `hugo server` (serves at localhost:1313 with live reload)
- **Build:** `hugo` (outputs to `public/`)
- Hugo version: 0.123.7+extended

## Architecture

This is a standard Hugo site with a single custom theme (`themes/onshore/`). There is no build toolchain beyond Hugo itself — no npm, no bundler.

### Content (`content/`)

Markdown files with YAML front matter. Two main content sections:
- `services/` — individual service pages (HVAC, electrical, refrigeration, etc.)
- `industries/` — industry-specific pages (restaurants, healthcare, etc.)

Standalone pages: `about.md`, `careers.md`, `contact.md`. Each uses `type: "page"` in front matter to select its layout.

Content pages use `description` in front matter as a subtitle/tagline displayed in hero sections and card grids. The `capabilities` front matter param (list of strings) renders a grid on single pages. The `label` param controls card display text.

### Theme (`themes/onshore/`)

- `layouts/index.html` — Homepage with hardcoded sections (hero, stats, clients, reviews, service area, CTA). Services and industries cards are generated dynamically from content.
- `layouts/_default/baseof.html` — Base template: head partial, header, main block, footer, JS.
- `layouts/_default/list.html` — Section list pages (card grid of child pages).
- `layouts/_default/single.html` — Default content page (hero + capabilities grid + content + CTA).
- `layouts/page/single.html`, `contact.html`, `careers.html` — Type-specific page layouts.
- `layouts/partials/` — `head.html`, `header.html`, `footer.html`.
- `static/css/main.css` — All styles in one file. Uses CSS custom properties. DM Sans + JetBrains Mono from Google Fonts.
- `static/js/main.js` — Client-side JS (scroll animations via IntersectionObserver `reveal` classes, mobile nav).

### Configuration (`hugo.toml`)

Site params include `phone`, `address`, `tagline`, `description`, and social links. Navigation defined under `[menu]`. Goldmark renderer set to `unsafe = true` to allow raw HTML in markdown.
