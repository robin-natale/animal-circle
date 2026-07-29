# Animal Circle

Animal communication, energetic support, and welfare advocacy for animals in
sanctuaries, rescues, and animal centres. A static marketing site + blog built
with **Astro 7**, deployed on **Cloudflare Pages**. Content is managed with
Git and Markdown — no CMS, no database.

Built on the [Astro Cloudflare Starter](https://github.com/milzamsz/astro-cloudflare-starter) theme.

## Features

- English-first with a multilanguage-ready i18n engine (prefix-based routing)
- Marketing pages, blog, and Starlight-powered docs with full-text search
- Light/dark theming with a monochrome OKLCH design system
- SEO defaults: canonical, hreflang, JSON-LD, Open Graph, sitemap, RSS, dynamic `llms.txt`
- Static output — fast on the Cloudflare CDN, cheap to host

## Quick Start

```bash
git clone <this-repo-url>
cd animal-circle
pnpm install
pnpm dev
```

Open **http://localhost:4321**.

## Configuration

- `src/config/site.config.ts` — site name, description, author, social links, OG image, branding (logo, colors, favicon). Single source of truth (canonical/OG/sitemap/`llms.txt`; `astro.config.ts` reads `url`).
- `src/config/nav.config.ts` — header/footer navigation and social URLs.
- `wrangler.jsonc` — Cloudflare Pages project name.
- `.env.example` → `.env`; set `SITE_URL`.
- Content in `src/content/` (blog, services, pages, docs, settings).

## Documentation

| Document | Purpose |
|----------|---------|
| [SETUP.md](SETUP.md) | Setup and Cloudflare Pages deployment |
| [SECURITY.md](SECURITY.md) | Reporting vulnerabilities |
| [CHANGELOG.md](CHANGELOG.md) | Release notes |
| `/docs` (Starlight) | In-app guides: getting started, content, i18n, deployment |

## Scripts

```bash
pnpm dev        # start dev server
pnpm build      # production build to dist/
pnpm preview    # preview the production build
pnpm lint       # eslint + stylelint + type-check + validations
pnpm test       # unit tests (vitest)
pnpm test:e2e   # end-to-end tests (playwright)
```

## Content model

All content lives in `src/content` as Markdown/JSON and is type-checked via content
collection schemas. Each entry uses `<slug>.md` with a `locale` frontmatter field
(English by default). To add a language, see `docs/guides/internationalization`.

## Deployment

Connect the repo to Cloudflare Pages (build command `pnpm build`, output `dist`), or
deploy manually with `npx wrangler pages deploy dist`. See [SETUP.md](SETUP.md).

## License

[MIT](LICENSE)
