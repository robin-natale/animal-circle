---
title: AI-assisted development
description: How this starter is wired for AI coding agents — config files, the design knowledge base, and ready-to-paste prompts.
sidebar:
  order: 4
---

This project is set up to be edited by AI coding agents — Claude in particular
(Claude Code, Claude in this chat, etc.). It ships a small "operating system" of
instructions, a canonical design knowledge base, and portable audit prompts so an
agent — or you — can make changes that stay **on-system** instead of drifting.

## What Claude reads

| File | Purpose |
| --- | --- |
| `AGENTS.md` | The universal brief: architecture tiers, hard rules, verification commands. Claude reads this at the start of a task. |
| `.agents/skills/` | Project-scoped skills available to Claude Code |

## The design knowledge base

Design decisions are centralized so an agent never has to guess:

- **`system/globals/`** — the single source of truth for colors, typography, spacing,
  interaction, imagery, effects, responsiveness, accessibility, and the component/
  pattern catalog. Read these before any UI work.
- **`src/config/site.config.ts`** — bring-your-own-brand input. Brand values are
  translated into design **tokens**, never inlined.
- **`src/registry.json`** — a machine-readable catalog of every component, section,
  and page.

**Architecture (three tiers):** components (`src/components/ui/**`) → sections
(`src/components/sections/**`) → pages (`src/pages/**`). Build pages by composing
sections; build sections from components.

## Hard rules (what "on-system" means)

- **Tokens only.** Colors/spacing/typography come from design tokens — no hardcoded
  hex/rgb, no raw Tailwind palette utilities (`bg-blue-500`). Use semantic tokens
  like `bg-primary`, `text-foreground`, `var(--muted-foreground)`.
- **Dark mode stays working.** Class strategy; never hand-invert colors.
- **Preserve cross-cutting features.** i18n (English default, locale routing ready
  under `src/pages/[locale]/`), Cloudflare Pages deployment, SEO/OG/RSS/sitemap,
  Pagefind search, and the Starlight docs.
- **Content lives in collections.** Blog, services, pages, FAQs, and stack are
  file-based content collections under `src/content/` — see
  [Content Management](/docs/guides/content-management/). Don't hardcode copy that
  belongs in a collection.

## Verify before "done"

Ask the agent to run these and fix anything that fails:

```bash
pnpm build          # static production build
pnpm lint           # eslint + stylelint + type-check + KPIs + i18n
pnpm run check:kpis # design-convention checks (the on-system source of truth)
```

## Prompting

### Starting a task

Point Claude at the system first, then state the goal:

```text
Read AGENTS.md and system/globals/ before editing.
Add a "Logos" section to the homepage that reuses existing components and tokens.
Keep dark mode and i18n intact, then run `pnpm build` and `pnpm lint`.
```

### Self-audit prompts

`system/prompts/` holds portable prompts you can paste into Claude to audit the
project against its conventions. They reference `system/globals/` and the `check:kpis`
script.

| Prompt | Audits |
| --- | --- |
| `system/prompts/tokens.md` | Hardcoded colors / off-token usage |
| `system/prompts/accessibility.md` | WCAG AA: keyboard, focus, alt text, landmarks |
| `system/prompts/responsive.md` | Layout integrity from 375–1920px |
| `system/prompts/darkmode.md` | Dark-mode parity & contrast |
| `system/prompts/performance.md` | Islands, assets, Lighthouse |
| `system/prompts/seo.md` | Metadata, OG, sitemap, structured data |

Example:

```text
Run the audit in system/prompts/accessibility.md against src/pages/contact.astro
and list concrete fixes with file:line references.
```

### Project skills

Project skills live in `.agents/skills/`. Add or update a skill there when Claude
needs project-specific guidance beyond `AGENTS.md`.
