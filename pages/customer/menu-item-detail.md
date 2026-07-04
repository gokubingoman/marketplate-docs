# Menu Item Detail

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/creator/:creatorSlug/item/:itemSlug`  
**Surface:** Customer marketplace  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Menu Item Detail page is where customers make an informed purchase decision on a specific dish. It provides complete transparency — ingredients, allergens, dietary tags, pricing, variants, lead time, and creator attribution — before the customer adds the item to their cart.

Allergen and ingredient information is **prominent and scannable**, not collapsed by default. This page embodies Marketplate's transparency standard: customers see what they need to trust before they pay.

---

## Goals

### User goals

- Understand exactly what the item contains and whether it fits dietary needs
- See allergen warnings clearly and completely
- Select variants (size, add-ons) and quantity
- Add item to cart with confidence
- Return to [Creator Storefront](creator-storefront.md) to continue browsing

### Business goals

- Reduce cart abandonment from surprise allergen or ingredient information at checkout
- Drive add-to-cart conversion with clear pricing and availability
- Minimize order errors from missing variant selection
- Support accessibility requirements for food safety information

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Often has dietary restrictions or allergen concerns |
| **Secondary** | First-time buyer from creator | Needs full transparency |
| **Anti-persona** | User skipping detail entirely | Quick-add on storefront serves this path |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| [Creator Storefront](creator-storefront.md) | Menu item card tap |
| [Search](search.md) | Item-level result tap |
| [Cart](cart.md) | Edit item link |
| Direct URL | Shareable item link |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Creator Storefront](creator-storefront.md) | Back link, breadcrumb, "Continue browsing" |
| [Cart](cart.md) | "View cart" after add; cart icon |
| [Checkout](checkout.md) | Only if cart shortcut with items (unusual on first add) |

### Breadcrumbs

`[Creator Name] > [Menu Section] > [Item Name]`

---

## Layout

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — back, cart                                     │
├─────────────────────────────────────────────────────────────┤
│  Mobile: full-bleed photo                                     │
│  Desktop: photo left (50%) | details right (50%)              │
├─────────────────────────────────────────────────────────────┤
│  Item name (h1)                                               │
│  Price — from $X.XX (if variants)                             │
│  Dietary badges — Vegan, Gluten-free, Contains nuts           │
├─────────────────────────────────────────────────────────────┤
│  Allergen block — PROMINENT, always visible                   │
│  "Contains: wheat, eggs, dairy" or "No major allergens listed"│
│  Disclaimer line — creator-reported, not Marketplate guarantee│
├─────────────────────────────────────────────────────────────┤
│  Description — creator-written, 1–3 paragraphs                │
├─────────────────────────────────────────────────────────────┤
│  Ingredients — full list, scannable                           │
├─────────────────────────────────────────────────────────────┤
│  Variants (if applicable)                                     │
│  Radio — size selection                                       │
│  Checkbox — add-ons                                             │
├─────────────────────────────────────────────────────────────┤
│  Quantity — stepper (min 1, max per creator policy)           │
├─────────────────────────────────────────────────────────────┤
│  Lead time / availability — "Requires 48-hour lead time"      │
│  Status badge — Available | Sold out | Limited                  │
├─────────────────────────────────────────────────────────────┤
│  Creator attribution — avatar, name, verification badge       │
│  Link to storefront                                           │
├─────────────────────────────────────────────────────────────┤
│  Special instructions — Textarea (optional, 200 char)           │
├─────────────────────────────────────────────────────────────┤
│  Sticky footer — price summary, Primary "Add to order"        │
└─────────────────────────────────────────────────────────────┘
```

### Information priority

1. Allergens and dietary badges
2. Price and availability
3. Description and ingredients
4. Variants and quantity
5. Creator trust attribution

---

## Components

| Component | Usage |
|-----------|-------|
| **Menu item card** (hero) | Large photo display |
| **Dietary badge** | Dietary classifications |
| **Verification badge** | Creator attribution row |
| **Status badge** | Availability state |
| **Radio** | Size / single-select variants |
| **Checkbox** | Add-on multi-select |
| **Textarea** | Special instructions |
| **Text input** (stepper) | Quantity selector |
| **Primary button** | "Add to order" (sticky footer) |
| **Secondary button** | "View cart" (post-add state) |
| **Ghost button** | "Back to menu" |
| **Creator avatar** | Attribution row |
| **Breadcrumbs** | Wayfinding |
| **Toast** (Success) | "Added to cart" with View cart action |
| **Toast** (Error) | Add failure |
| **Detail modal** (mobile alt) | Storefront may open this instead of full page on mobile — same content |

---

## Interactions

### Variants and pricing

- Selecting variant (Radio) updates price in sticky footer in real time
- Add-ons (Checkbox) adjust price incrementally; total always visible
- Required variant not selected → inline validation on "Add to order": "Select a size"
- Price displays item + add-ons + quantity; fees not shown until [Cart](cart.md)

### Quantity

- Stepper: − / + buttons and direct input
- Min: 1; Max: creator-defined or platform cap
- Exceeding max → inline message: "Maximum [N] per order for this item"

### Add to cart

- **Primary button** "Add to order" → POST cart → **Success toast** with "View cart" and "Continue browsing"
- Sold out → button disabled; **Status badge** "Sold out"
- Different creator in cart → **Confirmation modal**: "Your cart has items from [Other Creator]. Replace cart?" Confirm clears and adds

### Allergens

- Allergen block always expanded — never behind accordion in v1
- Tap allergen term → tooltip with FDA major allergen definition (educational, not legal advice)
- "No major allergens listed" still shows disclaimer: "Ingredients confirmed by creator. Cross-contact may occur."

### Special instructions

- Optional; placeholder: "Allergies, modifications, or notes for the creator"
- Allergy-related instructions show helper: "For severe allergies, confirm directly with the creator via order messages after purchase."

### Share

- Ghost share button in header → copy item URL

### Keyboard

- Variant radios: arrow key selection within group
- Sticky footer primary action always reachable via Tab
- Enter on page does not auto-submit (prevent accidental add)

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Price update | Number crossfade 150ms on variant change |
| Add to cart success | Button brief checkmark morph 200ms; toast slide-up |
| Photo load | Blur-up 300ms |
| Sticky footer | Slide-up into view when scrolling past fold on mobile |
| Quantity stepper | Subtle scale on tap 100ms |

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Full-bleed photo top; stacked content; sticky bottom CTA bar |
| **Tablet** | Photo 60% width top; side-by-side variants |
| **Desktop** | Split layout: photo left, all details right; sticky CTA in right column bottom |

Allergen block uses warning-tinted background token on all breakpoints — never minimized on mobile.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Full page | Photo skeleton (4:3) + text bars + variant skeleton |
| Variants | Radio skeleton group |
| Creator attribution | Avatar circle + name bar |

Item detail is a single API call — target < 300ms p95.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Item not found | "This item is no longer available." | **Primary button** "View [Creator] menu" |
| Item sold out (race) | Button disabled; message updated | Browse other items link |
| Add to cart API error | **Error toast**: "Couldn't add item. Try again." | Retry button in toast |
| Variant unavailable | Inline on affected option: "No longer available" | Auto-select next available |
| Creator suspended mid-session | Banner: "This creator is not accepting orders." | Disable add; link to [Search](search.md) |

---

## Empty States

Not applicable for primary item detail view. Edge cases:

| Scenario | Message |
|----------|---------|
| No ingredients provided by creator | "Ingredient list not provided. Contact creator with questions before ordering." |
| No allergens flagged | "No major allergens listed by creator. See disclaimer." — still show disclaimer |

---

## Permissions

| Capability | Guest | Authenticated |
|------------|-------|---------------|
| View item detail | ✓ | ✓ |
| Add to cart | ✓ | ✓ |
| Special instructions | ✓ | ✓ |

Item visible only if creator verified and item published. Unpublished items return 404.

---

## Analytics

| Event | Properties |
|-------|------------|
| `page_view` | `page: item_detail`, `creator_id`, `item_id` |
| `item_variant_selected` | `item_id`, `variant_id` |
| `item_addon_toggled` | `item_id`, `addon_id`, `selected` |
| `item_quantity_changed` | `item_id`, `quantity` |
| `item_add_to_cart` | `creator_id`, `item_id`, `quantity`, `variant_ids`, `addon_ids`, `price` |
| `item_add_failed` | `item_id`, `error_code` |
| `item_allergen_tooltip_opened` | `allergen` |
| `item_share` | `item_id` |

---

## Accessibility

- **Allergen block:** `role="region"` `aria-label="Allergen information"`; high contrast; not color-alone
- **Dietary badges:** Text labels always present, not icon-only
- **Variant radios:** `fieldset` + `legend` for each group
- **Quantity stepper:** `aria-label="Quantity"`; announce value changes via `aria-live="polite"`
- **Sticky CTA:** Does not trap focus; `aria-label="Add [item name] to order, total [price]"`
- **Photo:** `alt="[Item name] by [Creator name]"`
- **Price updates:** `aria-live="polite"` region announces new total

WCAG 2.2 AA — allergen information meets enhanced visibility requirements for safety content.

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | `{Item Name} — {Creator Name} | Marketplate` |
| `<meta name="description">` | Item description excerpt + dietary tags + creator name |
| Canonical | `/creator/:slug/item/:itemSlug` |
| Structured data | `Product` with `name`, `description`, `image`, `offers` (price), `brand` (creator) |

Item pages indexable when creator is verified and item is published.

---

## Future Improvements

- Nutritional information panel (calories, macros) for meal prep creators
- "Frequently bought together" suggestions
- Customer photos in reviews specific to this item
- Allergen filter highlight when arriving from [Search](search.md) dietary filter
- AR portion preview (long-term)
- Per-item pickup window availability

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/creators/:slug/items/:itemSlug` | GET | Full item detail |
| `/api/v1/cart/items` | POST | Add to cart |
| `/api/v1/cart/items/:lineId` | PATCH | Update quantity/variants (from edit flow) |

Item response fields (required):
- `id`, `slug`, `name`, `description`, `photos[]`, `price`, `variants[]`, `addons[]`
- `ingredients[]`, `allergens[]`, `dietary_tags[]`
- `lead_time_hours`, `availability_status`, `max_quantity`
- `creator` (id, slug, name, avatar, verification)
- `section_name` (for breadcrumb)

---

## Related Pages

- [Creator Storefront](creator-storefront.md) — Parent menu and creator context
- [Cart](cart.md) — Post-add destination
- [Checkout](checkout.md) — Allergen acknowledgment at payment
- [Search](search.md) — Item discovery entry
- [Help](help.md) — Allergen disclaimer and food safety FAQ
