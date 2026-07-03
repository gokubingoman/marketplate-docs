# Spacing Foundations

> Spacing scale, grid system, and layout rhythm for calm, consistent Marketplate interfaces.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Spacing is the primary tool for creating **calm, premium layouts**. Generous whitespace reduces cognitive load, separates trust-critical information (pricing, allergens, verification), and lets food photography breathe.

These foundations implement [design principles](../principles.md): whitespace as a feature, responsive across all breakpoints.

---

## Spacing Scale

Marketplate uses a **4px base unit**. All spacing values are multiples of 4.

| Token | Value | px | Typical usage |
|-------|-------|----|---------------|
| `space-0` | 0 | 0 | Reset |
| `space-0.5` | 0.125rem | 2 | Hairline adjustments (rare) |
| `space-1` | 0.25rem | 4 | Tight inline gaps (icon + label) |
| `space-2` | 0.5rem | 8 | Compact list item padding |
| `space-3` | 0.75rem | 12 | Form field internal padding (vertical) |
| `space-4` | 1rem | 16 | Default component padding, stack gaps |
| `space-5` | 1.25rem | 20 | Card internal padding (compact) |
| `space-6` | 1.5rem | 24 | Card internal padding (default) |
| `space-8` | 2rem | 32 | Section gaps within a page |
| `space-10` | 2.5rem | 40 | Between related sections |
| `space-12` | 3rem | 48 | Major section separation |
| `space-16` | 4rem | 64 | Page-level vertical rhythm |
| `space-20` | 5rem | 80 | Hero / marketing section padding |
| `space-24` | 6rem | 96 | Large marketing whitespace |

**Rule:** If a spacing value is not on this scale, it does not ship.

---

## Spacing Principles

### 1. Inside-out

Set **internal component padding** first, then **gaps between components**, then **section margins**.

```
Component padding  →  space-4 to space-6
Stack gap          →  space-4 to space-8
Section gap        →  space-10 to space-16
Page margin        →  space-6 (mobile) to space-16 (desktop)
```

### 2. Related things close, unrelated things far

| Relationship | Gap |
|--------------|-----|
| Label → input | `space-2` |
| Input → helper text | `space-1` |
| Form fields in a group | `space-4` |
| Unrelated form sections | `space-8` |
| Page sections | `space-12` to `space-16` |

### 3. More space, not more lines

Prefer increasing `space-*` over adding divider lines. When dividers are needed, use `border-subtle` — see [color foundations](color.md).

---

## Layout Grid

### Breakpoints

| Name | Min width | Max width | Columns | Gutter | Margin |
|------|-----------|-----------|---------|--------|--------|
| Mobile | 320px | 767px | 4 | 16px (`space-4`) | 16px (`space-4`) |
| Tablet | 768px | 1023px | 8 | 24px (`space-6`) | 32px (`space-8`) |
| Desktop | 1024px | 1439px | 12 | 24px (`space-6`) | 48px (`space-12`) |
| Wide | 1440px | — | 12 | 24px (`space-6`) | auto (max-width container) |

### Max-width containers

| Container | Max width | Usage |
|-----------|-----------|-------|
| `container-sm` | 640px | Forms, narrow content, checkout |
| `container-md` | 768px | Storefront menu (mobile-first) |
| `container-lg` | 1024px | Default page content |
| `container-xl` | 1200px | Dashboard layouts |
| `container-full` | 100% | Marketing heroes with full-bleed photography |

Content never spans full viewport width on desktop without intentional full-bleed design (hero images only).

---

## Common Layout Patterns

### Storefront menu (customer)

```
Page margin:     space-4 (mobile) → space-8 (tablet) → space-12 (desktop)
Creator header:  space-8 bottom margin
Menu sections:   space-12 between sections
Menu items:      space-6 between items
Item internal:   space-4 padding, space-2 between name and description
```

### Card

```
Padding:         space-6 (default), space-5 (compact/mobile)
Border radius:   12px (radius-lg — defined in Phase 2)
Gap (items):     space-4 between card elements
Stack margin:    space-6 between cards
```

### Form

```
Field group gap:     space-6
Label to input:      space-2
Input padding:       space-3 vertical, space-4 horizontal
Section divider gap: space-10
Submit button top:   space-8
```

### Dashboard table

```
Cell padding:    space-4 horizontal, space-3 vertical
Row gap:         0 (use border-subtle dividers)
Table to action: space-6
```

---

## Vertical Rhythm

Pages follow a consistent top-to-bottom rhythm:

```
┌─────────────────────────────────┐
│  Page margin top     space-8+   │
│  ┌───────────────────────────┐  │
│  │  Page title              │  │
│  │  space-8                 │  │
│  │  Section A               │  │
│  │  space-12                │  │
│  │  Section B               │  │
│  │  space-12                │  │
│  │  Section C               │  │
│  └───────────────────────────┘  │
│  Page margin bottom  space-16    │
└─────────────────────────────────┘
```

Marketing pages use `space-20` to `space-24` between major blocks for premium feel.

---

## Responsive Spacing

Spacing compresses on mobile — never eliminated.

| Context | Mobile | Tablet+ |
|---------|--------|---------|
| Page horizontal margin | `space-4` | `space-8` to `space-12` |
| Section vertical gap | `space-8` | `space-12` to `space-16` |
| Card padding | `space-5` | `space-6` |
| Stack gap (related items) | `space-3` to `space-4` | `space-4` to `space-6` |

Use consistent ratios when scaling — do not invent mobile-specific values off-scale.

---

## Touch & Pointer Targets

Minimum interactive target: **44×44 CSS pixels** per [accessibility standards](../accessibility-standards.md).

When visual element is smaller (e.g., icon button), expand the **touch target** with padding to meet 44px — the spacing scale supports this:

```
Icon size 20px + space-3 padding on each side = 20 + 12 + 12 = 44px ✓
```

---

## Z-Index Scale

Minimal, predictable stacking:

| Token | Value | Usage |
|-------|-------|-------|
| `z-base` | 0 | Default content |
| `z-dropdown` | 100 | Dropdowns, popovers |
| `z-sticky` | 200 | Sticky nav, order summary bar |
| `z-modal` | 300 | Modals, dialogs |
| `z-toast` | 400 | Toast notifications |
| `z-max` | 500 | Critical overlays (cookie consent) |

Avoid arbitrary z-index values.

---

## Border Radius (foundation)

Defined here for layout consistency; component specs in Phase 2.

| Token | Value | Usage |
|-------|-------|-------|
| `radius-sm` | 6px | Badges, small chips |
| `radius-md` | 8px | Buttons, inputs |
| `radius-lg` | 12px | Cards, modals |
| `radius-xl` | 16px | Large cards, hero images |
| `radius-full` | 9999px | Avatars, pills |

---

## Related Documents

- [Founding Constitution](../../company/constitution.md)
- [Design Principles](../principles.md)
- [Color Foundations](color.md)
- [Typography Foundations](typography.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Components Overview](../components-overview.md)
