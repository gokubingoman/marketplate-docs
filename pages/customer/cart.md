# Customer Cart

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/cart`  
**Surface:** Customer marketplace (web + mobile)  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Cart page is where customers review and validate their order before committing to checkout. It consolidates line items from a single verified creator, surfaces pricing and fulfillment constraints early, and flags availability issues before payment.

This page exists to prevent surprise at checkout — customers see subtotal, fees, lead times, and creator trust signals in one calm review surface before proceeding to [Checkout](checkout.md).

---

## Goals

### User goals

- Review all items, variants, and special instructions before paying
- Adjust quantities or remove items without losing context
- Understand estimated total, fees, and fulfillment requirements
- Return to [Creator Storefront](creator-storefront.md) or [Menu Item Detail](menu-item-detail.md) to add or edit items
- Proceed to checkout only when the cart is valid and complete

### Business goals

- Maximize cart → checkout conversion with transparent pricing
- Enforce single-creator cart and minimum order rules before checkout
- Surface expired pickup windows and sold-out items before payment attempt
- Reduce checkout abandonment from hidden fees or fulfillment mismatches
- Measure cart edit patterns and drop-off points

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Validating order before payment |
| **Secondary** | Returning customer reordering | May arrive with pre-populated cart from [Order History](order-history.md) |
| **Anti-persona** | Multi-creator comparison shopper | v1 single-creator cart — must choose one creator per order |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| [Creator Storefront](creator-storefront.md) | Floating cart bar, nav cart icon |
| [Menu Item Detail](menu-item-detail.md) | "View cart" after add; edit item return |
| [Home](home.md), [Search](search.md), [Browse](browse.md) | Nav cart icon |
| [Order History](order-history.md) | Reorder pre-populates cart |
| Direct URL | Bookmark or return visit |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Checkout](checkout.md) | **Primary button** "Continue to checkout" (auth gate if guest) |
| [Creator Storefront](creator-storefront.md) | Creator name link, "Continue shopping" |
| [Menu Item Detail](menu-item-detail.md) | Line item tap, "Edit item" |
| [Home](home.md) | Logo tap, empty cart CTA |
| [Browse](browse.md) | Empty cart "Browse creators" |
| [Help](help.md) | Fee or policy explainer link |

### Global chrome

- **Top nav bar:** Logo, search, cart (active state with count), account menu
- **Tab bar (mobile):** Visible — cart is not a tab; nav cart icon reflects count
- Checkout flow hides tab bar — cart is pre-checkout surface

---

## Layout

### Content hierarchy (top to bottom)

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — logo, search, cart (active), account         │
├─────────────────────────────────────────────────────────────┤
│  Page header — "Your order" (h1)                            │
├─────────────────────────────────────────────────────────────┤
│  Creator header row                                         │
│  Avatar, name, verification badges, link to storefront      │
├─────────────────────────────────────────────────────────────┤
│  Trust strip — "Ordering from verified creator · [Kitchen]"   │
├─────────────────────────────────────────────────────────────┤
│  Line items (stacked)                                       │
│  ┌─ Line item card ──────────────────────────────────────┐  │
│  │  Photo, name, variant summary, dietary badges         │  │
│  │  Special instructions (truncated)                     │  │
│  │  Quantity stepper · line price · Remove (ghost)       │  │
│  │  Warning inline if availability issue                 │  │
│  └───────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│  Fulfillment preview — pickup/delivery summary (read-only)  │
│  "Select fulfillment at checkout" helper                    │
├─────────────────────────────────────────────────────────────┤
│  Order summary (sticky on mobile)                           │
│  Subtotal · Service fee · Tax estimate · Total              │
│  Minimum order progress bar (if applicable)                 │
├─────────────────────────────────────────────────────────────┤
│  Primary "Continue to checkout" · Secondary "Continue       │
│  shopping"                                                  │
├─────────────────────────────────────────────────────────────┤
│  Policies strip — cancellation summary link to Help         │
└─────────────────────────────────────────────────────────────┘
```

### Grid

| Breakpoint | Layout |
|------------|--------|
| Mobile (320–767px) | Single column; sticky bottom summary bar with CTA |
| Tablet (768–1023px) | Single column; summary card below items |
| Desktop (1024px+) | Max-width 720px centered; summary card sticky right column (2-col: items 60%, summary 40%) |

---

## Components

| Component | Usage on this page |
|-----------|-------------------|
| **Top nav bar** | Global navigation; cart icon active |
| **Creator avatar** | Creator header row |
| **Verification badge** | Creator header — Identity + Kitchen |
| **Dietary badge** | Line item dietary tags |
| **Status badge** | Availability warnings — "Sold out", "Window expired" |
| **Menu item card** (compact) | Line item display with photo and metadata |
| **Text input** (stepper) | Quantity adjustment per line |
| **Primary button** | "Continue to checkout" |
| **Secondary button** | "Continue shopping" → storefront |
| **Ghost button** | "Remove" per line item; "Edit item" |
| **Confirmation modal** | Remove item confirm; replace cart on creator conflict |
| **Toast** (Success) | Quantity updated |
| **Toast** (Error) | Update failure |
| **Toast** (Warning) | Minimum order not met, availability flag |
| **Toast** (Info) | Cart merged after login |

---

## Interactions

### Line items

- Tap item name or photo → [Menu Item Detail](menu-item-detail.md) with edit context
- **Ghost button** "Edit item" → same destination with line ID for PATCH
- Quantity stepper → PATCH `/api/v1/cart/items/:lineId`; debounced 300ms on rapid taps
- **Ghost button** "Remove" → **Confirmation modal** if item has special instructions; else immediate remove with undo **Success toast** (5s)
- Sold-out or expired line → **Status badge** + inline message; checkout CTA disabled until resolved

### Creator header

- Creator name tap → [Creator Storefront](creator-storefront.md)
- Verification badge tap → tooltip explaining credential scope per [naming conventions](../../brand/naming-conventions.md#verification--trust-labels)

### Order summary

- Subtotal, service fee, tax estimate, and total update in real time on quantity change
- Minimum order: progress indicator shows "$X more to reach minimum" until met
- Fee line tap → inline expand with fee breakdown; link to [Help](help.md#fees)

### Checkout CTA

- **Primary button** "Continue to checkout" → validate cart server-side → auth gate if guest (return URL `/checkout`) → [Checkout](checkout.md)
- Disabled when: empty cart, validation errors, minimum not met, creator not accepting orders
- Guest checkout not supported in v1 — login required at checkout per [customer purchase flow](../flows/customer-purchase-flow.md#authentication-gates)

### Continue shopping

- **Secondary button** → [Creator Storefront](creator-storefront.md) for cart creator

### Keyboard

- Tab order: skip link → nav → line items (quantity before remove) → summary → primary CTA
- Enter on focused line item opens item detail
- Delete on focused remove button triggers confirmation flow

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Page load | Line items stagger fade-in 50ms offset; respects `prefers-reduced-motion` |
| Quantity change | Line price crossfade 150ms |
| Item remove | Collapse height 200ms ease-out; undo toast slide-up |
| Summary update | Total number crossfade 150ms |
| Sticky summary (mobile) | Slide-up into view when scrolling past first line item |
| Validation error | Inline shake 100ms on blocked checkout tap |

No auto-refresh animations — availability re-validated on focus and checkout tap.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Sticky bottom bar: total + primary CTA; line items full-width; creator header compact |
| **Tablet** | Summary card below items; sticky CTA in summary |
| **Desktop** | Two-column layout; summary sticky in viewport; wider line item photos |

**Content parity:** Allergen summary per line, verification badges, and fee breakdown visible on all breakpoints — never collapsed behind accordion on mobile.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Initial page | Full-page skeleton: creator header bars + 3 line item skeletons + summary skeleton |
| Quantity update | Inline spinner on affected line; other lines remain interactive |
| Remove item | Line opacity 50% until confirmed |
| Checkout validation | Primary button loading state; label "Checking availability…" |
| Reorder populate | Full-page skeleton while cart rebuilds from order |

Cart data fetched on mount; optimistic UI for quantity with rollback on error.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Cart load failure | "We couldn't load your cart." | **Primary button** "Try again" |
| Item update failure | **Error toast**: "Couldn't update quantity. Try again." | Retry in toast |
| Item no longer available | **Status badge** on line + banner: "Some items need attention." | Remove or edit links |
| Creator suspended | Banner: "This creator is not accepting orders." | **Secondary button** "Find other creators" → [Search](search.md) |
| Minimum order not met | **Warning toast** + disabled checkout with inline helper | Add items link to storefront |
| Pickup window expired | Inline on fulfillment preview: "Selected window no longer available." | Proceed to checkout to re-select |
| Network offline | **Info toast**: "You're offline. Cart changes will sync when reconnected." | Queue updates locally |
| Auth merge conflict | **Confirmation modal**: "Your saved cart differs. Keep which?" | Choose session or account cart |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| Empty cart | "Your cart is empty." | **Primary button** "Browse creators" → [Browse](browse.md) |
| Empty after last remove | Same as above; brief empty animation | **Secondary button** "Search" → [Search](search.md) |
| Reorder failed (all unavailable) | "These items aren't available right now." | **Primary button** "View creator menu" → [Creator Storefront](creator-storefront.md) |

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| View cart | ✓ (session) | ✓ (persisted) |
| Edit quantities / remove | ✓ | ✓ |
| Proceed to checkout | ✗ (auth required) | ✓ |
| Reorder from history | ✗ | ✓ |
| Cart persistence | Session + 7-day cookie | Account-linked |

Single-creator rule enforced in v1 per [marketplace mechanics](../../product/marketplace-mechanics.md#transactions). Adding from different creator triggers replace-cart flow on source page, not on cart.

---

## Analytics

### Page events

| Event | Properties |
|-------|------------|
| `page_view` | `page: cart`, `creator_id`, `item_count`, `cart_value` |
| `cart_item_quantity_changed` | `line_id`, `item_id`, `old_qty`, `new_qty` |
| `cart_item_removed` | `item_id`, `had_special_instructions` |
| `cart_item_edit_clicked` | `item_id` |
| `cart_checkout_started` | `creator_id`, `item_count`, `subtotal`, `validation_passed` |
| `cart_checkout_blocked` | `reason: minimum | availability | creator_closed` |
| `cart_continue_shopping` | `creator_id` |
| `cart_empty_viewed` | `referrer` |

### Funnel metrics

- Cart → checkout start rate
- Cart abandonment rate (exit without checkout)
- Average items per cart
- Validation failure rate by reason

→ [Customer Metrics](../../product/success-metrics-overview.md#customer-metrics)

---

## Accessibility

- **Landmark regions:** `banner` (nav), `main` (cart content), `contentinfo` (policies strip)
- **Skip link:** "Skip to order summary"
- **Page title (document):** `Your cart — Marketplate`
- **Line items:** `ul` / `li` structure; each item `aria-label="[quantity] × [item name], [price]"`
- **Quantity stepper:** `aria-label="Quantity for [item name]"`; value changes announced via `aria-live="polite"`
- **Remove action:** `aria-label="Remove [item name] from cart"`
- **Order summary:** `aria-label="Order summary"`; total updates in live region
- **Checkout CTA disabled:** `aria-disabled="true"` with `aria-describedby` explaining reason
- **Minimum order progress:** Progressbar role with `aria-valuenow`, `aria-valuemax`
- **Touch targets:** Minimum 44×44px on stepper and remove controls

→ [Accessibility Standards](../../design-system/accessibility-standards.md)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Your Cart | Marketplate |
| `<meta name="description">` | Review your order from verified local food creators before checkout. |
| Canonical | `https://marketplate.com/cart` |
| `robots` | `noindex, nofollow` — session-specific content |

Cart is not indexable.

---

## Future Improvements

- Multi-creator cart with creator-grouped checkout (deferred)
- Save cart for later (authenticated)
- Suggested add-ons based on cart contents
- Promo code entry
- Estimated pickup window preview before checkout
- Share cart link for group orders (catering)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/cart` | GET | Full cart: creator, lines, pricing, validation flags |
| `/api/v1/cart/items/:lineId` | PATCH | Update quantity |
| `/api/v1/cart/items/:lineId` | DELETE | Remove line |
| `/api/v1/cart/validate` | POST | Pre-checkout validation: availability, minimum, creator status |
| `/api/v1/cart/reorder` | POST | Populate from order ID (auth) |

Cart response includes:
- `creator` (id, slug, name, avatar, verification, minimum_order, accepting_orders)
- `lines[]` (id, item_id, slug, name, photo, variants, addons, quantity, unit_price, line_total, special_instructions, availability_status, allergens[])
- `pricing` (subtotal, service_fee, tax_estimate, total)
- `validation` (errors[], warnings[], minimum_order_progress)

---

## Related Pages

- [Creator Storefront](creator-storefront.md) — Add items and continue shopping
- [Menu Item Detail](menu-item-detail.md) — Edit line items
- [Checkout](checkout.md) — Next step in purchase flow
- [Order History](order-history.md) — Reorder entry
- [Home](home.md) — Discovery after empty cart
- [Browse](browse.md) — Empty cart destination
- [Help](help.md) — Fees, cancellation, and allergen policy
