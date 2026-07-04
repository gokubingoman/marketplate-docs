# Creator Order Detail

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/orders/{order_id}`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

Order Detail is the **single-order operational view** — everything a creator needs to fulfill one order correctly: line items, modifications, customer notes, allergen alerts, fulfillment instructions, payment summary, and status actions.

This page exists because mistakes on allergies, modifications, and timing destroy trust. Creators must never hunt across messages and order lists to assemble context.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| See complete order context in one place | Reduce fulfillment errors and disputes |
| Act on allergen and dietary flags before cooking | Protect customer safety and platform trust |
| Advance order status with clear next step | Improve on-time ready rate |
| Communicate with customer without leaving order | Faster issue resolution |

**Primary action:** Contextual lifecycle action — "Confirm order," "Mark in production," "Mark ready for pickup," or "Mark completed" depending on current state.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Independent Chef](../../product/personas.md#independent-chef) | Allergy flags critical |
| **Secondary** | [Baker](../../product/personas.md#baker) | Custom decoration notes, lead times |
| **Secondary** | [Caterer](../../product/personas.md#caterer) | Event details, headcount, venue notes |
| **Anti-persona** | Platform operator | Admin dispute view is separate internal surface |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| [Orders](./orders.md) | List tap, primary action bar |
| [Dashboard](./dashboard.md) | Order preview tap |
| [Messages](./messages.md) | Order-linked thread header link |
| Push notification | Deep link to specific order |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Orders](./orders.md) | Back / breadcrumb |
| [Messages](./messages.md) | "Message customer" — thread scoped to order |
| [Catalog](./catalog.md) | Tap menu item name (reference only) |

### Breadcrumbs

`Dashboard → Orders → Order #1042`

---

## Layout

Two-column on desktop; stacked on mobile. **Allergen alert** pinned below header when present — never collapsed by default per [trust in design](../../design-system/principles.md#trust-in-design).

```
┌─────────────────────────────────────────────────────────────────┐
│ ← Orders    Order #1042                    Status: Confirmed    │
├─────────────────────────────────────────────────────────────────┤
│ ⚠ ALLERGEN ALERT — Customer reported: tree nut allergy         │
│   Items flagged: Pesto Pasta (contains pine nuts)              │
├───────────────────────────────┬─────────────────────────────────┤
│ ITEMS                         │ FULFILLMENT                     │
│ ┌─────────────────────────┐   │ Pickup · Today 4:30–5:00 PM     │
│ │ Pesto Pasta        $18  │   │ Location: Main Kitchen          │
│ │ Qty 1 · Size: Regular   │   │ [Verified Kitchen badge]        │
│ │ ⚠ Contains: tree nuts   │   │                                 │
│ │ Note: Extra basil       │   │ CUSTOMER                        │
│ └─────────────────────────┘   │ Sarah M. · Verified purchase    │
│ ┌─────────────────────────┐   │ [Avatar]                        │
│ │ Sourdough Loaf     $12  │   │ Order note: "Gift — no price    │
│ │ Qty 2                   │   │  on receipt"                    │
│ └─────────────────────────┘   │                                 │
│                               │ PAYMENT SUMMARY                 │
│ Subtotal              $42.00  │ Subtotal · Fees · Total         │
│                               │ Paid ✓                          │
├───────────────────────────────┴─────────────────────────────────┤
│ [ Mark in production ]  ← PRIMARY    [Message]  [Cancel order]  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Components

| Component | Usage | DS reference |
|-----------|-------|--------------|
| **Status badge** | Header order state | [Badges — Status](../../design-system/components-overview.md#badges) |
| **Dietary badge** | Per-item allergen tags | [Badges — Dietary](../../design-system/components-overview.md#badges) |
| **Verification badge** | Kitchen/production location | [Badges — Verification](../../design-system/components-overview.md#badges) |
| **Order card sections** | Grouped content blocks | [Cards](../../design-system/components-overview.md#cards) |
| **Avatar** | Customer identity | [Avatars](../../design-system/components-overview.md#avatars) |
| **Primary button** | Next lifecycle status action | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Secondary button** | Message customer | [Buttons — Secondary](../../design-system/components-overview.md#buttons) |
| **Destructive button** | Cancel order (with modal) | [Buttons — Destructive](../../design-system/components-overview.md#buttons) |
| **Confirmation modal** | Cancel confirmation, refund acknowledgment | [Modals — Confirmation](../../design-system/components-overview.md#modals) |
| **Toast** | Status update success/failure | [Toasts](../../design-system/components-overview.md#toasts) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Primary status button** | Advances to next valid state per [lifecycle](../../product/marketplace-mechanics.md#order-lifecycle); label updates dynamically |
| **Allergen banner** | Tap expands full allergen matrix: customer-stated + item-declared + checkout acknowledgment |
| **Item row** | Tap item name opens read-only catalog reference modal |
| **Message customer** | Opens [Messages](./messages.md) thread with order context header |
| **Cancel order** | Opens confirmation modal with policy summary and refund implication |
| **Print ticket** | v1 optional — triggers browser print stylesheet |
| **Timeline (footer)** | Expandable audit: placed → confirmed → status changes with timestamps |

Invalid transitions disabled with tooltip explaining prerequisite (e.g., "Confirm order first").

---

## Animations

| Trigger | Motion |
|---------|--------|
| Status advance | Primary button → loading → success checkmark morph; header badge crossfade | 300ms |
| Allergen banner expand | Accordion height animation | 250ms ease-out |
| Page enter | Content fade-up | 200ms |
| Cancel modal | Standard modal enter | 200ms |

Reduced motion: instant status label swap.

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Single column; fulfillment + customer above payment; primary action sticky footer bar |
| **Tablet** | Single column with wider item cards |
| **Desktop** | Two-column: items left (60%), fulfillment/customer/payment right (40%) |

Allergen banner full-width all breakpoints. Primary action always visible — sticky on mobile.

---

## Loading States

- Skeleton: header bar, allergen placeholder strip, 2 item rows, sidebar blocks
- Status button shows spinner during PATCH; optimistic UI with rollback on failure
- Timeline loads progressively below fold

---

## Error States

| Error | Recovery |
|-------|----------|
| Order not found | 404 page with link to [Orders](./orders.md) |
| Status transition rejected | Inline error on button + toast; explain valid transitions |
| Permission denied | Read-only view with explanation |
| Stale data (updated elsewhere) | Banner: "Order updated" + refresh button |

---

## Empty States

Not applicable — order detail requires an order ID. Invalid ID shows error state.

Partial order (all items cancelled): show remaining items with struck-through removed items in timeline.

---

## Permissions

| Role | Access |
|------|--------|
| Owner | Full status control, cancel, refund initiation |
| Staff — orders | Status advance, message; no cancel |
| Staff — read-only | View only |
| Unverified | Cannot access live order actions |

---

## Analytics

| Event | Properties |
|-------|------------|
| `creator_order_detail_viewed` | `order_id`, `status`, `has_allergen_flag`, `item_count` |
| `creator_order_status_changed` | `order_id`, `from`, `to`, `time_in_previous_state_seconds` |
| `creator_order_allergen_banner_expanded` | `order_id` |
| `creator_order_message_clicked` | `order_id` |
| `creator_order_cancel_initiated` | `order_id`, `reason` |
| `creator_order_cancel_confirmed` | `order_id` |

Safety metric: orders with allergen flags where status advanced without banner view (should be zero — track expand or dwell time).

---

## Accessibility

- Page title: `Order #1042 — Confirmed`
- Allergen alert: `role="alert"` on initial load when flags present
- Status button: `aria-label` includes action + order number
- Item list: table semantics on desktop, list on mobile
- Timeline: accessible definition list with datetime in `<time datetime>`
- Focus trap in cancel modal; return focus to cancel button on close

---

## SEO

Not applicable — authenticated, `noindex`.

---

## Future Improvements

- Photo proof of fulfillment upload
- Delivery driver handoff tracking
- Item-level prep checklist for catering
- Voice read-aloud of order for kitchen (accessibility + hands-busy)
- Integration with kitchen display system (KDS)
- Change order workflow (modifications with customer approval)

---

## API Requirements

| Endpoint | Purpose |
|----------|---------|
| `GET /api/v1/creator/orders/{id}` | Full order: items, notes, allergens, fulfillment, payment, timeline |
| `PATCH /api/v1/creator/orders/{id}/status` | Lifecycle transition with validation |
| `POST /api/v1/creator/orders/{id}/cancel` | Cancel with reason code |
| `GET /api/v1/creator/orders/{id}/messages` | Thread preview / link to messaging |

Include `customer_allergen_declarations`, `item_allergens`, `checkout_allergen_ack` in response.

---

## Related Pages

- [Orders](./orders.md) — queue and filters
- [Dashboard](./dashboard.md) — order preview entry
- [Messages](./messages.md) — customer communication
- [Catalog](./catalog.md) — item allergen source data
- [Menu Item Editor](./menu-item-editor.md) — edit item allergens
- [Availability](./availability.md) — pickup window source
- [Compliance](./compliance.md) — kitchen verification on fulfillment block
