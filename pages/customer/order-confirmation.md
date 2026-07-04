# Order Confirmation

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/orders/:orderId/confirmation`  
**Surface:** Customer marketplace (web + mobile)  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Order Confirmation page delivers immediate reassurance after payment — the order is real, the timing is clear, and next steps are obvious. It replaces anxiety with confidence before the customer navigates away.

This page exists to close the checkout loop with trust-forward clarity: order number, fulfillment details, creator verification, and a visible path to tracking via [Order Detail](order-detail.md).

---

## Goals

### User goals

- Confirm the order was placed successfully without doubt
- See pickup/delivery time, location, and creator contact at a glance
- Copy order number for reference
- Understand what happens next in the fulfillment timeline
- Navigate to order tracking or continue shopping

### Business goals

- Reduce post-purchase support contacts ("Did my order go through?")
- Drive immediate engagement with [Order Detail](order-detail.md) for tracking
- Reinforce trust with creator verification repeated post-purchase
- Prevent duplicate orders via history replace (no back to checkout)
- Measure confirmation → tracking click-through

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Moments after first or repeat purchase |
| **Secondary** | Gift order sender | May share confirmation details with recipient |
| **Anti-persona** | User attempting to re-submit checkout | Blocked by history replace |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| [Checkout](checkout.md) | Successful **Place order** — primary entry |
| Email confirmation link | Deep link with order token |
| Push notification tap | Post-order alert |
| Direct URL | Bookmark; requires auth + order ownership |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Order Detail](order-detail.md) | **Primary button** "View order" |
| [Home](home.md) | **Secondary button** "Continue shopping" |
| [Creator Storefront](creator-storefront.md) | Creator name link |
| [Help](help.md) | "Questions about your order?" link |
| Calendar add | External calendar app (pickup window) |

### Global chrome

- **Top nav bar:** Logo (→ [Home](home.md)), account menu
- **Tab bar (mobile):** Visible — Orders tab highlights active order context
- **No back to checkout:** Browser history replace on mount prevents duplicate submission

---

## Layout

### Content hierarchy (top to bottom)

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — logo, account                                │
├─────────────────────────────────────────────────────────────┤
│  Success header — checkmark icon, "Your order is confirmed" │
│  Subhead — "We've sent a confirmation to [email]"           │
├─────────────────────────────────────────────────────────────┤
│  Order number card — prominent, copyable                    │
│  "Order #MP-12345" · Copy button                            │
├─────────────────────────────────────────────────────────────┤
│  Fulfillment card — Order card (compact)                    │
│  Pickup/delivery window · location · directions link        │
│  Status badge — "Confirmed"                                 │
├─────────────────────────────────────────────────────────────┤
│  Creator card — avatar, name, verification badges           │
│  "Message creator" link (future: messaging thread)          │
├─────────────────────────────────────────────────────────────┤
│  What's next — vertical timeline (3–4 steps preview)        │
│  Confirmed → In production → Ready → Completed              │
├─────────────────────────────────────────────────────────────┤
│  Order summary — collapsible line items + total charged     │
├─────────────────────────────────────────────────────────────┤
│  Actions row                                                │
│  Primary "View order" · Secondary "Add to calendar"         │
│  Ghost "Continue shopping"                                  │
├─────────────────────────────────────────────────────────────┤
│  Help strip — "Questions?" link to Help with order context  │
└─────────────────────────────────────────────────────────────┘
```

### Grid

| Breakpoint | Layout |
|------------|--------|
| Mobile (320–767px) | Single column; sticky bottom "View order" CTA |
| Tablet (768–1023px) | Single column centered; max-width 640px |
| Desktop (1024px+) | Max-width 720px centered; two-column action row |

---

## Components

| Component | Usage on this page |
|-----------|-------------------|
| **Top nav bar** | Logo, account |
| **Tab bar (mobile)** | Bottom navigation |
| **Order card** (compact) | Fulfillment summary with window and location |
| **Status badge** | "Confirmed" initial state |
| **Creator avatar** | Creator attribution card |
| **Verification badge** | Creator card — Identity + Kitchen |
| **Primary button** | "View order" |
| **Secondary button** | "Add to calendar" |
| **Ghost button** | "Continue shopping", "Copy order number" |
| **Toast** (Success) | "Order number copied" |
| **Toast** (Info) | Calendar add instructions if native unsupported |

---

## Interactions

### Order number

- Display format: `Order #MP-{id}` — human-readable, support-reference friendly
- **Ghost button** "Copy" → clipboard → **Success toast** "Order number copied"
- Tap order number (mobile) → same copy behavior

### Fulfillment card

- Pickup: date/time window, address (full address post-purchase per policy), **Secondary button** "Get directions" → maps deep link
- Delivery: estimated window, address summary, delivery instructions if provided
- **Status badge** shows current state — "Confirmed" at confirmation time

### Creator card

- Creator name → [Creator Storefront](creator-storefront.md)
- Verification badge tap → tooltip with credential detail
- "Message creator" → order-scoped thread (future); v1 links to [Help](help.md) contact with order ID pre-filled

### What's next timeline

- Read-only preview of fulfillment states per [order fulfillment flow](../flows/order-fulfillment-flow.md)
- Current step highlighted; future steps muted
- Tap "View order" for live timeline on [Order Detail](order-detail.md)

### Order summary

- Collapsible on mobile — default collapsed showing total only
- Expand reveals line items with dietary badges and quantities
- Total shows amount charged (matches checkout review)

### Actions

- **Primary button** "View order" → [Order Detail](order-detail.md)
- **Secondary button** "Add to calendar" → `.ics` download or native calendar API for pickup window
- **Ghost button** "Continue shopping" → [Home](home.md)

### Browser navigation

- Back button from confirmation does NOT return to checkout — history replace
- Back navigates to pre-checkout origin (typically [Cart](cart.md) or [Creator Storefront](creator-storefront.md))

### Keyboard

- Tab order: skip link → nav → order number copy → fulfillment card → actions
- Enter on "View order" navigates to detail

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Page mount | Success checkmark draw 400ms; content fade-in 200ms stagger |
| Copy order number | Brief highlight flash on number 300ms |
| Timeline | Current step pulse once on mount (subtle) |
| Collapsible summary | Height transition 200ms ease-out |
| Reduced motion | Instant content display; static checkmark |

Calm celebration — no confetti or excessive motion per [voice and tone](../../brand/voice-and-tone.md).

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Sticky bottom "View order"; summary collapsed; calendar via share sheet |
| **Tablet** | Centered card layout; inline action buttons |
| **Desktop** | Wider fulfillment card; horizontal action row |

**Content parity:** Full address, verification badges, and timeline visible on all breakpoints.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Initial load | Success icon skeleton + 3 content card skeletons |
| Order fetch | Single API call — target < 400ms p95 |
| Calendar generate | **Secondary button** loading spinner on tap |
| Copy action | Instant — no loading state |

Confirmation page loads order by ID from URL — no client-side checkout state dependency.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Order not found | "We couldn't find this order." | **Primary button** "View order history" → [Order History](order-history.md) |
| Unauthorized (wrong user) | "This order belongs to another account." | **Primary button** "Go to orders" |
| Order still processing | "Your order is being processed." with spinner | Auto-refresh 3s; max 30s then **Primary button** "View order" |
| Partial data load | Render available sections; inline retry on failed card | **Ghost button** "Refresh" |
| Network offline | **Info toast**: "You're offline. Confirmation details may be incomplete." | Cached order if available |

Payment succeeded but order pending edge case: show reassuring processing state, never error tone.

---

## Empty States

Not applicable — confirmation requires valid order ID. Invalid ID handled in Error States.

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| View confirmation | ✗ | ✓ (order owner only) |
| Copy order number | ✓ (if authorized) | ✓ |
| Add to calendar | ✓ (if authorized) | ✓ |
| View full pickup address | ✓ (post-purchase) | ✓ |

Order ownership verified server-side. Email deep links include signed token for one-time access before login prompt.

---

## Analytics

### Page events

| Event | Properties |
|-------|------------|
| `page_view` | `page: order_confirmation`, `order_id`, `creator_id`, `total`, `fulfillment_type` |
| `confirmation_order_number_copied` | `order_id` |
| `confirmation_view_order_clicked` | `order_id` |
| `confirmation_calendar_added` | `order_id`, `method: ics | native` |
| `confirmation_continue_shopping` | `order_id` |
| `confirmation_creator_clicked` | `order_id`, `creator_id` |
| `confirmation_help_clicked` | `order_id` |

### Funnel metrics

- Confirmation → order detail CTR
- Time on confirmation page
- Calendar add rate (pickup orders)

→ [Customer Metrics](../../product/success-metrics-overview.md#customer-metrics)

---

## Accessibility

- **Landmark regions:** `banner` (nav), `main` (confirmation content)
- **Success header:** `role="status"` `aria-live="polite"` announces "Your order is confirmed" on load
- **Order number:** `aria-label="Order number MP-12345"`; copy button `aria-label="Copy order number"`
- **Fulfillment card:** `aria-label="Pickup on [date] at [time] from [location]"`
- **Timeline:** Ordered list with `aria-label="Order progress"`; current step `aria-current="step"`
- **Primary CTA:** Does not trap focus; first focusable after success announcement
- **Checkmark icon:** Decorative; confirmation conveyed in text
- **Color:** Success state not conveyed by green alone — text confirmation required

→ [Accessibility Standards](../../design-system/accessibility-standards.md)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Order Confirmed — #{orderId} | Marketplate |
| `<meta name="description">` | Your order from [Creator Name] is confirmed. |
| `robots` | `noindex, nofollow` |

Confirmation pages are not indexable.

---

## Future Improvements

- SMS opt-in for status updates on confirmation page
- Share order status link for gift recipients
- Estimated preparation start time from creator queue
- Review prompt scheduling preview ("You'll be invited to review after pickup")
- Print-friendly confirmation view
- Wallet pass for pickup (Apple Wallet / Google Wallet)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/customers/me/orders/:orderId/confirmation` | GET | Confirmation payload: order, fulfillment, creator, timeline preview |
| `/api/v1/customers/me/orders/:orderId/calendar` | GET | `.ics` file for pickup window |

Response includes:
- `order` (id, number, status, total_charged, created_at, lines[])
- `fulfillment` (type, window_start, window_end, location, instructions)
- `creator` (id, slug, name, avatar, verification, contact_policy)
- `timeline_preview[]` (status, label, completed, estimated_at)
- `customer_email` (masked for display)

---

## Related Pages

- [Checkout](checkout.md) — Predecessor in purchase flow
- [Order Detail](order-detail.md) — Live tracking destination
- [Order History](order-history.md) — All orders list
- [Creator Storefront](creator-storefront.md) — Creator context
- [Home](home.md) — Continue shopping
- [Help](help.md) — Post-purchase support
