# Design System Audit Checklist

Run this against your system before you call it v1. Score honestly — anything
marked ✗ is a ticket, not an opinion.

---

## 1. Token hygiene

- [ ] Every colour in every component resolves to a **semantic** token, not a primitive and not a hex.
- [ ] Semantic tokens point at primitives — never at other semantic tokens (no alias chains).
- [ ] Token names describe **role**, not appearance (`text-secondary`, not `gray-text`).
- [ ] Dark mode is a **mode on the semantic collection**, not a duplicate component set.
- [ ] Spacing values all come from the scale. Search your file for `13`, `15`, `18`, `22` — any hit is a violation.
- [ ] Radius, shadow and z-index are tokenised, not typed per component.
- [ ] Type styles are bound; no detached text layers with manual sizes.
- [ ] There is exactly **one** place to change the brand colour.

## 2. Colour & contrast

- [ ] Body text ≥ 4.5:1 on every surface it appears on — light **and** dark.
- [ ] Large text (≥ 24 px, or 19 px bold) ≥ 3:1.
- [ ] Icons, borders and focus rings ≥ 3:1 against adjacent colour.
- [ ] Disabled text is visibly disabled but still readable enough to identify.
- [ ] No information conveyed by colour alone — every status has an icon or label.
- [ ] Data-viz palette is distinguishable in greyscale **and** for deuteranopia.
- [ ] Dark mode is not just inverted — surfaces get lighter with elevation, saturated colours are toned down.

## 3. Components

- [ ] Every component has all nine states drawn: default, hover, focus-visible, active, loading, disabled, error, selected, read-only (where applicable).
- [ ] Focus-visible exists on **everything** interactive, including custom controls.
- [ ] Property names match what engineering will call them.
- [ ] Variants use Figma variant properties, not separate detached copies.
- [ ] Auto-layout everywhere; nothing breaks when the label doubles in length.
- [ ] Every component survives: empty content, one character, and 200 characters.
- [ ] Icon-only controls have a tooltip and an accessible name.
- [ ] Nothing in the library is a one-off used exactly once.

## 4. Patterns & templates

- [ ] All five screen states exist for every data surface: empty, loading, partial, error, ideal.
- [ ] Empty states distinguish first-run vs cleared-out vs no-results.
- [ ] Table spec covers: sort, filter, select, bulk action, pagination, column resize, sticky header, row density.
- [ ] Modal vs drawer vs inline is a documented decision, not a per-designer preference.
- [ ] Toast, inline message and banner each have a written "use when".
- [ ] Page templates exist for: list, detail, settings, dashboard, wizard, auth.

## 5. Responsive & platform

- [ ] Every template is drawn at your smallest and largest breakpoints.
- [ ] Touch targets ≥ 44 px (web/iOS) or 48 dp (Android) at every breakpoint.
- [ ] Nothing depends on hover alone.
- [ ] Text reflows at 200% zoom without horizontal scrolling.
- [ ] Layouts survive the longest realistic translated string (+30% German rule).

## 6. Documentation

- [ ] Every component has a filled `component-spec-template.md`.
- [ ] Each has "use when" **and** "don't use when".
- [ ] Do/don't examples are visual, not just prose.
- [ ] Getting-started page tells a new designer what to do in their first hour.
- [ ] Contribution process is written down: how to propose, review, ship.
- [ ] Versioning and deprecation policy exists.
- [ ] Changelog is current.

## 7. Handoff

- [ ] Tokens export to a format engineering consumes (DTCG JSON, CSS vars, Tailwind theme).
- [ ] Figma component names match code component names.
- [ ] Spacing in the spec is stated in the unit engineering uses.
- [ ] Interaction and motion specs include duration and easing tokens.
- [ ] Edge cases are documented in the spec, not discovered in QA.
- [ ] A developer can build the component **without asking you a question**. This is the real test.

---

## Scoring

| Score | Meaning |
|---|---|
| 90–100% | Ship it. Publish the library. |
| 70–89% | Usable internally; fix gaps before wider rollout. |
| 50–69% | It's a UI kit, not a system yet. |
| < 50% | Start with tokens and states — those two fix most of the list. |
