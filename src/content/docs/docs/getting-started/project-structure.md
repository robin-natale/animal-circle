---
title: Project Structure
description: How the project is organised and where to find key files.
sidebar:
  order: 3
---

```
.
├── public/
│   ├── _headers             # Cloudflare Pages headers (security/CSP)
│   ├── logos/                # Light/dark logo SVGs
│   └── favicon.svg
├── src/
│   ├── components/          # Reusable Astro components (Hero, CTA, FAQ…)
│   ├── content/             # Content collections (blog, docs, pages, services)
│   ├── i18n/                # Internationalisation utilities (routes, switcher, UI)
│   ├── layouts/             # Base layout with SEO, analytics, navigation
│   ├── lib/                 # Shared libraries (analytics, images, SEO, site config)
│   ├── pages/               # Astro pages with locale routing (+ llms.txt, robots.txt, rss)
│   ├── styles/              # Global CSS and Tailwind layers
│   └── content.config.ts    # Content collection schemas
├── astro.config.ts          # Astro + Starlight + integrations config
├── wrangler.jsonc           # Cloudflare Pages config
└── package.json
```

## Key Patterns

- **Locale routing**: default-locale routes live at the root; add `src/pages/[locale]/` routes when introducing more languages.
- **Content collections**: Markdown files in `src/content/` with a `locale` frontmatter field (English by default).
- **Content editing**: pure Git/Markdown — edit files and open a pull request.
