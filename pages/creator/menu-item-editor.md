# Creator Menu Item Editor

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/catalog/items/new` · `/creator/catalog/items/{item_id}/edit`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Menu Item Editor is the **create/edit form for a single listing** — photos, description, pricing, allergens, dietary tags, fulfillment options, and availability rules. It is the most detail-dense creator workflow and the primary enforcement point for [listing transparency](../../product/marketplace-mechanics.md#transparency).

Every field maps to customer trust: incomplete allergen data blocks publish. Cottage food category violations block save.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| Create professional listings with accurate food photography | Improve discovery conversion |
| Declare allergens and ingredients completely | Prevent safety incidents |
| Set pricing, lead times, and capacity per item | Reduce overselling and disputes |
| Save drafts and publish when ready | Support iterative menu building |

**Primary action:** "Save & publish" when validation passes; "Save draft" when incomplete; "Save changes" on edit.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Baker](../../product/personas.md#baker) | Custom pricing, lead times, deposit items |
| **Secondary** | [Cottage Food Operator](../../product/personas.md#cottage-food-operator) | Category restrictions, label requirements |
| **Secondary** | [Meal Prep Business](../../product/personas.md#meal-prep-business) | Nutrition fields, batch identifiers |
| **Anti-persona** | Customer | Read-only product page is customer surface |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| [Catalog](./catalog.md) | Add item, edit item, duplicate |
| [Dashboard](./dashboard.md) | "Add first menu item" onboarding |
| [Compliance](./compliance.md) | Fix allergen gap deep link with item pre-loaded |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Catalog](./catalog.md) | Save, cancel, back breadcrumb |
| [Availability](./availability.md) | Link from item-level schedule override |
| [Compliance](./compliance.md) | Blocked category explanation |

### Breadcrumbs

`Dashboard → Catalog → New menu item` or `Dashboard → Catalog → Edit: Sourdough Loaf`

---

## Layout

Single-column form with sticky footer action bar. Progressive sections — essentials above fold; advanced below.

```
┌─────────────────────────────────────────────────────────────────┐
│ ← Catalog    New menu item                    [ Save draft ]    │
├─────────────────────────────────────────────────────────────────┤
│ PHOTOS *                                                        │
│ ┌────────┐ ┌────────┐ ┌ + Add photo ──────────────────────────┐ │
│ │ primary│ │        │ │  Drag or upload · JPG/PNG · Max 5    │ │
│ └────────┘ └────────┘ └───────────────────────────────────────┘ │
│                                                                 │
│ BASICS *                                                        │
│ Name [________________________]                                 │
│ Section [ Weekend Bakes ▾ ]                                     │
│ Description [________________________________]                  │
│                                                                 │
│ PRICING *                                                       │
│ Price [ $________ ]  ○ Fixed  ○ Starting at  ○ Custom quote    │
│                                                                 │
│ ALLERGENS & DIETARY *  (required before publish)                │
│ ☑ Contains: [ tree nuts ▾ ] [ dairy ▾ ] [ + Add ]              │
│ Dietary tags: [ Vegan ] [ GF ] [ + Add ]                        │
│ Ingredients list [________________________________]             │
│                                                                 │
│ AVAILABILITY                                                    │
│ ○ Follow store schedule  ○ Custom schedule  ○ Sold out          │
│ Lead time: [ 24 ] hours · Max per day: [ 20 ]                   │
│ Fulfillment: ☑ Pickup  ☐ Delivery  ☐ Catering                   │
│                                                                 │
│ PRODUCTION LOCATION *                                           │
│ [ Verified Kitchen: Main Kitchen ▾ ]  [Verified Kitchen badge] │
├─────────────────────────────────────────────────────────────────┤
│              [ Save & publish ]  ← PRIMARY    [ Cancel ]        │
└─────────────────────────────────────────────────────────────────┘
```

---

## Components

| Component | Usage | DS reference |
|-----------|-------|--------------|
| **File upload** | Menu photos (multi) | [Inputs — File upload](../../design-system/components-overview.md#inputs) |
| **Text input** | Name, price, lead time, max quantity | [Inputs — Text](../../design-system/components-overview.md#inputs) |
| **Textarea** | Description, ingredients list | [Inputs — Textarea](../../design-system/components-overview.md#inputs) |
| **Select / dropdown** | Section, allergens, kitchen location | [Inputs — Select](../../design-system/components-overview.md#inputs) |
| **Checkbox** | Allergen contains flags, fulfillment types | [Inputs — Checkbox](../../design-system/components-overview.md#inputs) |
| **Radio** | Pricing model, availability mode | [Inputs — Radio](../../design-system/components-overview.md#inputs) |
| **Dietary badge** | Tag preview chips | [Badges — Dietary](../../design-system/components-overview.md#badges) |
| **Verification badge** | Kitchen selector confirmation | [Badges — Verification](../../design-system/components-overview.md#badges) |
| **Primary button** | Save & publish | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Secondary button** | Save draft | [Buttons — Secondary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | Cancel | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Confirmation modal** | Discard unsaved changes, delete item | [Modals — Confirmation](../../design-system/components-overview.md#modals) |
| **Toast** | Save success, validation summary | [Toasts](../../design-system/components-overview.md#toasts) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Photo upload** | Drag-drop or file picker; first image = primary; reorder via drag |
| **Save & publish** | Validates required fields + compliance; publishes to Active catalog |
| **Save draft** | Saves partial data; no storefront visibility |
| **Allergen selector** | Multi-select from standardized allergen taxonomy; "None" requires explicit confirm |
| **Pricing model** | Fixed / Starting at / Custom quote changes checkout behavior |
| **Kitchen selector** | Only verified kitchens listed; required per [kitchen verification](../../product/marketplace-mechanics.md#kitchen-verification) |
| **Category restriction** | Real-time validation for cottage food — inline block with policy link |
| **Cancel** | Unsaved changes modal if dirty |
| **Auto-save** | Draft auto-save every 30s with subtle "Saved" indicator |

Validation errors inline at field level; summary at top on submit failure.

---

## Animations

| Trigger | Motion |
|---------|--------|
| Section validation error | Gentle shake on summary banner + scroll to first error | 200ms |
| Photo upload progress | Progress bar on thumbnail | — |
| Publish success | Toast + optional confetti-free checkmark (calm) | 300ms |
| Sticky footer appear | Slide up when user scrolls past basics | 200ms |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Single column; photo grid 2-wide; sticky footer with full-width primary |
| **Tablet** | Single column max-width centered |
| **Desktop** | Two-column optional for photos + basics side-by-side; form max-width 720px |

Photo upload remains touch-friendly — 44px minimum tap targets on mobile.

---

## Loading States

- Edit mode: skeleton form while item loads
- Save/publish: primary button loading spinner; form disabled
- Photo upload: per-thumbnail progress overlay
- Kitchen list: dropdown skeleton until verified locations load

---

## Error States

| Error | Recovery |
|-------|----------|
| Validation failure | Inline field errors + summary banner with jump links |
| Publish blocked — allergens | Highlight Allergens section; explain checkout requirement |
| Publish blocked — unverified kitchen | Kitchen selector error + link to [Compliance](./compliance.md) |
| Category not permitted (cottage) | Save as draft only; inline policy explanation |
| Upload failed | Retry per photo; preserve other form state |
| Network save failure | Toast + retry; local draft preserved |

---

## Empty States

| Scenario | Treatment |
|----------|-------------|
| **New item** | Empty photo upload zone with guidance; placeholder in description |
| **Duplicate item** | Pre-filled from source; "(Copy)" appended to name |
| **No verified kitchen** | Kitchen section empty state with CTA to [Compliance](./compliance.md) |

---

## Permissions

| Role | Access |
|------|--------|
| Owner | Full create/edit/publish/delete |
| Staff — catalog | Create/edit draft; publish if owner-enabled setting |
| Unverified creator | Draft only; publish disabled with explanation |

---

## Analytics

| Event | Properties |
|-------|------------|
| `creator_menu_item_editor_viewed` | `mode` (new/edit), `item_id` |
| `creator_menu_item_saved` | `item_id`, `save_type` (draft/publish), `duration_seconds` |
| `creator_menu_item_publish_blocked` | `reason` (allergens, kitchen, category) |
| `creator_menu_item_photo_uploaded` | `photo_count` |
| `creator_menu_item_abandoned` | `fields_completed_count`, `mode` |

Quality metric: % published items with complete allergen data.

---

## Accessibility

- Required fields marked with text "(required)" — not color alone
- Error summary: `role="alert"` with focus move to summary on submit fail
- Photo upload: keyboard-accessible file input + alt text prompt per image
- Allergen checkboxes: grouped with `fieldset`/`legend`
- Sticky footer does not trap focus; form submittable via keyboard
- Price input: `inputmode="decimal"`, labeled currency

---

## SEO

Not applicable — authenticated editor route.

Published items affect customer-facing product URLs (separate customer page spec).

---

## Future Improvements

- Rich text editor for descriptions
- Variant builder (size/price matrix)
- Nutrition facts panel (meal prep)
- AI photo quality check (lighting, framing)
- Ingredient parser from recipe paste
- Deposit and cancellation policy per item (custom cakes)

---

## API Requirements

| Endpoint | Purpose |
|----------|---------|
| `GET /api/v1/creator/catalog/items/{id}` | Load item for edit |
| `POST /api/v1/creator/catalog/items` | Create item |
| `PATCH /api/v1/creator/catalog/items/{id}` | Update item |
| `POST /api/v1/creator/catalog/items/{id}/photos` | Upload photos |
| `DELETE /api/v1/creator/catalog/items/{id}/photos/{photo_id}` | Remove photo |
| `GET /api/v1/creator/kitchens` | Verified production locations |
| `POST /api/v1/creator/catalog/items/validate` | Pre-publish compliance check |
| `GET /api/v1/creator/compliance/category-rules` | Jurisdiction restrictions |

---

## Related Pages

- [Catalog](./catalog.md) — list manager
- [Availability](./availability.md) — store-level schedule overrides
- [Compliance](./compliance.md) — kitchen verification, category rules
- [Storefront Settings](./storefront-settings.md) — brand context
- [Order Detail](./order-detail.md) — how items appear on orders
- [Dashboard](./dashboard.md) — onboarding action items
