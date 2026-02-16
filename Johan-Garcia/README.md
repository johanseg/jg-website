# johangarcia.com

Personal website for Johan Garcia — AI Growth Architect & Performance Marketing Strategist.

Built with [Astro](https://astro.build), deployed at [johangarcia.com](https://johangarcia.com).

## Stack

- **Framework:** Astro 5
- **Styling:** Scoped CSS with CSS custom properties
- **Fonts:** Outfit + JetBrains Mono (Google Fonts)
- **Forms:** Formspree
- **Animations:** CSS + IntersectionObserver

## Development

```bash
npm install
npm run dev       # localhost:4321
npm run build     # production build
npm run preview   # preview build
```

## Structure

```
src/
├── layouts/
│   └── Layout.astro      # Base layout with SEO meta, fonts, global styles
└── pages/
    └── index.astro        # Single-page site with all sections
public/
└── media/                 # Images and logos
```
