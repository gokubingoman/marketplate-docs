# Typography Foundations

> Type scale, font roles, and responsive sizing for readable, premium Marketplate interfaces.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Typography carries **clarity and trust**. Readable type hierarchy helps customers scan menus, review allergen information, and confirm orders without strain. Creators manage complex dashboards — typography must organize information calmly.

These foundations implement [design principles](../principles.md): calm interfaces, premium feel, accessibility first.

---

## Font Roles

Marketplate uses three typographic roles. Each has a distinct job.

| Role | Job | Characteristics |
|------|-----|-----------------|
| **Display** | Marketing headlines, hero moments, creator name on storefront | Expressive but restrained; larger sizes; tighter tracking at large sizes |
| **Body** | Paragraphs, descriptions, menu item details, reviews | Optimized for reading comfort; generous line height |
| **UI** | Labels, buttons, navigation, form fields, badges | Neutral, compact, highly legible at small sizes |

### Recommended typefaces (foundation)

| Role | Primary | Fallback stack |
|------|---------|----------------|
| Display | **Inter** (weight 600–700) | `system-ui, -apple-system, sans-serif` |
| Body | **Inter** (weight 400–500) | `system-ui, -apple-system, sans-serif` |
| UI | **Inter** (weight 400–600) | `system-ui, -apple-system, sans-serif` |

A single family (Inter) simplifies loading, maintains cohesion, and performs well across platforms. Differentiation comes from **scale and weight**, not family mixing.

TODO(decision): Final typeface selection — evaluate licensed alternatives (e.g., Söhne, GT America) against Inter for premium differentiation before Phase 2 component specs.

---

## Type Scale

Base size: **16px** (`1rem`) on mobile. Scale uses a **1.250 major third** ratio, adjusted for practical UI sizes.

| Token | Size (rem) | Size (px) | Line height | Weight | Role |
|-------|------------|-----------|-------------|--------|------|
| `text-display-xl` | 3.052rem | ~49px | 1.1 | 700 | Marketing hero |
| `text-display-lg` | 2.441rem | ~39px | 1.15 | 700 | Page titles (desktop) |
| `text-display-md` | 1.953rem | ~31px | 1.2 | 600 | Section headers |
| `text-display-sm` | 1.563rem | ~25px | 1.25 | 600 | Card titles, creator name |
| `text-body-lg` | 1.125rem | 18px | 1.6 | 400 | Lead paragraphs, menu descriptions |
| `text-body-md` | 1rem | 16px | 1.6 | 400 | Default body text |
| `text-body-sm` | 0.875rem | 14px | 1.5 | 400 | Secondary content, reviews |
| `text-ui-lg` | 1rem | 16px | 1.4 | 500 | Primary buttons, nav items |
| `text-ui-md` | 0.875rem | 14px | 1.4 | 500 | Labels, secondary buttons |
| `text-ui-sm` | 0.75rem | 12px | 1.4 | 500 | Badges, captions, metadata |
| `text-ui-xs` | 0.6875rem | 11px | 1.3 | 500 | Legal microcopy only — use sparingly |

**Minimum readable size:** 14px (`text-body-sm`, `text-ui-md`) for any essential content. 12px and below for supplementary metadata only.

---

## Responsive Sizing

Typography scales down on smaller viewports to preserve hierarchy without overflow.

| Token | Mobile (< 768px) | Tablet (768–1023px) | Desktop (≥ 1024px) |
|-------|------------------|---------------------|---------------------|
| `text-display-xl` | display-md | display-lg | display-xl |
| `text-display-lg` | display-sm | display-md | display-lg |
| `text-display-md` | body-lg (600 wt) | display-sm | display-md |
| `text-display-sm` | body-lg (600 wt) | display-sm | display-sm |
| Body & UI tokens | No change | No change | No change |

**Rule:** Display sizes adapt; body and UI sizes stay constant for reading consistency.

Implementation: use CSS `clamp()` or breakpoint-specific token mappings in Phase 2.

---

## Hierarchy Patterns

### Storefront (customer-facing)

```
Creator name          → text-display-sm (mobile) / text-display-md (desktop)
Menu section title    → text-display-sm
Menu item name        → text-body-lg (weight 500)
Menu item description → text-body-md, text-secondary color
Price                 → text-ui-lg (weight 600)
Allergen label        → text-ui-md (weight 600), never below body-sm
Metadata (pickup)     → text-body-sm
```

### Dashboard (creator-facing)

```
Page title            → text-display-md (desktop) / text-display-sm (mobile)
Section header        → text-display-sm
Table header          → text-ui-md (weight 600), uppercase tracking optional
Table cell            → text-body-sm
Form label            → text-ui-md (weight 500)
Helper text           → text-body-sm, text-tertiary color
```

### Marketing

```
Hero headline         → text-display-xl
Subhead               → text-body-lg
CTA button            → text-ui-lg
```

---

## Weight Usage

| Weight | Value | Usage |
|--------|-------|-------|
| Regular | 400 | Body text, descriptions |
| Medium | 500 | UI labels, emphasized body, prices |
| Semibold | 600 | Headings, section titles, buttons |
| Bold | 700 | Display headlines, hero text only |

Avoid weights below 400 and above 700. Do not use italic for emphasis in UI — use weight or color.

---

## Letter Spacing & Line Length

| Context | Letter spacing | Max line length |
|---------|----------------|-----------------|
| Display headlines | `-0.02em` at xl sizes | — |
| Body text | `0` (default) | **65 characters** (~35rem) |
| UI labels | `0.01em` at sm/xs sizes | — |
| All-caps labels (if used) | `0.05em` | — |

Long-form content (policies, help articles) uses `text-body-md` with max-width container (~680px) for comfortable reading.

---

## Text Color Pairings

Typography tokens define size and weight; color comes from [color foundations](color.md):

| Role | Default color token |
|------|---------------------|
| Headings | `text-primary` |
| Body | `text-primary` |
| Secondary | `text-secondary` |
| Captions / metadata | `text-tertiary` |
| Links | `text-link` → `text-link-hover` on hover |
| Error inline | `color-error-default` |
| Disabled | `text-disabled` |

---

## Accessibility

- **Minimum 14px** for essential content
- **Line height ≥ 1.5** for body text (1.6 preferred)
- **No justified text** — left-align for readability
- **No all-caps paragraphs** — all-caps acceptable for short UI labels only
- Support **200% browser zoom** without horizontal scroll or clipped text
- Semantic HTML headings (`h1`–`h6`) match visual hierarchy — one `h1` per page

→ Full requirements: [accessibility-standards.md](../accessibility-standards.md)

---

## Font Loading

- Load Inter via **variable font** (single file, weights 400–700)
- Use `font-display: swap` to prevent invisible text
- Subset to Latin character set at launch; expand for localization
- System font fallback ensures content is readable before webfont loads

---

## Related Documents

- [Founding Constitution](../../company/constitution.md)
- [Design Principles](../principles.md)
- [Color Foundations](color.md)
- [Spacing Foundations](spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Naming Conventions](../../brand/naming-conventions.md)
- [Components Overview](../components-overview.md)
