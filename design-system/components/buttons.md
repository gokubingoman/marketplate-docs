# Buttons

> Action triggers for forms, navigation, and confirmations — one primary action per context.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Buttons trigger user actions: submit forms, navigate, confirm decisions, and initiate async operations. They implement the [one primary action](../principles.md#4-one-primary-action-per-screen) principle — each view hierarchy level has at most one filled primary button.

### Variants

| Variant | Usage | Example |
|---------|-------|---------|
| **Primary** | Single main action per view | "Place order," "Submit for review" |
| **Secondary** | Supporting actions alongside primary | "View menu," "Save draft" |
| **Ghost / text** | Tertiary, low-commitment actions | "Cancel," "Learn more" |
| **Destructive** | Irreversible actions — always requires confirmation modal | "Cancel order," "Delete item" |

**Appears on:** Every page — checkout, forms, dashboards, modals, empty states.

→ Inventory context: [components-overview.md](../components-overview.md#buttons)

---

## Anatomy

```
┌─────────────────────────────────────┐
│  [Icon]  Label  [Icon]              │  ← Container (button element)
└─────────────────────────────────────┘
     ↑       ↑        ↑
  Leading  Label   Trailing
  icon     text     icon
```

| Part | Required | Description |
|------|----------|-------------|
| **Container** | Yes | Interactive `<button>` or `<a role="button">` when navigation is action-like |
| **Label** | Yes | Action verb — "Place order," not "Submit" alone |
| **Leading icon** | No | 16–20px icon before label; `aria-hidden="true"` when label present |
| **Trailing icon** | No | External link or dropdown indicator only |
| **Loading indicator** | Conditional | Replaces or accompanies label in loading state |

Icon-only buttons require `aria-label` and meet 44×44px touch target.

---

## Sizes

| Size | Height | Horizontal padding | Typography | Icon size | Usage |
|------|--------|-------------------|------------|-----------|-------|
| **sm** | 36px | `space-3` (12px) | `text-ui-md` | 16px | Dense dashboards, inline actions, table rows |
| **md** | 44px | `space-4` (16px) | `text-ui-lg` | 20px | Default — forms, modals, cards |
| **lg** | 52px | `space-6` (24px) | `text-ui-lg` (weight 600) | 20px | Marketing CTAs, checkout primary |

**Minimum touch target:** 44×44 CSS pixels at all sizes. Size `sm` expands hit area with padding if visual height is below 44px.

**Border radius:** `radius-md` (8px) for all sizes.

**Icon + label gap:** `space-2` (8px).

---

## States

### Primary

| State | Background | Text | Border | Notes |
|-------|------------|------|--------|-------|
| **Default** | `color-trust-default` | `text-inverse` | none | — |
| **Hover** | `color-trust-hover` | `text-inverse` | none | Pointer devices only |
| **Focus** | `color-trust-default` | `text-inverse` | `border-focus` 2px outline, 2px offset | Always visible |
| **Active** | `color-trust-hover` | `text-inverse` | none | Scale none; darken background |
| **Disabled** | `color-neutral-200` | `text-disabled` | none | `aria-disabled="true"`, no pointer events |
| **Loading** | `color-trust-default` | hidden or sr-only label | none | Spinner + "Loading…" sr-only text |

### Secondary

| State | Background | Text | Border |
|-------|------------|------|--------|
| **Default** | `surface-default` | `text-primary` | `border-default` 1px |
| **Hover** | `surface-subtle` | `text-primary` | `border-default` |
| **Focus** | `surface-default` | `text-primary` | `border-focus` outline |
| **Active** | `color-neutral-200` | `text-primary` | `border-default` |
| **Disabled** | `surface-default` | `text-disabled` | `border-default` |
| **Loading** | `surface-default` | hidden/sr-only | `border-default` |

### Ghost / text

| State | Background | Text | Border |
|-------|------------|------|--------|
| **Default** | transparent | `text-link` | none |
| **Hover** | `color-trust-subtle` | `text-link-hover` | none |
| **Focus** | transparent | `text-link` | `border-focus` outline |
| **Active** | `color-trust-subtle` | `text-link-hover` | none |
| **Disabled** | transparent | `text-disabled` | none |
| **Loading** | transparent | hidden/sr-only | none |

### Destructive

| State | Background | Text | Border |
|-------|------------|------|--------|
| **Default** | `surface-default` | `color-error-default` | `color-error-default` 1px |
| **Hover** | `color-error-subtle` | `color-error-hover` | `color-error-hover` |
| **Focus** | `surface-default` | `color-error-default` | `border-focus` outline |
| **Active** | `color-error-subtle` | `color-error-hover` | `color-error-hover` |
| **Disabled** | `surface-default` | `text-disabled` | `border-default` |
| **Loading** | `surface-default` | hidden/sr-only | `color-error-default` |

**Never style destructive as primary filled.** Destructive confirmation modals use secondary styling for the destructive action inside the modal.

---

## Component Tokens

| Token | Maps to | Context |
|-------|---------|---------|
| `button-primary-background` | `color-trust-default` | Primary default |
| `button-primary-background-hover` | `color-trust-hover` | Primary hover/active |
| `button-primary-text` | `text-inverse` | Primary label |
| `button-secondary-background` | `surface-default` | Secondary default |
| `button-secondary-border` | `border-default` | Secondary border |
| `button-ghost-text` | `text-link` | Ghost label |
| `button-destructive-text` | `color-error-default` | Destructive label |
| `button-disabled-background` | `color-neutral-200` | Disabled primary |
| `button-disabled-text` | `text-disabled` | All disabled labels |

→ Semantic source: [color foundations](../foundations/color.md)

---

## Token Usage Summary

| Property | Token |
|----------|-------|
| Label typography (md/lg) | `text-ui-lg`, weight 500–600 |
| Label typography (sm) | `text-ui-md`, weight 500 |
| Internal padding | `space-3` (sm), `space-4` (md), `space-6` (lg) |
| Icon gap | `space-2` |
| Focus ring | `border-focus`, 2px width, 2px offset |
| Transition | 150ms ease-out (background, border) |

→ Typography: [typography foundations](../foundations/typography.md)  
→ Spacing: [spacing foundations](../foundations/spacing.md)

---

## Accessibility

Target: **WCAG 2.2 AA** → [accessibility standards](../accessibility-standards.md)

| Requirement | Implementation |
|-------------|----------------|
| **Keyboard** | `Enter` and `Space` activate; native `<button>` preferred |
| **Focus visible** | 2px `border-focus` outline, never removed |
| **Touch target** | Minimum 44×44px — [spacing foundations](../foundations/spacing.md#touch--pointer-targets) |
| **Disabled state** | Use `disabled` attribute or `aria-disabled="true"`; do not rely on color alone |
| **Loading state** | `aria-busy="true"`; preserve button dimensions; announce "Loading…" via `aria-live="polite"` on form submit |
| **Icon-only** | Required `aria-label` describing action |
| **Destructive** | Accessible name includes consequence — "Delete menu item, permanent" |
| **Link styled as button** | Use `<button>` for actions; use `<a>` only for navigation |

Loading buttons must not be double-submitted. Disable interaction while `aria-busy="true"`.

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| **Mobile (320–767px)** | Primary CTAs in checkout and forms use **full width** (`width: 100%`). Button groups stack vertically with `space-3` gap. Secondary/ghost pair below primary. |
| **Tablet (768–1023px)** | Full-width primary in narrow containers (`container-sm`); inline sizing in dashboard layouts. |
| **Desktop (1024px+)** | Inline/auto width by default. Button groups align horizontally — primary rightmost in dialogs (Western reading order). |

**Sticky mobile CTA bar:** Checkout "Place order" may sit in a sticky footer bar with `space-4` padding, `surface-default` background, `border-subtle` top border, `z-sticky`.

**Reduced motion:** No scale or bounce on press. Background color transition only — or instant swap with `prefers-reduced-motion`.

---

## Do / Don't

### Do

- Use **one primary button** per view hierarchy level
- Lead with **action verbs** — "Save changes," "Add to order"
- Show **loading state** during async operations; keep label in sr-only
- Use **destructive variant + confirmation modal** for irreversible actions
- Expand **sm buttons** to 44px touch target on mobile

### Don't

- Use multiple primary buttons on the same screen
- Style destructive actions as primary filled buttons
- Use buttons for navigation when a link is appropriate (use ghost link pattern)
- Disable buttons without explanation when blocking is non-obvious — add helper text
- Use icon-only buttons without `aria-label`
- Submit forms on Enter from non-submit inputs without user intent

---

## Related Documents

- [Design Principles](../principles.md)
- [Components Overview](../components-overview.md#buttons)
- [Color Foundations](../foundations/color.md)
- [Typography Foundations](../foundations/typography.md)
- [Spacing Foundations](../foundations/spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Modals](modals.md) — destructive confirmation pattern
- [Voice and Tone — CTAs](../../brand/voice-and-tone.md)
