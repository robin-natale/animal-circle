# Colors

Single source of truth for color. Tokens are defined in
`src/styles/tokens/colors.css` and exposed to Tailwind via the `@theme` block in
`src/styles/global.css`. **Never hardcode colors** (no `#hex`, no `bg-blue-500`).
Always use a semantic token.

## System

- **Model:** OKLCH (`oklch(L C H)`), perceptually uniform.
- **Palette:** "Woodland at Dawn" — warm, muted, nature-toned. Light mode is
  cream + deep pine with olive/copper accents; dark mode is dark pine surfaces
  with a copper "dawn glow" primary. Chroma is kept low (≤0.09) everywhere so
  it stays calm rather than saturated.
- **Dark mode:** class strategy (`.dark` on `<html>`). Every semantic token has a
  light and dark value; components reference the token, never a mode-specific color.

## Palette reference

| Name | Hex | Role |
| --- | --- | --- |
| Cream | `#F8F5EE` | Light background |
| Deep pine | `#274137` | Light foreground / primary (light mode) |
| Olive | `#6B7C57` | Secondary, ring |
| Bark brown | `#6D5545` | Muted/accent foreground |
| Muted copper | `#B6815D` | Accent, primary (dark mode) |
| Dark bg | `#18211D` | Dark background |
| Dark surface | `#25302A` | Dark card/popover |
| Dark text | `#F4F1EA` | Dark foreground |

## Semantic tokens

| Token | Use |
| --- | --- |
| `--background` / `--foreground` | page surface / primary text |
| `--card` / `--card-foreground` | raised surfaces, panels |
| `--popover` / `--popover-foreground` | overlays, menus |
| `--primary` / `--primary-foreground` | primary actions, emphasis (near-black ↔ near-white) |
| `--secondary` / `--secondary-foreground` | secondary surfaces/buttons |
| `--accent` / `--accent-foreground` | subtle highlights |
| `--muted` / `--muted-foreground` | muted surfaces / secondary text |
| `--border` | hairlines, dividers, card borders |
| `--ring` | focus ring |
| `--surface-invert` / `--surface-invert-foreground` / `--surface-invert-border` | inverted band (e.g. final CTA) that flips tone in each mode |

## Functional status

`--destructive`, `--success`, `--warning`, `--info` (+ `-foreground`). Use **only**
for genuine status meaning (errors, validation, score gauges) — never as decoration.
They're kept independent of the brand palette so status meaning is never confused
with a themed color.

## Usage

```css
/* in a component <style> */
color: var(--foreground);
background: var(--card);
border: 1px solid var(--border);
```

```astro
<!-- Tailwind utilities map to the same tokens -->
<div class="bg-card text-foreground border border-border">…</div>
<!-- arbitrary value when no utility exists -->
<span class="text-[color:var(--muted-foreground)]">…</span>
```

## Rules

- No raw hex/rgb/hsl in components. Hex is allowed only in token files,
  `site.config.ts` (brand source), and OG image generation.
- Don't invert colors manually for dark mode — swap is automatic via tokens.
- `check:kpis` flags hardcoded Tailwind palette utilities as errors.
