# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio/marketing site for Johan Garcia (johangarcia.com) — a Fractional CMO & digital marketing professional. The actual Astro project lives inside the `Johan-Garcia/` subdirectory (not the repo root).

## Commands

All commands must be run from `Johan-Garcia/`:

```bash
cd Johan-Garcia
npm run dev        # Dev server at localhost:4321
npm run build      # Type-check (astro check) then build to dist/
npm run preview    # Preview production build locally
```

## Architecture

- **Framework**: Astro 5.x with TypeScript (strict config)
- **Single-page site**: Only one page at `src/pages/index.astro` — a self-contained SPA-style page with all sections (hero, about, services, case studies, contact) and all CSS/JS inline
- **Unused components**: `src/components/` has Card, ContactForm, Header, Footer, and `src/layouts/Layout.astro` — these were scaffolded but are **not imported** by `index.astro`. The index page has its own standalone markup, styles, and scripts.
- **Static assets**: Images in `public/media/`, favicon in `public/favicon.svg`
- **Contact form**: Uses Formspree (`formspree.io`) in the ContactForm component (currently unused)
- **No CSS framework**: All styling is vanilla CSS with scoped `<style>` blocks
- **Brand colors**: Primary purple `#7c60d5`, secondary `#5a4ad1`, accent `#a18ff7`, blue gradient `#3a8dde`
- **Mobile nav**: Hamburger menu with JS toggle in `index.astro` `<script>` block

## Key Considerations

- The `index.astro` page does NOT use the Layout component — it has its own full HTML document structure
- Spanish comments appear throughout the CSS/JS (the developer is bilingual)
- The `.claude/settings.local.json` is gitignored (contains Hostinger API token for MCP server)
