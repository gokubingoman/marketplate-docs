# Badges

> Compact status, category, and trust indicators — verification, order status, dietary info, and cuisine tags.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Badges communicate compact metadata at a glance. Trust-critical badges (verification) use consistent icon + label treatment so customers learn to recognize them once — [trust in design](../principles.md#trust-in-design).

### Variants

| Variant | Usage | Semantic color |
|---------|-------|----------------|
| **Verification badge** | "Verified Identity," "Verified Kitchen" | Trust |
| **Status badge** | Order status — "Confirmed," "Ready for pickup," "Completed" | Status-specific |
| **Dietary badge** | "Vegan," "Gluten-free," "Contains nuts" | Neutral or warning |
| **Category badge** | Cuisine type, menu section tags | Neutral |

**Appears on:** Creator profiles, menu items, order lists, checkout trust strip.

→ Verification naming: [naming conventions — verification labels](../../brand/naming-conventions.md#verification--trust-labels)  
→ Inventory context: [components-overview.md](../components-overview.md#badges)

---

## Anatomy

```
┌──────────────────────┐
│ [Icon]  Label text   │  ← Inline flex container
└──────────────────────┘
```

| Part | Required | Description |
|------|----------|-------------|
| **Container** | Yes | Inline pill or rounded rect |
| **Icon** | Verification: yes; others: optional | 12–14px; `aria-hidden="true"` when label present |
| **Label** | Yes | Short text — 1–3 words |
| **Tooltip trigger** | Verification only | Info icon or hover/focus reveals credential detail |

Badges are **non-interactive** except verification badges, which may open a tooltip or link to verification detail.

---

## Sizes

| Size | Height | Horizontal padding | Typography | Icon |
|------|--------|-------------------|------------|------|
| **sm** | 20px | `space-2` (8px) | `text-ui-sm` | 12px |
| **md** | 24px | `space-2` (8px) | `text-ui-sm` | 14px |
| **lg** | 28px | `space-3` (12px) | `text-ui-md` | 14px |

**Border radius:** `radius-sm` (6px) for rect badges; `radius-full` for pill badges. Pick one style per context — pills for status, rounded rect for dietary.

**Gap (icon to label):** `space-1` (4px).

---

## Variant Specifications

### Verification badge

| Property | Value |
|----------|-------|
| Background | `color-trust-subtle` |
| Text | `color-trust-default` |
| Icon | Shield/checkmark, trust hue |
| Tooltip | Credential type, verification date |

Labels must match [naming conventions](../../brand/naming-conventions.md#verification--trust-labels) exactly — "Verified Kitchen," not "Kitchen verified."

### Status badge — order lifecycle

| Status | Background | Text | Icon |
|--------|------------|------|------|
| **Pending** | `color-neutral-100` | `text-secondary` | Clock |
| **Confirmed** | `color-trust-subtle` | `color-trust-default` | Check |
| **Preparing** | `color-warning-subtle` | `color-warning-default` | — |
| **Ready for pickup** | `color-success-subtle` | `color-success-default` | — |
| **Completed** | `color-neutral-100` | `text-tertiary` | — |
| **Cancelled** | `color-error-subtle` | `color-error-default` | — |

Status text always accompanies color — never color alone.

### Dietary badge

| Type | Background | Text | Notes |
|------|------------|------|-------|
| **Positive** (Vegan, GF) | `color-success-subtle` | `color-success-default` | Preference tags |
| **Contains allergen** | `color-warning-subtle` | `color-warning-default` | "Contains nuts," "Contains dairy" |
| **Neutral** | `color-neutral-100` | `text-secondary` | Optional tags |

Allergen badges use **warning** treatment — they signal caution, not error.

### Category badge

| Property | Value |
|----------|-------|
| Background | `color-neutral-100` |
| Text | `text-secondary` |
| Border | optional `border-subtle` 1px |

---

## States

Badges are predominantly static. Verification badges with tooltips:

| State | Behavior |
|-------|----------|
| **Default** | Static display |
| **Hover** (tooltip trigger) | Tooltip appears after 300ms delay |
| **Focus** | Tooltip visible; `border-focus` on trigger |
| **Active** | Tooltip remains until dismiss |
| **Disabled** | N/A — badges are not form controls |

No loading state for badges. During data fetch, omit badge until data resolves — do not show skeleton badges.

---

## Component Tokens

| Token | Maps to | Context |
|-------|---------|---------|
| `badge-trust-background` | `color-trust-subtle` | Verification |
| `badge-trust-text` | `color-trust-default` | Verification label |
| `badge-success-background` | `color-success-subtle` | Ready, positive dietary |
| `badge-success-text` | `color-success-default` | — |
| `badge-warning-background` | `color-warning-subtle` | Preparing, allergens |
| `badge-warning-text` | `color-warning-default` | — |
| `badge-error-background` | `color-error-subtle` | Cancelled |
| `badge-error-text` | `color-error-default` | — |
| `badge-neutral-background` | `color-neutral-100` | Category, completed |
| `badge-neutral-text` | `text-secondary` | — |

→ Semantic source: [color foundations](../foundations/color.md)

---

## Token Usage Summary

| Property | Token |
|----------|-------|
| Label typography | `text-ui-sm` (sm/md), `text-ui-md` (lg) |
| Padding | `space-2` horizontal, vertical centered |
| Icon gap | `space-1` |
| Border radius | `radius-sm` or `radius-full` |
| Tooltip text | `text-body-sm`, `text-primary` |

→ Typography: [typography foundations](../foundations/typography.md)  
→ Spacing: [spacing foundations](../foundations/spacing.md)

---

## Accessibility

Target: **WCAG 2.2 AA** → [accessibility standards](../accessibility-standards.md)

| Requirement | Implementation |
|-------------|----------------|
| **Text labels** | Every badge includes visible text — no color-only status |
| **Verification alt** | Icon badges: `alt="Verified Kitchen"` matching visible label |
| **Tooltip** | Trigger is keyboard-focusable; tooltip content in `role="tooltip"` linked via `aria-describedby` |
| **Touch target** | Tooltip trigger: 44×44px hit area even if badge is smaller |
| **Allergen badges** | Full allergen name — "Contains tree nuts," not "Nuts" alone on checkout |
| **Screen reader** | Badges in lists: content in DOM order; no `aria-live` for static badges |
| **Contrast** | All text/background pairs pass AA — verified in [color foundations](../foundations/color.md) |

Do not convey order status by badge color alone — always include status text in order cards and detail views.

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| **Mobile (320–767px)** | Badges wrap to next line; max 3 visible on menu cards — overflow to "+2 more" text link. Verification badge always visible on creator header. |
| **Tablet (768–1023px)** | Full badge row visible on cards. |
| **Desktop (1024px+)** | Same as tablet. Tooltip on hover for verification detail. |

**Checkout trust strip:** Verification badges displayed horizontally with `space-2` gap; wrap if needed. Never truncate verification labels.

**Font scaling:** Badge text does not scale below `text-ui-sm` (12px) — supplementary only per [typography](../foundations/typography.md).

---

## Do / Don't

### Do

- Pair **icon + text** on verification badges
- Use **exact verification labels** from naming conventions
- Limit badges per card to **avoid noise** — max 3 dietary + overflow
- Use **warning treatment** for allergen "contains" badges
- Provide **tooltip detail** for verification credentials

### Don't

- Use badges for long sentences — use body text
- Rely on **red/green color alone** for status
- Abbreviate allergen names on checkout or item detail
- Make every tag a badge — plain text comma lists work for low-priority metadata
- Use badges as buttons — use [buttons](buttons.md) for actions
- Invent verification labels outside naming conventions

---

## Related Documents

- [Design Principles](../principles.md)
- [Components Overview](../components-overview.md#badges)
- [Color Foundations](../foundations/color.md)
- [Typography Foundations](../foundations/typography.md)
- [Spacing Foundations](../foundations/spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Naming Conventions — Verification Labels](../../brand/naming-conventions.md#verification--trust-labels)
- [Cards](cards.md)
- [Avatars](avatars.md)
