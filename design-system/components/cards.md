# Cards

> Elevated surfaces that group related content for scanning — menu items, orders, creators, metrics, and reviews.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Cards group related content into scannable, elevated surfaces. They implement [calm interfaces](../principles.md#1-calm-interfaces) and [whitespace as a feature](../principles.md#2-whitespace-is-a-feature) — generous internal padding, minimal chrome, content-led layout.

### Variants

| Variant | Usage | Interactive |
|---------|-------|-------------|
| **Menu item card** | Food photo, name, price, dietary tags, add action | Yes — tap opens detail or adds to cart |
| **Order card** | Order summary, status, pickup details | Yes — navigates to order detail |
| **Creator card** | Discovery — photo, name, verification, cuisine tags | Yes — navigates to storefront |
| **Dashboard stat card** | Metrics — orders, revenue, pending verifications | Static |
| **Review card** | Customer review with date, rating, text | Static |

**Appears on:** Storefronts, discovery, dashboards, order history.

→ Inventory context: [components-overview.md](../components-overview.md#cards)

---

## Anatomy

### Menu item card

```
┌─────────────────────────────────┐
│                                 │
│         Image (16:9)            │  ← Media (optional on list layout)
│                                 │
├─────────────────────────────────┤
│  Item name              $12.00  │  ← Title row
│  Short description…             │  ← Description
│  [Vegan] [GF]                   │  ← Badges
│                      [Add +]    │  ← Action (button)
└─────────────────────────────────┘
```

### Order card

```
┌─────────────────────────────────┐
│  Order #1234          [Status]  │  ← Header + badge
│  3 items · $45.00               │  ← Metadata
│  Pickup: Today, 5:30 PM         │  ← Key detail
│  ─────────────────────────────  │  ← Divider (border-subtle)
│  View details →                 │  ← Footer action
└─────────────────────────────────┘
```

### Creator card

```
┌─────────────────────────────────┐
│  ┌────┐  Creator name             │
│  │ AV │  [Verified Kitchen]      │  ← Avatar + verification
│  └────┘  Italian · 0.8 mi         │  ← Tags + distance
│         Short tagline…            │
└─────────────────────────────────┘
```

| Part | Required | Description |
|------|----------|-------------|
| **Container** | Yes | `surface-default` with border or shadow |
| **Media** | Variant-dependent | 16:9 image for menu/creator; none for stat |
| **Header** | Yes | Title, price, or metric |
| **Body** | No | Description, metadata |
| **Footer** | No | Actions, timestamps |
| **Badges** | No | Status, dietary, verification → [badges](badges.md) |

---

## Sizes & Layout

| Property | Compact | Default |
|----------|---------|---------|
| **Padding** | `space-5` (20px) | `space-6` (24px) |
| **Internal gap** | `space-3` | `space-4` |
| **Border radius** | `radius-lg` (12px) | `radius-lg` (12px) |
| **Stack gap (between cards)** | `space-4` | `space-6` |

### Image aspect ratios

| Variant | Ratio | Object fit |
|---------|-------|------------|
| Menu item (grid) | 16:9 | cover |
| Menu item (list) | 1:1 thumbnail, 80×80px | cover |
| Creator card | 1:1 avatar, 48–64px | cover |
| Review card | No image | — |

**Image border radius:** `radius-md` for thumbnails; top corners `radius-lg` for full-bleed card images.

---

## States (Interactive Cards)

| State | Visual treatment | Notes |
|-------|------------------|-------|
| **Default** | `surface-default`, `border-default` 1px OR subtle shadow | Prefer border for calm aesthetic |
| **Hover** | `border-default` darkens slightly; optional `surface-subtle` background | Pointer devices only |
| **Focus** | `border-focus` 2px outline on card or internal link | Card as `<a>` or wrapper with focusable child |
| **Active** | Brief background `surface-subtle` | 150ms transition |
| **Disabled** | Reduced opacity 0.5; no pointer events | Rare — prefer hiding unavailable items |
| **Loading** | Skeleton placeholders matching card anatomy | Static skeleton with `prefers-reduced-motion` |
| **Error** | Not applicable at card level | Use inline error or toast |

**Shadow token (optional):** `0 1px 3px rgba(26, 26, 26, 0.08)` — use border OR shadow, not both heavily.

Static stat cards have no hover state. No faux interactivity.

---

## Component Tokens

| Token | Maps to | Context |
|-------|---------|---------|
| `card-background` | `surface-default` | Card fill |
| `card-border` | `border-default` | Outline |
| `card-background-hover` | `surface-subtle` | Interactive hover |
| `card-padding` | `space-6` / `space-5` | Internal padding |
| `card-radius` | `radius-lg` | Corner radius |
| `card-title` | `text-body-lg` weight 500 | Menu item name |
| `card-price` | `text-ui-lg` weight 600 | Price display |
| `card-meta` | `text-body-sm` + `text-tertiary` | Timestamps, counts |

→ Semantic source: [color foundations](../foundations/color.md)

---

## Token Usage Summary

| Property | Token |
|----------|-------|
| Title (menu item) | `text-body-lg`, weight 500, `text-primary` |
| Title (section/card header) | `text-display-sm` |
| Description | `text-body-md`, `text-secondary` |
| Metadata | `text-body-sm`, `text-tertiary` |
| Price | `text-ui-lg`, weight 600, `text-primary` |
| Padding | `space-6` (default), `space-5` (compact/mobile) |
| Element gap | `space-4` |
| Divider | `border-subtle` |

→ Typography: [typography foundations](../foundations/typography.md)  
→ Spacing: [spacing foundations](../foundations/spacing.md)

---

## Accessibility

Target: **WCAG 2.2 AA** → [accessibility standards](../accessibility-standards.md)

| Requirement | Implementation |
|-------------|----------------|
| **Interactive cards** | Single `<a>` wrapping card OR heading link + distinct action buttons — not nested interactive elements |
| **Heading structure** | Card title as heading level appropriate to page (`h2`–`h4`) |
| **Images** | Descriptive `alt` on food/creator photos — [image requirements](../accessibility-standards.md#image--media) |
| **Allergen info** | Menu cards surface allergen badges with text labels; `aria-describedby` on item detail |
| **Focus** | Entire card clickable OR explicit "View" link — keyboard user must reach all actions |
| **Loading** | `aria-busy="true"` on card grid during fetch |
| **Stat cards** | Metric value in text, not color alone; include label — "24 orders" not just "24" |

Review cards: include reviewer name, date, and rating text — not stars alone.

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| **Mobile (320–767px)** | Menu items: single-column list layout with 80px thumbnail left. Creator cards: full width. Stat cards: 2-column grid. Padding: `space-5`. Cards stack with `space-4` gap. |
| **Tablet (768–1023px)** | Menu grid: 2 columns. Creator discovery: 2 columns. Dashboard stats: 3–4 columns. |
| **Desktop (1024px+)** | Menu grid: 2–3 columns depending on container. Creator grid: 3 columns. Stat row: 4 columns. Padding: `space-6`. |

**Interactive target on mobile:** Full card tap area meets 44px minimum height. "Add" button remains distinct control — `space-4` from card edge.

**Detail modal on mobile:** Tapping menu item card opens [detail modal](modals.md) instead of new page when viewport < 768px.

---

## Do / Don't

### Do

- Lead with **photography** on menu and creator cards — real content, not placeholders
- Keep **one primary action** per interactive card
- Use **consistent image ratios** within a grid
- Show **price and allergens** scannable without opening detail
- Prefer **borders over heavy shadows** for calm aesthetic

### Don't

- Nest buttons inside link-wrapped cards
- Show more than **2 badge types** per menu card — prioritize allergens
- Use cards for single-line content — use list rows instead
- Animate cards on scroll (parallax, stagger) — violates [motion principles](../principles.md#3-motion-communicates-state)
- Display stat cards as clickable when they aren't
- Truncate allergen information on item cards

---

## Related Documents

- [Design Principles](../principles.md)
- [Components Overview](../components-overview.md#cards)
- [Color Foundations](../foundations/color.md)
- [Typography Foundations](../foundations/typography.md)
- [Spacing Foundations](../foundations/spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Badges](badges.md)
- [Avatars](avatars.md)
- [Buttons](buttons.md)
- [Modals](modals.md)
