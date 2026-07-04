# Order Detail

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/orders/:orderId`  
**Surface:** Customer marketplace (web + mobile)  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Order Detail page is the customer's single source of truth post-purchase — live status, fulfillment instructions, item summary, payment record, and support paths in one view. It reduces uncertainty between order placement and completion.

Customers must always know: *Where is my order? When do I pick it up or receive delivery? Who do I contact? Can I cancel?*

---

## Goals

### User goals

- Monitor order status in real time with a clear timeline
- Access pickup location, directions, and time window when ready
- Review items ordered, allergens, and special instructions
- Contact creator or support when something goes wrong
- Cancel within policy window when permitted
- Reorder when the experience was positive

### Business goals

- Minimize "where is my order?" support volume
- Drive reorder via [Cart](cart.md) pre-population
- Capture review submissions post-completion
- Surface trust signals (verification, verified purchase context) throughout post-purchase
- Measure status page engagement and cancel/help rates

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Active order tracking |
| **Secondary** | Returning customer | Reorder and review paths |
| **Anti-persona** | Non-owner attempting to view order | Blocked — ownership required |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| [Order Confirmation](order-confirmation.md) | **Primary button** "View order" |
| [Order History](order-history.md) | Order card tap |
| [Home](home.md) | Active order banner |
| Email / push notification | Status update deep link |
| Tab bar "Orders" (mobile) | Active order shortcut |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Order History](order-history.md) | Back, breadcrumb |
| [Creator Storefront](creator-storefront.md) | Creator name link, reorder unavailable items |
| [Cart](cart.md) | **Secondary button** "Order again" |
| [Help](help.md) | "Get help with this order" with order context |
| [Home](home.md) | Logo tap |
| Maps app | "Get directions" external link |

### Breadcrumbs

`Orders > Order #MP-{id}`

---

## Layout

### Content hierarchy (top to bottom)

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — back, logo, account                          │
├─────────────────────────────────────────────────────────────┤
│  Breadcrumbs — Orders > Order #MP-12345                     │
├─────────────────────────────────────────────────────────────┤
│  Header — Order #MP-12345 · Status badge · Placed [date]    │
├─────────────────────────────────────────────────────────────┤
│  Status timeline — vertical, live-updating                  │
│  Confirmed → In production → Ready → Completed              │
│  (Cancelled / Refunded branch when applicable)              │
├─────────────────────────────────────────────────────────────┤
│  Fulfillment card — Order card (expanded)                   │
│  Window, location, directions, delivery tracking (if any)   │
│  Primary action contextual — "Get directions" | "Track"     │
├─────────────────────────────────────────────────────────────┤
│  Creator card — avatar, verification, message link          │
├─────────────────────────────────────────────────────────────┤
│  Items — line list with allergens, instructions               │
├─────────────────────────────────────────────────────────────┤
│  Payment summary — subtotal, fees, tax, total, method       │
├─────────────────────────────────────────────────────────────┤
│  Actions — Order again · Get help · Cancel (if allowed)       │
├─────────────────────────────────────────────────────────────┤
│  Review prompt (completed orders) — star rating entry         │
└─────────────────────────────────────────────────────────────┘
```

### Status timeline (customer-visible)

| Status | Customer sees | Visual |
|--------|---------------|--------|
| Confirmed | Order accepted; ETA shown | Active step |
| In production | Being prepared | Active step |
| Ready | Ready for pickup / out for delivery | Active + **Primary button** CTA |
| In fulfillment | Handoff in progress | Active (delivery) |
| Completed | Order fulfilled | Final step; review prompt |
| Cancelled | Reason displayed | Struck timeline; **Status badge** |
| Refunded | Refund status and amount | Appended to cancelled branch |

Timeline updates near-real-time when creator advances status per [order fulfillment flow](../flows/order-fulfillment-flow.md).

### Grid

| Breakpoint | Layout |
|------------|--------|
| Mobile (320–767px) | Single column; sticky contextual CTA when Ready |
| Tablet (768–1023px) | Single column; max-width 720px |
| Desktop (1024px+) | Max-width 800px; timeline left 40%, details right 60% on wide screens |

---

## Components

| Component | Usage on this page |
|-----------|-------------------|
| **Top nav bar** | Back, logo, account |
| **Tab bar (mobile)** | Orders tab context |
| **Breadcrumbs** | Orders > current order |
| **Order card** (expanded) | Fulfillment details and actions |
| **Status badge** | Header and timeline step states |
| **Creator avatar** | Creator attribution |
| **Verification badge** | Creator card |
| **Dietary badge** | Line item allergen/dietary flags |
| **Review card** (inline prompt) | Post-completion review entry |
| **Primary button** | Contextual — "Get directions", "Track delivery" |
| **Secondary button** | "Order again" |
| **Ghost button** | "Get help", "Copy order number" |
| **Destructive button** | "Cancel order" (when policy allows) |
| **Confirmation modal** | Cancel order confirm |
| **Toast** (Success) | Status update received, cancel submitted |
| **Toast** (Info) | Real-time connection status |

---

## Interactions

### Status timeline

- Read-only visual — customers cannot advance status
- New status → step animates to active; `aria-live` announces change
- Push/email notifications link to this page with status anchor
- Cancelled: timeline grays future steps; reason displayed inline

### Fulfillment card

- Pickup Ready: **Primary button** "Get directions" → maps with full address
- Delivery In fulfillment: **Primary button** "Track delivery" → tracking URL if available
- Window countdown shown when within 24h of pickup
- Add to calendar available until order completed

### Creator card

- Creator name → [Creator Storefront](creator-storefront.md)
- Verification badge → tooltip
- "Message creator" → order thread (future); v1 → [Help](help.md) with order context

### Items section

- Read-only line list — no edit post-purchase
- Allergens highlighted with **Dietary badge** styling
- Special instructions displayed in full

### Actions

- **Secondary button** "Order again" → POST reorder → [Cart](cart.md) with availability validation
- **Ghost button** "Get help" → [Help](help.md)?order={id}
- **Destructive button** "Cancel order" → **Confirmation modal** with policy summary → POST cancel
- Cancel availability per [marketplace mechanics](../../product/marketplace-mechanics.md#cancellations-and-refunds) — hidden when not allowed

### Review prompt

- Appears when status = Completed and within review window (default 14 days)
- Star rating + optional text inline; submit → **Success toast**
- Verified purchase label shown
- Dismissible — single reminder at day 7 via notification, not on-page nagging

### Real-time updates

- WebSocket or polling (30s) for status changes while page open
- **Info toast** on reconnect after offline: "Order status updated"

### Keyboard

- Tab through timeline (informational), fulfillment actions, item list, action buttons
- Cancel modal: focus trap per [modals spec](../../design-system/components/modals.md)

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Status change | New timeline step scale-in 200ms; previous step checkmark |
| Ready state | Subtle pulse on **Primary button** once |
| Cancel confirm | Modal fade-in 200ms |
| Reorder loading | **Secondary button** spinner |
| Review submit | Star fill animation 150ms per star |
| Page refresh (poll) | No layout shift — inline status update only |

Respect `prefers-reduced-motion`: instant status swap.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Sticky bottom bar when Ready — directions/tracking CTA; timeline compact |
| **Tablet** | Full timeline with labels |
| **Desktop** | Side-by-side timeline and details on wide screens |

**Content parity:** Full pickup address, allergen info, and cancel policy visible on all breakpoints post-purchase.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Initial page | Header skeleton + timeline skeleton (4 steps) + fulfillment card skeleton |
| Status poll | No full-page reload — inline badge update |
| Reorder | **Secondary button** loading state |
| Cancel submit | Modal primary button loading |
| Review submit | Inline spinner on submit button |

Order detail is single fetch + subscription — target < 400ms initial p95.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Order not found | "This order doesn't exist or was removed." | **Primary button** "View orders" → [Order History](order-history.md) |
| Unauthorized | "You don't have access to this order." | Login prompt or order history link |
| Reorder partial failure | **Warning toast**: "Some items unavailable." | **Secondary button** "View cart" anyway |
| Cancel rejected | **Error toast**: "This order can't be cancelled." + reason | Link to [Help](help.md) |
| Real-time disconnect | Subtle banner: "Live updates paused." | Auto-reconnect; manual **Ghost button** "Refresh" |
| Creator suspended mid-fulfillment | Banner: "Creator temporarily unavailable. Support will contact you." | **Primary button** "Get help" |

Never leave customer without visible status — show last known state with stale indicator if fetch fails.

---

## Empty States

Not applicable for valid order detail. Edge cases handled in Error States.

Review prompt empty: if review already submitted, show **Review card** with submitted content read-only.

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| View order detail | ✗ (login required) | ✓ (owner only) |
| Cancel order | ✗ | ✓ (within policy) |
| Reorder | ✗ | ✓ |
| Submit review | ✗ | ✓ (completed + window) |
| View full pickup address | ✗ | ✓ (post-purchase) |

Order ownership enforced on all API calls. Signed email links grant temporary read access.

---

## Analytics

### Page events

| Event | Properties |
|-------|------------|
| `page_view` | `page: order_detail`, `order_id`, `status`, `creator_id` |
| `order_detail_status_viewed` | `order_id`, `status`, `time_since_order` |
| `order_detail_directions_clicked` | `order_id` |
| `order_detail_track_delivery_clicked` | `order_id` |
| `order_detail_reorder_clicked` | `order_id` |
| `order_detail_reorder_completed` | `order_id`, `items_added`, `items_unavailable` |
| `order_detail_cancel_initiated` | `order_id`, `status` |
| `order_detail_cancel_completed` | `order_id`, `reason` |
| `order_detail_help_clicked` | `order_id` |
| `order_detail_review_submitted` | `order_id`, `rating` |
| `order_detail_creator_clicked` | `order_id`, `creator_id` |

### Funnel metrics

- Active order page views per order
- Reorder rate from detail
- Cancel rate by status
- Review submission rate

→ [Customer Metrics](../../product/success-metrics-overview.md#customer-metrics)

---

## Accessibility

- **Landmark regions:** `banner`, `main`, `nav` (breadcrumbs)
- **Status timeline:** `ol` with `aria-label="Order status"`; `aria-current="step"` on active
- **Live updates:** `aria-live="polite"` region announces status changes
- **Fulfillment card:** Complete window and address readable by screen reader
- **Cancel flow:** **Destructive button** with `aria-describedby` linking to policy text
- **Review form:** Star rating keyboard operable; labels for each star value
- **Map/directions link:** `aria-label="Get directions to pickup location for order MP-12345"`
- **Color:** Status never conveyed by color alone — text label always present

→ [Accessibility Standards](../../design-system/accessibility-standards.md)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Order #{orderId} — {Status} | Marketplate |
| `<meta name="description">` | Track your order from [Creator Name]. |
| `robots` | `noindex, nofollow` |

Order detail is not indexable.

---

## Future Improvements

- Live map for food truck pickup
- In-app messaging thread with creator
- Photo proof of delivery
- Proactive delay notifications with revised ETA
- Split order view for catering multi-drop
- Dispute initiation flow with evidence upload

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/customers/me/orders/:orderId` | GET | Full order detail |
| `/api/v1/customers/me/orders/:orderId/events` | GET | Status timeline events (or included in detail) |
| `/api/v1/customers/me/orders/:orderId/cancel` | POST | Customer cancel with reason |
| `/api/v1/customers/me/orders/:orderId/reorder` | POST | Pre-populate cart |
| `/api/v1/customers/me/orders/:orderId/review` | POST | Submit review |
| `/api/v1/customers/me/orders/:orderId/subscribe` | WebSocket | Real-time status updates |

Response includes:
- `order` (id, number, status, created_at, cancellable, cancel_policy)
- `timeline[]` (status, label, timestamp, note)
- `fulfillment` (type, window, location, tracking_url)
- `creator` (id, slug, name, avatar, verification)
- `lines[]` (item details, allergens, instructions)
- `payment` (subtotal, fees, tax, total, method_last4, refund_status)
- `review` (eligible, submitted, window_ends_at)

---

## Related Pages

- [Order Confirmation](order-confirmation.md) — Immediate post-checkout view
- [Order History](order-history.md) — All orders list
- [Cart](cart.md) — Reorder destination
- [Creator Storefront](creator-storefront.md) — Creator profile
- [Checkout](checkout.md) — Original purchase flow
- [Help](help.md) — Order support and policies
- [Home](home.md) — Active order banner source
