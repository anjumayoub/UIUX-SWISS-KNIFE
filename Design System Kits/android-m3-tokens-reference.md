# Android / Material 3 — Token Reference

Material 3 is the most explicitly tokenised design system in production. Learn its
three-letter prefixes and you can read any M3 spec, Figma kit or Compose theme.

---

## 1. Token architecture — `ref` → `sys` → `comp`

| Tier | Prefix | Holds | Example |
|---|---|---|---|
| Reference | `md.ref.palette.*` | Raw values. 6 tonal palettes × 13 tones. | `md.ref.palette.primary40` |
| System | `md.sys.color.*`, `md.sys.typescale.*`, `md.sys.shape.*`, `md.sys.elevation.*`, `md.sys.motion.*` | Roles and decisions. **This is the tier you design against.** | `md.sys.color.primary` |
| Component | (no prefix) | Per-component overrides. | `filled-button.container-color` |

Same one-way rule as the web kit: **component → system → reference**, never
backwards, never skipping.

---

## 2. Tonal palettes

A single **seed colour** generates six palettes: Primary, Secondary, Tertiary,
Error, Neutral, Neutral Variant. Each has 13 tones: `0, 10, 20, 30, 40, 50, 60,
70, 80, 90, 95, 99, 100` where 0 = black and 100 = white.

**Tone is lightness, not brightness.** Tone 40 of any hue has roughly the same
perceived lightness as tone 40 of any other — which is how M3 guarantees contrast
algorithmically. (The web kit in this folder uses the same idea, expressed as
target contrast ratios instead of tones.)

---

## 3. Colour roles — the mapping table

Memorise the pattern, not the individual rows: **container = the surface, on-X =
what sits on it, and dark mode flips high tone for low tone.**

| Role | Light tone | Dark tone | Use |
|---|---|---|---|
| `primary` | P40 | P80 | Filled buttons, FAB, active states |
| `on-primary` | P100 | P20 | Text/icons on `primary` |
| `primary-container` | P90 | P30 | Lower-emphasis brand surfaces |
| `on-primary-container` | P10 | P90 | Text/icons on `primary-container` |
| `secondary` | S40 | S80 | Less-prominent accents, filter chips |
| `on-secondary` | S100 | S20 | |
| `secondary-container` | S90 | S30 | Selected chip, nav indicator pill |
| `on-secondary-container` | S10 | S90 | |
| `tertiary` | T40 | T80 | Contrasting accent, balance |
| `tertiary-container` | T90 | T30 | |
| `error` | E40 | E80 | Errors, destructive actions |
| `error-container` | E90 | E30 | Error banners |
| `surface` | N98 | N6 | Default background |
| `on-surface` | N10 | N90 | Primary text |
| `surface-variant` | NV90 | NV30 | Differentiated fill |
| `on-surface-variant` | NV30 | NV80 | Secondary text, icons |
| `surface-container-lowest` | N100 | N4 | Elevation level 0 |
| `surface-container-low` | N96 | N10 | Elevation level 1 |
| `surface-container` | N94 | N12 | Elevation level 2 (cards, sheets) |
| `surface-container-high` | N92 | N17 | Elevation level 3 (menus, dialogs) |
| `surface-container-highest` | N90 | N22 | Elevation level 4/5 |
| `outline` | NV50 | NV60 | Borders that must be visible |
| `outline-variant` | NV80 | NV30 | Dividers, decorative rules |
| `inverse-surface` | N20 | N90 | Snackbars |
| `on-inverse-surface` | N95 | N20 | |
| `inverse-primary` | P80 | P40 | Action text inside a snackbar |
| `scrim` | N0 | N0 | Modal backdrop (at ~32–60% alpha) |

**The M3 elevation lesson:** elevation is expressed as a **surface tone**, not a
shadow. A dialog is not "the card plus a bigger shadow"; it is
`surface-container-high`. Shadows are optional garnish.

---

## 4. Type scale — `md.sys.typescale.*`

| Role | Size | Line height | Weight | Tracking | Use |
|---|---|---|---|---|---|
| Display Large | 57 sp | 64 sp | 400 | -0.25 | Hero numerals, splash |
| Display Medium | 45 sp | 52 sp | 400 | 0 | |
| Display Small | 36 sp | 44 sp | 400 | 0 | |
| Headline Large | 32 sp | 40 sp | 400 | 0 | Screen title |
| Headline Medium | 28 sp | 36 sp | 400 | 0 | |
| Headline Small | 24 sp | 32 sp | 400 | 0 | |
| Title Large | 22 sp | 28 sp | 400 | 0 | Top app bar |
| Title Medium | 16 sp | 24 sp | **500** | 0.15 | List item title |
| Title Small | 14 sp | 20 sp | **500** | 0.1 | |
| Body Large | 16 sp | 24 sp | 400 | 0.5 | Reading text |
| Body Medium | 14 sp | 20 sp | 400 | 0.25 | Default body |
| Body Small | 12 sp | 16 sp | 400 | 0.4 | Supporting text |
| Label Large | 14 sp | 20 sp | **500** | 0.1 | **Button labels** |
| Label Medium | 12 sp | 16 sp | **500** | 0.5 | Nav bar labels |
| Label Small | 11 sp | 16 sp | **500** | 0.5 | Smallest label |

**sp, not dp** — sp scales with the user's font-size setting. Never set text in dp.

---

## 5. Shape scale — `md.sys.shape.corner.*`

| Token | Radius | Applied to |
|---|---|---|
| `none` | 0 dp | Full-bleed images |
| `extra-small` | 4 dp | Menus, snackbars, text-field top corners |
| `small` | 8 dp | Chips, small cards |
| `medium` | 12 dp | Cards |
| `large` | 16 dp | FAB, dialogs, navigation drawer |
| `extra-large` | 28 dp | Bottom sheet top corners, extended FAB, search bar |
| `full` | 50% | Buttons, chips (M3 default), badges, switch thumb |

Shape carries brand personality: swap `full` for `small` on buttons and the whole
product reads more serious. Change it once in the theme, not per component.

---

## 6. Spacing, density and targets

| Token | Value |
|---|---|
| Base grid | 4 dp (blocks land on 8 dp) |
| Screen margin — compact | 16 dp |
| Screen margin — medium/expanded | 24 dp |
| Gutter | 16 dp compact / 24 dp medium+ |
| Minimum touch target | **48 × 48 dp** |
| List item height — one line | 56 dp |
| List item height — two line | 72 dp |
| Top app bar (small) | 64 dp |
| Navigation bar | 80 dp |
| FAB | 56 dp (small 40, large 96) |

## Window size classes

| Class | Width | Response |
|---|---|---|
| Compact | < 600 dp | Navigation bar, single pane |
| Medium | 600–839 dp | Navigation rail, optional two panes |
| Expanded | ≥ 840 dp | Rail or drawer, canonical layouts |

Canonical layouts: **list-detail**, **supporting pane**, **feed**.

---

## 7. Motion — `md.sys.motion.*`

| Easing token | Curve | Use |
|---|---|---|
| `emphasized` | `cubic-bezier(0.2, 0, 0, 1)` | Default for visible transitions |
| `emphasized-decelerate` | `cubic-bezier(0.05, 0.7, 0.1, 1)` | Elements entering |
| `emphasized-accelerate` | `cubic-bezier(0.3, 0, 0.8, 0.15)` | Elements exiting |
| `standard` | `cubic-bezier(0.2, 0, 0, 1)` | Small utility motion |

| Duration token | Value | Use |
|---|---|---|
| `short2` | 100 ms | Selection, icon toggle |
| `short4` | 200 ms | Small component transitions |
| `medium2` | 300 ms | Component entering the screen |
| `medium4` | 400 ms | **Container transform** |
| `long2` | 500 ms | Large full-screen transitions |

Signature transitions: **container transform** (a card grows into the detail
screen), **shared axis** (X for lateral, Y for hierarchy, Z for depth),
**fade through** (unrelated content).

---

## 8. Dynamic colour (Material You)

The user's wallpaper seeds the palettes. Consequences you must design for:

- Your brand colour may be **completely replaced** on the user's device.
- So brand identity must survive in *layout, type, shape and iconography*.
- Always design a **baseline theme** (your seed) plus verify the UI in two or
  three wildly different dynamic schemes.
- Opt out per surface if brand fidelity is contractual — but justify it.

---

## 9. Practice references

The Mobbin connector used by this course serves iOS and Web only. For Android,
browse mobbin.com directly — for example
[Grab (iOS + Android)](https://mobbin.com/apps/grab-android-6bde1579-1164-4e3f-ac66-cece8b2afd2e/146e61f6-1624-42aa-882f-b36a2d2d8645/screens),
which is a good cross-platform teardown because the same product ships both.

Drop your own screenshots into the course `Images/` folder and register them in
the course file's `MEDIA` manifest to make them appear as practice cards.

---

## Sources

- [Material 3 — Design tokens](https://m3.material.io/foundations/design-tokens)
- [Material 3 — How the colour system works](https://m3.material.io/styles/color/system/how-the-system-works)
- [Material 3 — Typography](https://m3.material.io/styles/typography/type-scale-tokens)
- [Material 3 — Shape](https://m3.material.io/styles/shape/overview)
- [Material Theme Builder](https://material-foundation.github.io/material-theme-builder/)
- [Material 3 in Compose](https://developer.android.com/develop/ui/compose/designsystems/material3)
