# iOS Design System — Token Reference

The iOS "token sheet". Apple already ships you a design system; your job is to
name your brand inside it, not to replace it. Everything below is a **name you
design with** — the OS decides the number.

---

## 1. Type — Dynamic Type text styles

Sizes shown at the **Large** setting (the default). Users can go down to xSmall
and up to AX5; your layout must survive both.

| Text style | Size | Line height | Weight | Use it for |
|---|---|---|---|---|
| Large Title | 34 pt | 41 pt | Regular | Scroll-to-top screen title |
| Title 1 | 28 pt | 34 pt | Regular | Section screen title |
| Title 2 | 22 pt | 28 pt | Regular | Prominent card heading |
| Title 3 | 20 pt | 25 pt | Regular | Sub-section heading |
| Headline | 17 pt | 22 pt | **Semibold** | Row title, emphasised body |
| Body | 17 pt | 22 pt | Regular | Default reading text |
| Callout | 16 pt | 21 pt | Regular | Slightly de-emphasised body |
| Subheadline | 15 pt | 20 pt | Regular | Secondary row text |
| Footnote | 13 pt | 18 pt | Regular | Timestamps, attribution |
| Caption 1 | 12 pt | 16 pt | Regular | Image captions, tags |
| Caption 2 | 11 pt | 13 pt | Regular | Smallest permissible label |

**Rules**

- Never hard-code a point size. Bind to the style; the system scales it.
- Minimum body text is Caption 2. Anything smaller fails accessibility.
- Test at AX3 minimum. Rows must reflow to vertical stacks, not truncate.
- Font: **SF Pro** (Text below 20 pt, Display at 20 pt and above — the OS
  switches optical size automatically). SF Pro Rounded for playful brands.

---

## 2. Color — semantic system colors

These are your **semantic tier**. They already have light/dark, increased-contrast
and elevated variants baked in.

### Text

| Token | Role |
|---|---|
| `label` | Primary text |
| `secondaryLabel` | Supporting text |
| `tertiaryLabel` | Placeholder, disabled-ish text |
| `quaternaryLabel` | Barely-there text — use sparingly |
| `placeholderText` | Text-field placeholder |

### Backgrounds — two families, pick one per screen and stay in it

| Standard family | Grouped family | Use |
|---|---|---|
| `systemBackground` | `systemGroupedBackground` | Screen canvas |
| `secondarySystemBackground` | `secondarySystemGroupedBackground` | Cards / grouped list rows |
| `tertiarySystemBackground` | `tertiarySystemGroupedBackground` | Content inside a card |

Use the **grouped** family on any screen built from inset grouped lists
(Settings-style). Use the **standard** family everywhere else. Mixing them is the
single most common iOS colour mistake.

### Fills, separators, tint

| Token | Role |
|---|---|
| `systemFill` → `quaternarySystemFill` | Layered fills for small controls, chips, thumbnails |
| `separator` | Hairline that lets background through |
| `opaqueSeparator` | Solid hairline |
| `tintColor` / `accentColor` | **Your brand.** Almost the only colour you supply |

### Dark mode

- Dark mode has **two surface levels**: base and *elevated*. Sheets, popovers and
  anything presented over content use the elevated variants automatically —
  which is why you must not hard-code dark greys.
- Elevation in dark mode is expressed as *lighter surface*, not shadow.

### Materials (blur)

`.ultraThinMaterial` → `.thinMaterial` → `.regularMaterial` → `.thickMaterial` →
`.ultraThickMaterial`. Use with **vibrancy** label styles so text stays legible.
Materials are for chrome floating over content (nav bars, tab bars, sheets), not
for content itself.

---

## 3. Layout — spacing and metrics

| Token | Value | Note |
|---|---|---|
| Standard content margin | 16 pt (compact) / 20 pt (regular) | The `layoutMargins` default |
| Grouped list inset | 20 pt side | Inset grouped table style |
| Minimum tap target | 44 × 44 pt | Non-negotiable |
| Spacing base | 8 pt | 4 pt allowed for tight optical fixes |
| Corner radius — card | 10–16 pt | Continuous curve, not circular |
| Corner radius — sheet | 10 pt top (system) | Don't redraw it |
| Nav bar height | 44 pt (+ large-title 52 pt) | Plus safe area |
| Tab bar height | 49 pt | Plus home-indicator inset |
| Toolbar height | 44 pt | |

**Safe areas** are tokens too: top inset varies by device (Dynamic Island vs
notch vs flat), bottom home-indicator inset is 34 pt on gesture devices. Never
place a tap target under the indicator.

---

## 4. Icons — SF Symbols configuration

SF Symbols are not images; they are **fonts with a configuration**, so treat the
configuration as tokens.

| Axis | Values | Default |
|---|---|---|
| Weight | Ultralight → Black | Matches adjacent text weight |
| Scale | Small / Medium / Large | Medium |
| Rendering | Monochrome / Hierarchical / Palette / Multicolor | Monochrome |
| Variable value | 0.0–1.0 | For progress-style symbols |

**Rule:** an icon's weight should match the weight of the text next to it.
Pick a rendering mode per surface and keep it — mixing hierarchical and
multicolor in one toolbar reads as a bug.

---

## 5. Motion

| Token | Value | Use |
|---|---|---|
| Default spring | response 0.5, damping 0.825 | Most transitions |
| Snappy spring | response 0.3, damping 0.85 | Buttons, toggles |
| Bouncy spring | response 0.5, damping 0.65 | Playful confirmation |
| Sheet presentation | System | Never re-implement |

iOS motion is **interruptible and physical**. If your prototype cannot be grabbed
mid-animation and reversed, it is not iOS motion. Honour
`Reduce Motion` by swapping slides for cross-fades.

---

## 6. What you actually supply

Out of everything above, a real iOS design system usually adds only:

1. **Tint / accent colour** (+ its dark-mode variant)
2. **A custom display face** for marketing surfaces (body stays SF)
3. **Brand illustration and icon style** where SF Symbols don't reach
4. **Component compositions** — your card, your row, your empty state
5. **Content voice** — the strings

Everything else you inherit. That is the point.

---

## Sources

- [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines)
- [HIG — Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- [HIG — Color](https://developer.apple.com/design/human-interface-guidelines/color)
- [HIG — Materials](https://developer.apple.com/design/human-interface-guidelines/materials)
- [Apple Design Resources (Figma libraries)](https://developer.apple.com/design/resources/)
- [SF Symbols](https://developer.apple.com/sf-symbols/)
