# Component Spec Template

Copy this for every component you add to a system. A component is not "done"
until every heading below has an answer. Headings you leave blank are the ones a
developer will guess at — and guess differently from you.

---

# Component: `<Name>`

**Status:** Draft / Review / Stable / Deprecated
**Version:** 1.0.0
**Owner:** <name>
**Last updated:** <date>

---

## 1. Purpose

One sentence: what problem this solves for the user.

**Use when:** …
**Do not use when:** … (name the component to use instead)

---

## 2. Anatomy

Numbered diagram + a table of parts.

| # | Part | Required | Notes |
|---|---|---|---|
| 1 | Container | Yes | |
| 2 | Leading icon | No | |
| 3 | Label | Yes | |
| 4 | Trailing element | No | |

---

## 3. Properties (this is the developer's API)

| Property | Type | Values | Default | Notes |
|---|---|---|---|---|
| `variant` | enum | primary / secondary / tertiary / destructive | primary | |
| `size` | enum | sm / md / lg | md | |
| `disabled` | boolean | true / false | false | |
| `loading` | boolean | true / false | false | |
| `iconLeading` | slot | — | none | |
| `fullWidth` | boolean | true / false | false | |

Name properties the way the code will. `isDisabled` in Figma and `disabled` in
React is a papercut that repeats a thousand times.

---

## 4. States — every one, every variant

| State | Trigger | Token changes |
|---|---|---|
| Default | — | `--action-primary-bg` |
| Hover | pointer over | `--action-primary-bg-hover` |
| Focus-visible | keyboard | 2 px `--border-focus`, 2 px offset |
| Active / pressed | pointer down | `--action-primary-bg-active` |
| Loading | async | spinner replaces label, width locked |
| Disabled | prop | `--bg-disabled` + `--text-disabled`, no pointer events |
| Error | validation | `--border-danger` + message below |
| Selected | prop | `--bg-brand-subtle` + `--text-brand` |
| Read-only | prop | no border, `--text-primary` |

**A state you did not draw is a state a developer invented.**

---

## 5. Sizing & spacing

| Size | Height | Padding X | Gap | Font | Icon | Radius |
|---|---|---|---|---|---|---|
| sm | 32 px | 12 px | 6 px | text-sm | 16 px | radius-sm |
| md | 40 px | 16 px | 8 px | text-sm | 20 px | radius-sm |
| lg | 48 px | 20 px | 8 px | text-md | 20 px | radius-sm |

All values reference tokens, never literals.

---

## 6. Behaviour

- What happens on click / tap / enter / space?
- Is it interruptible?
- What happens on double-submit?
- Minimum and maximum content length?
- What happens when content overflows — truncate, wrap, or scroll?

---

## 7. Responsive

| Breakpoint | Change |
|---|---|
| < 768 px | Full width, size lg for thumb reach |
| ≥ 768 px | Auto width, size md |

---

## 8. Accessibility

| Requirement | Spec |
|---|---|
| Role | `button` (native `<button>` preferred) |
| Accessible name | Visible label; icon-only requires `aria-label` |
| Keyboard | `Tab` to reach, `Enter`/`Space` to activate |
| Focus indicator | 2 px ring, 2 px offset, ≥ 3:1 against adjacent colours |
| Contrast | Label ≥ 4.5:1; container edge ≥ 3:1 |
| Target size | ≥ 44 × 44 px effective (padding counts) |
| Motion | Respects `prefers-reduced-motion` |
| Screen reader | Announce loading and disabled state changes |

---

## 9. Motion

| Property | Duration | Easing |
|---|---|---|
| Background colour | `--duration-fast` | `--ease-standard` |
| Focus ring | `--duration-instant` | `--ease-standard` |
| Loading spinner | 800 ms loop | linear |

---

## 10. Content guidelines

- Label: sentence case, verb-first, 1–3 words ("Save changes", not "Submit").
- Never use "Click here" or "OK" for a destructive action.
- Loading label: keep the verb ("Saving…").

---

## 11. Do / Don't

| Do | Don't |
|---|---|
| One primary button per view | Two primaries competing |
| Put the destructive action second | Make destructive the default focus |
| Keep width stable during loading | Let the button resize mid-action |

---

## 12. Related

- Depends on: `Icon`, `Spinner`
- Alternatives: `Link`, `IconButton`
- Composed into: `Modal footer`, `Form actions`, `Toolbar`

---

## 13. Changelog

| Version | Date | Change |
|---|---|---|
| 1.0.0 | | Initial release |
