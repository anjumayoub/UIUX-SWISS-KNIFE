# Watch Design Systems — Token Reference

A watch design system is mostly a **constraint system**. The tokens are short
because the decisions are few — and each one matters more than it would on a
phone.

---

## The constraints that generate every token

| Constraint | Consequence for your system |
|---|---|
| Task length ≈ 2–10 seconds | One idea per screen. No secondary content tier. |
| Screen 1–2 inches | Type scale starts where a phone's ends. |
| Arm raised, in motion | Targets grow; precision gestures die. |
| OLED, battery-bound | Black is free. Large light fills cost power. |
| Glanced, not read | Numbers and icons over sentences. |

---

## watchOS

### Type — SF Compact

| Text style | Size (45 mm) | Weight | Use |
|---|---|---|---|
| Large Title | 34 pt | Regular | A single glanceable number |
| Title 1 | 30 pt | Regular | Screen title |
| Title 2 | 22 pt | Regular | |
| Title 3 | 18 pt | Regular | |
| Headline | 16 pt | **Semibold** | Row title |
| Body | 16 pt | Regular | Default |
| Caption 1 | 14 pt | Regular | Supporting |
| Caption 2 | 13 pt | Regular | Smallest |
| Footnote | 12 pt | Regular | Absolute floor |

SF Compact has **tighter apertures and narrower forms** than SF Pro — it is a
different face, not the same face smaller. Sizes shift by case size (40/41/42 vs
44/45/46/49 mm), so bind to styles, never numbers.

### Colour

| Token | Rule |
|---|---|
| Background | **Pure black** (`#000000`). Not dark grey. It's free power and infinite contrast. |
| Accent / tint | Your one brand colour. Used for actions and state only. |
| Text primary | White |
| Text secondary | White at ~60% opacity |
| Fills | White at 10–20% for card backgrounds |
| Semantic | System red/green/orange only — no custom palettes |

There is effectively **no light mode**. Design one theme, on black.

### Layout & metrics

| Token | Value |
|---|---|
| Side margins | ~8–10 pt (case dependent) |
| Minimum tap target | 44 × 44 pt |
| Preferred row | **Full width**, ~50–60 pt tall |
| Corner radius | Follows the case curve — use system containers |
| Safe area | Follows the display curve — never place targets in corners |

### Component families you must spec

- **List rows** (the default screen)
- **Page-based views** (horizontal swipe between peer screens)
- **Digital Crown interactions** (scroll, pick, adjust) — always pair with haptics
- **Complications** — WidgetKit families: `accessoryCircular`,
  `accessoryCorner`, `accessoryRectangular`, `accessoryInline`
- **Smart Stack widgets** — the modern surface people actually see
- **Notifications** — short look (auto) + **long look** (you design this)
- **Always-On state** — a dimmed, redacted variant of every screen

**The Always-On rule:** if your screen has no designed always-on variant, the
system will make an ugly one for you.

---

## Wear OS

### Type — Wear Material 3 typescale

| Role | Size | Use |
|---|---|---|
| Display Large | 40 sp | Single hero number |
| Display Medium | 30 sp | |
| Display Small | 24 sp | |
| Title Large | 20 sp | Screen title |
| Title Medium | 16 sp | Card title |
| Title Small | 14 sp | |
| Body Large | 16 sp | Default reading |
| Body Medium | 14 sp | |
| Body Small | 12 sp | Supporting |
| Label Large | 16 sp | Button label |
| Label Medium | 14 sp | |
| Label Small | 12 sp | Floor |

### Colour — on-black scheme

Wear uses the M3 role vocabulary with a dark-only mapping:

| Role | Value |
|---|---|
| `background` | `#000000` |
| `surface` / `surfaceContainer` | Very dark neutral, 8–15% lightness |
| `primary` | Brand tone 80 (light, for legibility on black) |
| `onPrimary` | Brand tone 20 |
| `primaryContainer` | Brand tone 30 |
| `outline` | Neutral-variant 60 |

### Layout & metrics

| Token | Value |
|---|---|
| Screen widths | ~192 dp (small) / ~227 dp (large) — design for both |
| Side margins | **Percentage-based** (~5.2% side, ~10% top/bottom on round) |
| Minimum touch target | **48 × 48 dp** (40 dp tolerated where space forces it) |
| Shape | `full` on buttons and chips — round hardware, round components |
| List | `ScalingLazyColumn` — items scale down at the edges |

**Round-first math:** a rectangle inscribed in a circle loses the corners. Design
the content column at roughly 70% of screen width and let the system scale the
first and last list items. Always add top/bottom spacers so item one and item
last can scroll clear of the curve.

### Component families you must spec

- **Tiles** — swipeable glanceable panels (your most-seen surface)
- **Complications** — on the watch face
- **Ongoing activity** — persistent notification during a live session
- **Watch faces** — a separate product; treat as its own system
- **Rotary input** (bezel / crown) — must work without touch

---

## Shared spec — build both from one sheet

| Decision | watchOS | Wear OS |
|---|---|---|
| Background | Pure black | Pure black |
| Target minimum | 44 pt | 48 dp |
| Glanceable surface | Complication + Smart Stack | Complication + Tile |
| Scroll input | Digital Crown | Rotary bezel / crown |
| Type family | SF Compact | Roboto (or brand, cautiously) |
| List behaviour | Straight list | Edge-scaling list |
| Theme count | 1 (dark) | 1 (dark) |
| Phone relationship | Companion app defines the full feature set; watch does the 3 things people do while moving |

**The 10-second test:** state the one task the screen exists for in a single
sentence. If it takes two sentences, the screen belongs on the phone.

---

## Sources

- [HIG — Designing for watchOS](https://developer.apple.com/design/human-interface-guidelines/designing-for-watchos)
- [HIG — Complications](https://developer.apple.com/design/human-interface-guidelines/complications)
- [Wear OS design guidelines](https://developer.android.com/design/ui/wear)
- [Wear OS — Screen sizes](https://developer.android.com/design/ui/wear/guides/m2-5/foundations/screen-sizes)
- [Wear OS — Accessibility & touch targets](https://developer.android.com/training/wearables/accessibility)
