# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Zola static site for King Audio Transcription & Typing Services (kingaudio.co.uk). Pure Zola project — no npm, no Makefile, no backend.

## Build & Development Commands

- `zola serve` — local dev server at http://127.0.0.1:1111 with live reload
- `zola build` — production build to `public/`
- `zola check` — validate content and config

## Architecture

**Content** (`content/`): Markdown files. The homepage (`_index.md`) is a single long page with anchor sections (services, testimonials, process, contact). Uses Zola front matter with aliases for legacy URLs.

**Templates** (`templates/`): Tera (Jinja2-like) templates that override the `after-dark` theme in `themes/after-dark/`. Key files:
- `index.html` — homepage with hero section, pulls in `page.content` and footer
- `page.html` — single page template
- `post_macros.html` — reusable macros (metadata display, KaTeX)

**Styling** (`sass/`): SCSS compiled by Zola. Modular structure:
- `_vendor.scss` — base framework (grid, forms, buttons)
- `_theme.scss` — theme animations and colors
- `_jpk.scss` — custom overrides (Mulish font, Gruvbox-inspired colors, form styling)

**Static assets** (`static/`): Mulish variable font files and images.

## Key Details

- Forms use **Netlify Forms** (`data-netlify="true"`) with a honeypot field ("alien-field") for spam protection. Form submits POST to `/contact_success`.
- Config is in `config.toml` (base_url, title, Sass settings).
- The theme (`themes/after-dark/`) is a vendored copy — template and style overrides go in the top-level `templates/` and `sass/` dirs, not in the theme directory.
- Deployed via Netlify from GitHub.
