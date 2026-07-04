# Creator Catalog (Menu / Listing Manager)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/catalog`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Catalog page is where creators **build and manage what they sell** — menu sections, items, pricing, photos, allergens, and availability states. It is the supply-side counterpart to customer-facing discovery and checkout.

Without a complete, compliant catalog, creators cannot go live. This page enforces [listing transparency](../../product/marketplace-mechanics.md#transparency) and jurisdiction-aware restrictions (especially for [Cottage Food Operators](../../product/personas.md#cottage-food-operator)).

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| Organize menu into scannable sections | Improve customer conversion on storefront |
| Quickly see item status (live, draft, sold out, blocked) | Accurate availability in discovery |
| Identify incomplete or non-compliant listings | Reduce trust incidents and checkout failures |
| Add and edit items efficiently | Faster creator activation (first listing → first order) |

**Primary action:** Contextual — "Add menu item" when catalog empty or incomplete; "Fix 2 items" when compliance gaps exist; "Edit item" when viewing existing catalog.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Baker](../../product/personas.md#baker) | Many SKUs, seasonal items, lead times |
| **Secondary** | [Meal Prep Business](../../product/personas.md#meal-prep-business) | Batch items, nutrition transparency |
| **Secondary** | [Cottage Food Operator](../../product/personas.md#cottage-food-operator) | Category restrictions enforced |
| **Anti-persona** | Customer browsing menu | Customer storefront is separate surface |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Sidebar nav | "Catalog" / "Menu" |
| [Dashboard](./dashboard.md) | Action item: missing allergen info, add first item |
| [Menu Item Editor](./menu-item-editor.md) | Save/back navigation |
| [Compliance](./compliance.md) | Blocked listing remediation link |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Menu Item Editor](./menu-item-editor.md) | Add item, edit item, duplicate item |
| [Availability](./availability.md) | Global schedule link from catalog header |
| [Storefront Settings](./storefront-settings.md) | Preview storefront |
| [Compliance](./compliance.md) | Item blocked by category restriction |

### Breadcrumbs

`Dashboard → Catalog`

---

## Layout

Section-grouped list with Active / Draft segmented toggle. Compliance and verification warnings surface at section level.

```
┌─────────────────────────────────────────────────────────────────┐
│ Catalog                          [ Preview storefront ]         │
├─────────────────────────────────────────────────────────────────┤
│ [ Active menu ] [ Draft menu ]              [ + Add menu item ] │ ← Primary when empty
├─────────────────────────────────────────────────────────────────┤
│ ⚠ 2 items need allergen information before they can go live    │
├─────────────────────────────────────────────────────────────────┤
│ SECTION: Weekend Bakes                           [ Edit section ]│
│ ┌ Menu item card ─────────────────────────────────────────────┐ │
│ │ [photo] Sourdough Loaf · $12 · Live · GF                  │ │
│ │ Sold out · Pickup only                                    │ │
│ └───────────────────────────────────────────────────────────┘ │
│ ┌ Menu item card ─────────────────────────────────────────────┐ │
│ │ [photo] Custom Cake · From $85 · Draft · ⚠ Allergens      │ │
│ └───────────────────────────────────────────────────────────┘ │
│                                                                 │
│ SECTION: Meal Prep Bowls                                        │
│ ...                                                             │
├─────────────────────────────────────────────────────────────────┤
│ [ Reorder sections ]                                            │
└─────────────────────────────────────────────────────────────────┘
```

---

## Components

| Component | Usage | DS reference |
|-----------|-------|--------------|
| **Segmented control** | Active / Draft menu toggle | [Navigation — Segmented control](../../design-system/components-overview.md#navigation) |
| **Menu item card** | Item row with photo, price, status, tags | [Cards — Menu item card](../../design-system/components-overview.md#cards) |
| **Status badge** | Live, Draft, Sold out, Blocked | [Badges — Status](../../design-system/components-overview.md#badges) |
| **Dietary badge** | GF, Vegan, Contains nuts | [Badges — Dietary](../../design-system/components-overview.md#badges) |
| **Category badge** | Section tags, cuisine | [Badges — Category](../../design-system/components-overview.md#badges) |
| **Primary button** | Add menu item (empty state / header) | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Secondary button** | Preview storefront | [Buttons — Secondary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | Edit section, reorder | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Search input** | Filter items by name | [Inputs — Search](../../design-system/components-overview.md#inputs) |
| **Confirmation modal** | Delete item, bulk unpublish | [Modals — Confirmation](../../design-system/components-overview.md#modals) |
| **Toast** | Quick actions: mark sold out, duplicate | [Toasts](../../design-system/components-overview.md#toasts) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Add menu item** | Navigate to [Menu Item Editor](./menu-item-editor.md) (new) |
| **Item card tap** | Open editor for that item |
| **Quick actions (overflow)** | Mark sold out, duplicate, move section, delete |
| **Active / Draft toggle** | Filters list; draft items never appear on storefront |
| **Compliance warning banner** | Tap filters to affected items |
| **Reorder sections** | Drag-and-drop (desktop) or explicit reorder mode (mobile) |
| **Preview storefront** | Opens customer-facing profile in new tab |
| **Search** | Filters across all sections; highlights matches |

Sold-out toggle is instant with toast undo — no page navigation.

---

## Animations

| Trigger | Motion |
|---------|--------|
| Section expand/collapse | Height accordion | 250ms |
| Drag reorder | Item lifts with shadow; drop zone highlight | 200ms |
| Mark sold out | Badge crossfade Live → Sold out | 150ms |
| Tab switch Active/Draft | Crossfade list | 200ms |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Single column cards; FAB for Add item; overflow menu on cards |
| **Tablet** | Two-column card grid within sections |
| **Desktop** | Dense list option with thumbnail column; drag reorder enabled |

Add item CTA: header button on desktop/tablet; FAB on mobile (same primary styling — one primary action visible).

---

## Loading States

- Section headers + 6 item card skeletons on first load
- Inline skeleton on single item after quick action
- Preview storefront opens immediately; catalog reloads on return if stale

---

## Error States

| Error | Recovery |
|-------|----------|
| Catalog fetch failed | Retry banner |
| Publish blocked (compliance) | Inline on item card + link to [Compliance](./compliance.md) |
| Category restriction (cottage food) | Item card "Blocked" with jurisdiction explanation |
| Photo upload failed (from editor return) | Item saves as draft; warning on card |

---

## Empty States

| Scenario | Message | Primary action |
|----------|---------|----------------|
| **No items ever** | "Your menu is empty — add your first item to start selling" | [Add menu item] |
| **Draft only** | "No active items — publish drafts to go live" | Select draft to edit |
| **Active empty, drafts exist** | Toggle prompt to Draft tab | — |
| **Search no results** | "No items match your search" | [Clear search] |

Illustration: calm, food-forward empty state — not an error tone.

---

## Permissions

| Role | Access |
|------|--------|
| Owner | Full CRUD, publish, delete |
| Staff — catalog | Add/edit items; no delete |
| Staff — read-only | View only |
| Unverified | Draft-only; cannot publish live listings |

Live listings require verified kitchen per [trust model](../../product/marketplace-mechanics.md#kitchen-verification).

---

## Analytics

| Event | Properties |
|-------|------------|
| `creator_catalog_viewed` | `active_count`, `draft_count`, `blocked_count` |
| `creator_catalog_item_clicked` | `item_id`, `status` |
| `creator_catalog_add_item_clicked` | `source` (header, empty_state, fab) |
| `creator_catalog_sold_out_toggled` | `item_id`, `sold_out` |
| `creator_catalog_preview_storefront` | — |
| `creator_catalog_compliance_warning_clicked` | `affected_item_count` |

Activation funnel: first item created → first item published → first order.

---

## Accessibility

- Sections use heading hierarchy (`h2` section, `h3` item name)
- Drag reorder has keyboard alternative: move up/down buttons in reorder mode
- Sold out status: text label + badge, not color alone
- Item cards: entire card focusable with descriptive `aria-label`
- Active/Draft tabs: proper tab semantics

---

## SEO

Not applicable — authenticated creator route.

Storefront preview link opens indexed customer URL (creator's public profile).

---

## Future Improvements

- Bulk import (CSV)
- Seasonal scheduling (auto publish/unpublish dates)
- Variant management UI (sizes, add-ons)
- Nutrition label builder for meal prep
- AI-assisted description and allergen suggestions (human confirms)
- Collection/event mode for pop-ups

---

## API Requirements

| Endpoint | Purpose |
|----------|---------|
| `GET /api/v1/creator/catalog` | Sections + items with status, compliance flags |
| `GET /api/v1/creator/catalog/items` | Flat list with filters: `status`, `q`, `compliance_issue` |
| `PATCH /api/v1/creator/catalog/items/{id}` | Quick updates: sold_out, section_id, sort_order |
| `DELETE /api/v1/creator/catalog/items/{id}` | Soft delete with confirmation |
| `PUT /api/v1/creator/catalog/sections/order` | Section reorder |
| `GET /api/v1/creator/catalog/compliance-summary` | Count of items needing attention |

---

## Related Pages

- [Menu Item Editor](./menu-item-editor.md) — create/edit item
- [Availability](./availability.md) — schedule affecting item availability
- [Storefront Settings](./storefront-settings.md) — brand context for preview
- [Compliance](./compliance.md) — listing eligibility
- [Dashboard](./dashboard.md) — catalog action items
- [Order Detail](./order-detail.md) — items as ordered
- [Analytics](./analytics.md) — item performance (future)
