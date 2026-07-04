# Customer Checkout

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/checkout`  
**Query params:** `step` (optional deep-link: `fulfillment`, `details`, `payment`, `review`)  
**Surface:** Customer marketplace (web + mobile)  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Checkout page completes the purchase with full transparency before payment — fulfillment confirmed, contact details verified, policies acknowledged, and price breakdown visible. No surprise fees, no hidden allergen acknowledgments, no ambiguous totals.

This page embodies Marketplate's trust thesis at the moment of commitment: customers know exactly who they are buying from, what they are paying, and what happens next before tapping **Place order**.

---

## Goals

### User goals

- Select fulfillment method and time window that fits their schedule
- Confirm contact information and order notes (especially allergy restatements)
- Enter payment securely with clear total before authorization
- Review complete itemized summary with creator verification repeated
- Place order with confidence and receive immediate confirmation

### Business goals

- Maximize checkout → order placed conversion
- Enforce capacity, lead time, and fulfillment validation server-side
- Capture explicit allergen and policy acknowledgments for trust audit trail
- Minimize payment failures through clear error recovery
- Measure step-level drop-off and validation failure reasons

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Final purchase decision |
| **Secondary** | First-time buyer | May need auth redirect from guest cart |
| **Anti-persona** | Guest expecting anonymous checkout | Auth required in v1 |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| [Cart](cart.md) | **Primary button** "Continue to checkout" |
| Auth redirect | Login/signup with return URL `/checkout` |
| Abandoned checkout recovery | Email link with saved session (72h) |
| Direct URL | Blocked if cart empty → redirect to [Cart](cart.md) |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Order Confirmation](order-confirmation.md) | Successful **Place order** |
| [Cart](cart.md) | Back from step 1; "Edit cart" link on review step |
| [Creator Storefront](creator-storefront.md) | Creator name in summary sidebar |
| [Menu Item Detail](menu-item-detail.md) | Item name in summary (opens read-only modal on mobile) |
| [Help](help.md) | Policy links, allergen FAQ, payment security |
| [Account Settings](account-settings.md) | "Add address" during delivery step |

### Global chrome

- **Top nav bar:** Minimal — logo (→ [Home](home.md)), secure checkout lock icon, help link
- **Tab bar (mobile):** Hidden during checkout — focused flow per [navigation model](../navigation-model.md)
- **Step indicator:** Horizontal progress — Fulfillment → Details → Payment → Review

---

## Layout

### Content hierarchy

```
┌─────────────────────────────────────────────────────────────┐
│  Minimal top nav — logo, "Secure checkout", Help            │
├─────────────────────────────────────────────────────────────┤
│  Step indicator — 1 Fulfillment · 2 Details · 3 Payment ·   │
│  4 Review (current step highlighted)                          │
├─────────────────────────────────────────────────────────────┤
│  Main column (left / full mobile)                           │
│  ┌─ Step content ─────────────────────────────────────────┐  │
│  │  Step-specific forms and selections                   │  │
│  └───────────────────────────────────────────────────────┘  │
│  Step navigation — Back (ghost) · Continue (primary)        │
├─────────────────────────────────────────────────────────────┤
│  Order summary sidebar (desktop) / collapsible (mobile)     │
│  Creator row — avatar, name, verification badges            │
│  Line items (compact) · Edit cart link                      │
│  Price breakdown — subtotal, fees, tax, total               │
│  Trust strip — verification + policy summary                │
└─────────────────────────────────────────────────────────────┘
```

### Step layouts

#### Step 1 — Fulfillment

```
Fulfillment method — Radio: Pickup | Delivery (creator-supported)
Pickup: Date/time picker — available windows from creator
Delivery: Address select/add · zone validation message
Lead time reminder — "Requires 48-hour notice"
Fulfillment instructions preview (read-only)
```

#### Step 2 — Details

```
Contact — name, phone, email (pre-filled from account)
Order notes — Textarea (optional)
Allergy restatement — Textarea with helper (prominent if cart has allergens)
Gift/message — Textarea (if creator supports)
```

#### Step 3 — Payment

```
Saved payment methods — Radio (authenticated)
New card — Stripe Elements embedded form
Billing address — if required
Authorization note — "Charged when order is confirmed by creator"
```

#### Step 4 — Review

```
Full itemized list with allergens highlighted
Fulfillment summary
Contact summary
Price breakdown (expanded, no collapse)
Policy checkboxes — cancellation, allergen acknowledgment (required)
Primary "Place order" — sole filled button on screen
```

### Grid

| Breakpoint | Layout |
|------------|--------|
| Mobile (320–767px) | Single column; collapsible order summary accordion at top |
| Tablet (768–1023px) | Single column; summary sticky bottom bar with total |
| Desktop (1024px+) | 60/40 split — steps left, sticky summary right; max-width 1100px |

---

## Components

| Component | Usage on this page |
|-----------|-------------------|
| **Top nav bar** (minimal) | Logo, secure indicator, Help link |
| **Segmented control** | Step indicator (non-interactive in v1 — linear flow) |
| **Radio** | Fulfillment method; saved payment method |
| **Select / dropdown** | Pickup window selection |
| **Date / time picker** | Pickup scheduling |
| **Text input** | Contact fields |
| **Textarea** | Order notes, allergy restatement, gift message |
| **Checkbox** | Required policy and allergen acknowledgments |
| **Primary button** | "Continue" (steps 1–3); "Place order" (step 4) |
| **Secondary button** | "Edit cart" |
| **Ghost button** | "Back" between steps |
| **Creator avatar** | Summary sidebar creator row |
| **Verification badge** | Creator row + trust strip |
| **Dietary badge** | Allergen flags on line items in review |
| **Status badge** | Window availability in fulfillment step |
| **Confirmation modal** | Leave checkout with unsaved changes |
| **Toast** (Error) | Payment failure, validation errors |
| **Toast** (Warning) | Capacity near limit |
| **Toast** (Info) | Session restored from abandoned checkout |

---

## Interactions

### Step navigation

- Linear flow in v1 — cannot skip steps via indicator tap
- **Ghost button** "Back" preserves entered data; back from step 1 → [Cart](cart.md)
- **Primary button** "Continue" validates current step server-side before advance
- Browser back: **Confirmation modal** if step data entered — "Leave checkout?"
- URL updates `?step=` for bookmarking within session (not shareable)

### Step 1 — Fulfillment

- Fulfillment **Radio** options filtered to creator-supported types
- Pickup **Date / time picker** shows only available windows; unavailable slots disabled with tooltip
- Delivery: address from account or inline add → link to [Account Settings](account-settings.md) for full address book
- Zone validation inline: "Delivery not available to this address" with nearest pickup suggestion
- Capacity exceeded → block continue; **Warning toast** with explanation

### Step 2 — Details

- Pre-fill from account; phone required for order notifications
- Allergy **Textarea** auto-populated from line item special instructions; editable
- Helper: "Restate severe allergies here. Creator will see this before preparing your order."

### Step 3 — Payment

- Stripe Elements for card entry — PCI scope externalized
- Saved methods for authenticated users; default pre-selected
- Payment authorization on **Place order**, not on Continue
- Inline error on decline: remain on payment step with specific message (insufficient funds, expired card)

### Step 4 — Review

- Allergen acknowledgment **Checkbox** required when cart contains flagged allergens — cannot proceed unchecked
- Cancellation policy **Checkbox** required — links to [Help](help.md#cancellations)
- **Primary button** "Place order" → POST order → loading state "Placing your order…" → [Order Confirmation](order-confirmation.md) on success
- History replace on success — prevents duplicate submission on back navigation

### Order summary sidebar

- Collapsible on mobile — default collapsed showing total only; expand for line items
- **Secondary button** "Edit cart" → [Cart](cart.md) with checkout state preserved 72h
- Creator verification badges always visible in summary

### Keyboard

- Step forms: logical tab order; Enter submits current step (not Place order until step 4)
- Checkbox groups: Space toggles; error summary at step top on validation fail
- Focus trap within Stripe Elements per Stripe accessibility guidance

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Step advance | Content slide-left 250ms; step indicator fill 200ms |
| Step back | Content slide-right 250ms |
| Validation error | Step content subtle shake 100ms; focus first error |
| Place order loading | Button spinner; disable form 400ms minimum for perceived confidence |
| Summary expand (mobile) | Accordion height 200ms ease-out |
| Success redirect | Brief checkmark on button 300ms before navigation |

Respect `prefers-reduced-motion`: instant step swap, no slide.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Summary accordion at top; full-width forms; sticky bottom bar with Continue/Place order |
| **Tablet** | Summary below step content; sticky total bar |
| **Desktop** | Persistent sidebar summary; step content max-width 560px |

**Content parity:** Allergen acknowledgment, policy checkboxes, and full price breakdown required on all breakpoints — never deferred to "fine print."

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Initial load | Step 1 skeleton + summary skeleton |
| Pickup windows | **Date / time picker** skeleton until availability API resolves |
| Step validation | Primary button loading; fields disabled |
| Place order | Full-step overlay spinner; "Placing your order…" |
| Payment Element | Stripe loading shimmer in card region |
| Address validation | Inline spinner on delivery address blur |

Checkout session restored from server on mount — cart, fulfillment selections, and contact pre-populated.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Empty cart on load | Redirect to [Cart](cart.md) with **Info toast** | — |
| Cart changed since session | Banner: "Your cart was updated." | Review summary; re-validate |
| Payment declined | Inline below payment form: specific decline reason | Update card; retry Place order |
| Capacity exceeded at submit | Return to step 1 with banner explanation | Select new window |
| Creator closed mid-checkout | Block Place order: "Creator not accepting orders." | **Secondary button** "Return to cart" |
| Fulfillment window expired | Step 1 banner: "Selected window expired." | Re-select window |
| Session expired (auth) | Redirect login with return URL; preserve checkout draft 72h | Re-auth and resume |
| Network failure on Place order | **Error toast**: "Connection lost. Your payment was not processed." | Retry Place order |
| Stripe Elements load failure | Inline error: "Payment form unavailable." | **Secondary button** "Try again" |

Critical payment errors use inline errors, not toast alone — user must see recovery path.

---

## Empty States

Not applicable — checkout requires non-empty cart. Edge case:

| Scenario | Message | Action |
|----------|---------|--------|
| All items became unavailable | "Items in your cart are no longer available." | **Primary button** "Return to cart" |

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| Access checkout | ✗ (redirect to login) | ✓ |
| Saved addresses | ✗ | ✓ |
| Saved payment methods | ✗ | ✓ |
| Place order | ✗ | ✓ |
| Guest cart preserved through login | ✓ (merge on auth) | — |

Auth gate enforced at checkout entry per [customer purchase flow](../flows/customer-purchase-flow.md#authentication-gates). Login preserves cart and restores checkout step.

---

## Analytics

### Page events

| Event | Properties |
|-------|------------|
| `page_view` | `page: checkout`, `step`, `creator_id`, `cart_value` |
| `checkout_step_completed` | `step`, `fulfillment_type`, `duration_ms` |
| `checkout_step_back` | `from_step` |
| `checkout_fulfillment_selected` | `type`, `window_id` |
| `checkout_payment_method_selected` | `method: saved | new` |
| `checkout_policy_acknowledged` | `policy_type` |
| `checkout_allergen_acknowledged` | `allergen_count` |
| `checkout_place_order_clicked` | `cart_value`, `item_count` |
| `checkout_order_placed` | `order_id`, `total`, `fulfillment_type` |
| `checkout_failed` | `step`, `error_code` |
| `checkout_abandoned` | `last_step`, `duration_ms` |

### Funnel metrics

- Step 1 → 4 completion rate
- Payment decline rate
- Time per step
- Abandonment by step

→ [Customer Metrics](../../product/success-metrics-overview.md#customer-metrics)

---

## Accessibility

- **Landmark regions:** `banner` (minimal nav), `main` (step content), `complementary` (order summary)
- **Step indicator:** `nav` with `aria-label="Checkout progress"`; current step `aria-current="step"`
- **Forms:** Each step wrapped in `form` with `aria-labelledby` pointing to step heading
- **Errors:** `role="alert"` summary at step top listing all field errors; `aria-invalid` on fields
- **Allergen checkbox:** `aria-describedby` linking to allergen list in review
- **Place order:** `aria-label="Place order, total [amount] from [creator name]"`
- **Secure checkout:** Lock icon decorative; text "Secure checkout" visible
- **Price updates:** `aria-live="polite"` on total in summary
- **Stripe Elements:** Stripe-provided labels; ensure sufficient color contrast per [accessibility standards](../../design-system/accessibility-standards.md)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Checkout | Marketplate |
| `<meta name="description">` | Complete your order from verified local food creators. |
| `robots` | `noindex, nofollow` |

Checkout is not indexable.

---

## Future Improvements

- Apple Pay / Google Pay express checkout
- Tip option (creator-configurable)
- Schedule recurring orders (meal prep)
- Multi-step progress save with shareable resume link
- Delivery tracking integration at checkout opt-in
- Corporate/expense receipt email field

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/checkout/session` | GET | Restore checkout state: cart, saved selections |
| `/api/v1/checkout/session` | PATCH | Save step progress (fulfillment, details) |
| `/api/v1/checkout/fulfillment-options` | GET | Available windows; params: `creator_id`, `cart_id` |
| `/api/v1/checkout/validate-delivery` | POST | Address zone validation |
| `/api/v1/checkout/orders` | POST | Place order; body: fulfillment, contact, payment_method, acknowledgments |
| `/api/v1/customers/me/addresses` | GET | Delivery address list |
| `/api/v1/customers/me/payment-methods` | GET | Saved cards (auth) |

Place order request requires:
- `cart_id`, `fulfillment` (type, window_id or address_id), `contact`, `payment_method_id` or Stripe token
- `acknowledgments` (cancellation: true, allergens: true when applicable)
- `order_notes`, `allergy_restatement`

Response: `order_id`, `confirmation_url`, `payment_status`

Authorization model per [marketplace mechanics](../../product/marketplace-mechanics.md#transactions) — capture timing varies by fulfillment model.

---

## Related Pages

- [Cart](cart.md) — Pre-checkout review and edit
- [Order Confirmation](order-confirmation.md) — Post-purchase reassurance
- [Menu Item Detail](menu-item-detail.md) — Allergen source data
- [Creator Storefront](creator-storefront.md) — Creator context and policies
- [Account Settings](account-settings.md) — Addresses and contact defaults
- [Help](help.md) — Cancellation, allergen, and payment FAQs
- [Home](home.md) — Exit via logo
