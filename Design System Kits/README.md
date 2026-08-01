# Design System Kits

Starter kits for the **UIUX Swiss Knife** course. Every file here is a working
artifact, not a sample — build your own systems by editing these rather than
starting from an empty Figma page.

## What's in here

| File | What it is | Use it in |
|---|---|---|
| `saas-tokens.css` | The full three-tier token set as CSS custom properties: primitives, semantic roles, component tokens, light + dark. | Module d1 (SaaS design system) |
| `saas-tokens.json` | The same tokens in **DTCG** format (the W3C Design Tokens spec). | Style Dictionary, Tokens Studio, any token pipeline |
| `saas-tokens.figma.json` | Flat `path: value` map grouped into Figma collections. | Figma Variables Import plugins |
| `saas-tokens.tailwind.css` | Tailwind v4 `@theme` block that aliases every token. | Handoff to a Tailwind codebase |
| `marketing-web-tokens.css` | Fluid type, section rhythm, containers, art-direction slots. Loads on top of `saas-tokens.css`. | Module d2 (website design system) |
| `ios-tokens-reference.md` | Dynamic Type, semantic colors, materials, SF Symbols config — the iOS equivalent of a token sheet. | Module d3 |
| `android-m3-tokens-reference.md` | M3 `ref` → `sys` → `comp` architecture, colour roles, typescale, shape, elevation. | Module d4 |
| `watch-tokens-reference.md` | watchOS + Wear OS token sheets and the constraints that generate them. | Module d5 |
| `component-spec-template.md` | The blank spec every component in your system gets filled in against. | Modules d1–d5 |
| `audit-checklist.md` | The pass/fail list to run your system against before you call it done. | Module d1 practice |

## How the colour ramps were built

Every ramp is generated to hit the **same contrast ratio against white at each
step**, across all hues. That is why `brand-700`, `danger-700` and `success-700`
all sit at roughly 7.2:1 — you can swap a hue without re-auditing contrast.

| Step | Contrast vs white | Safe for |
|---|---|---|
| 25–100 | 1.03–1.18 | Backgrounds, subtle tints |
| 200–300 | 1.42–1.95 | Borders on light, fills on dark |
| 400 | 2.75 | Large graphics, dark-mode text |
| 500 | 3.85 | Non-text UI (icons, borders) — passes 3:1 |
| 600 | 5.20 | Buttons, links, body text — passes AA 4.5:1 |
| 700 | 7.20 | Text — passes AAA 7:1 |
| 800–1000 | 9.6–17.6 | Headings, dark surfaces |

Verified pairs (light / dark):

| Pair | Light | Dark |
|---|---|---|
| `text-primary` on `bg-surface` | 12.32:1 | 14.13:1 |
| `text-secondary` on `bg-surface` | 7.14:1 | 7.85:1 |
| `text-tertiary` on `bg-surface` | 5.25:1 | 5.55:1 |
| `action-primary-fg` on primary button | 5.21:1 | 6.36:1 |
| `text-brand` on `bg-surface` | 7.20:1 | 7.83:1 |
| `text-danger` on `bg-surface` | 7.24:1 | 7.86:1 |
| Focus ring on `bg-canvas` | 4.81:1 | 6.36:1 |

All pass WCAG 2.1 AA; most pass AAA.

## The one rule

**Components read semantic tokens only.** A button never references
`--c-brand-600`; it references `--action-primary-bg`. That single discipline is
what makes dark mode, rebranding and theming a config change instead of a
redesign.

## Getting these into Figma

1. Open your design-system file → **Variables** panel.
2. Create three collections: `Primitives`, `Semantic` (modes: Light, Dark), `Scale`.
3. Install a variables-import plugin and feed it `saas-tokens.figma.json`.
4. In `Semantic`, set each variable's value to a **variable alias** pointing at
   the matching `Primitives` entry — not a raw hex. This is the step people skip,
   and it is the step that makes the system work.
5. Bind component properties to the `Semantic` collection only.

## Getting these into code

```html
<link rel="stylesheet" href="saas-tokens.css">
<!-- marketing pages only -->
<link rel="stylesheet" href="marketing-web-tokens.css">
```

```html
<!-- Theme switching -->
<html data-theme="dark">
```

With no `data-theme` attribute the kit follows `prefers-color-scheme`.
Setting `data-theme="light"` or `"dark"` overrides the OS.
