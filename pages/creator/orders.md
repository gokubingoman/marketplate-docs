# Creator Orders (Order Queue)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/orders`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Orders page is the **production command center** — where creators view, filter, and act on every customer order. It replaces scattered DMs and spreadsheets with a single queue tied to the [order lifecycle](../../product/marketplace-mechanics.md#order-lifecycle).

Creators spend most of their operational time here during service hours. The page must surface urgency (new confirmations, allergy flags, approaching pickup windows) without overwhelming batch operators with noise.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| See all orders organized by status and urgency | Reduce missed orders and late fulfillments |
| Filter quickly by today, status, or fulfillment type | Support diverse creator workflows (batch vs. à la carte) |
| Identify allergy and dietary flags before production | Prevent food safety incidents |
| Move orders through lifecycle with minimal taps | Improve completion rate and customer satisfaction |

**Primary action on this screen:** Open the next order requiring action (contextual label: "Review order #1042" or "Mark ready — pickup in 30 min").

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Meal Prep Business](../../product/personas.md#meal-prep-business) | Batch view; cut-off aware sorting |
| **Secondary** | [Independent Chef](../../product/personas.md#independent-chef), [Baker](../../product/personas.md#baker) | Custom order and lead-time sensitivity |
| **Secondary** | [Caterer](../../product/personas.md#caterer) | Event orders filtered by date range |
| **Anti-persona** | Customer placing an order | Customer-facing tracking lives on customer surfaces |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| [Dashboard](./dashboard.md) | "View all orders," primary action card, stat card |
| Sidebar nav | "Orders" — badge shows pending count |
| Push notification | Deep link with `?status=confirmed` or specific order |
| [Order Detail](./order-detail.md) | Back navigation via breadcrumb |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Order Detail](./order-detail.md) | Tap any order row/card |
| [Dashboard](./dashboard.md) | Sidebar home |
| [Messages](./messages.md) | "Message customer" from order row overflow |
| [Availability](./availability.md) | Capacity warning link when queue exceeds limits |

### Breadcrumbs

`Dashboard → Orders`

---

## Layout

List-first layout with persistent filter bar. **Verification gate:** unverified creators see read-only historical orders (if any) with banner blocking new acceptance.

```
┌─────────────────────────────────────────────────────────────────┐
│ Dashboard → Orders                              [Search orders] │
├─────────────────────────────────────────────────────────────────┤
│ [ Needs action (3) ] [ Today (12) ] [ Upcoming ] [ Completed ]  │  ← Segmented control
├─────────────────────────────────────────────────────────────────┤
│ Filters: Status ▾  Fulfillment ▾  Date ▾  [ Allergen flag only ]│
├─────────────────────────────────────────────────────────────────┤
│ ┌─ Primary action bar ─────────────────────────────────────────┐│
│ │ Next: Order #1042 — Confirm · Pickup today 4:30 PM          ││
│ │                              [ Review order ]  ← PRIMARY     ││
│ └──────────────────────────────────────────────────────────────┘│
├─────────────────────────────────────────────────────────────────┤
│ ┌ Order card ────────────────────────────────────────────────┐  │
│ │ #1042 · Confirmed · Sarah M. · $48.00                      │  │
│ │ 2 items · Pickup 4:30 PM · ⚠ Contains nuts (customer alert)│  │
│ │ [In production]  [Message]                                 │  │
│ └────────────────────────────────────────────────────────────┘  │
│ ┌ Order card ────────────────────────────────────────────────┐  │
│ │ #1041 · In production · ...                                │  │
│ └────────────────────────────────────────────────────────────┘  │
│                                                                 │
│ [ Load more ]                                                   │
└─────────────────────────────────────────────────────────────────┘
```

**Sort default:** Needs-action first → pickup window ascending → created_at descending.

---

## Components

| Component | Usage | DS reference |
|-----------|-------|--------------|
| **Segmented control** | View tabs: Needs action, Today, Upcoming, Completed | [Navigation — Segmented control](../../design-system/components-overview.md#navigation) |
| **Search input** | Filter by order #, customer name | [Inputs — Search](../../design-system/components-overview.md#inputs) |
| **Select / dropdown** | Status, fulfillment type, date filters | [Inputs — Select](../../design-system/components-overview.md#inputs) |
| **Checkbox** | "Allergen flag only" toggle filter | [Inputs — Checkbox](../../design-system/components-overview.md#inputs) |
| **Order card** | Primary list item with status, items summary, flags | [Cards — Order card](../../design-system/components-overview.md#cards) |
| **Status badge** | Lifecycle state per order | [Badges — Status](../../design-system/components-overview.md#badges) |
| **Dietary badge** | Allergen/dietary flags on card | [Badges — Dietary](../../design-system/components-overview.md#badges) |
| **Primary button** | Primary action bar CTA; inline quick actions use secondary | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Secondary button** | "In production," "Mark ready" on card | [Buttons — Secondary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | "Message," "Load more" | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Pagination** | Completed tab and long lists | [Navigation — Pagination](../../design-system/components-overview.md#navigation) |
| **Confirmation modal** | Cancel order, bulk status change | [Modals — Confirmation](../../design-system/components-overview.md#modals) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Segmented control** | Switches list query preset; preserves secondary filters where compatible |
| **Order card tap** | Opens [Order Detail](./order-detail.md) |
| **Inline status button** | Advances lifecycle one step with confirmation if destructive; toast on success |
| **Allergen flag icon** | Tooltip with customer-stated allergies + item-level allergens; card gets subtle warning border (not color-only) |
| **Search** | Debounced 300ms; searches order ID, customer name, item names |
| **Bulk select (desktop)** | Checkbox column on Completed tab for export; v1 optional |
| **Keyboard shortcuts** | `j`/`k` navigate list; `Enter` open detail; `p` mark in production (when focused) |
| **Swipe (mobile)** | Swipe right: advance status; swipe left: message customer |

**One primary action:** The primary action bar highlights exactly one next order. Per-card buttons are secondary styling.

---

## Animations

| Trigger | Motion |
|---------|--------|
| Tab switch | Crossfade list content | 200ms |
| Status advance | Card slides out / badge morphs to new state | 250ms ease-out |
| New order (realtime) | Card inserts at top with subtle highlight fade | 300ms |
| Filter apply | List reflow with stagger fade | 150ms per card, max 5 |
| Empty filter result | Illustration fade-in | 200ms |

`prefers-reduced-motion`: instant tab swap, no insert animation.

---

## Responsive Behaviour

| Breakpoint | Changes |
|------------|---------|
| **Mobile** | Segmented control scrolls horizontally; filters collapse to "Filters" sheet; cards full-width; swipe actions enabled |
| **Tablet** | Filters inline; two-column card grid optional for Completed tab |
| **Desktop** | Table view toggle for Completed tab (dense); filters always visible; bulk actions |

Order cards maintain identical information density across breakpoints — no hidden allergen flags on mobile.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Initial load | 8 skeleton order cards matching card anatomy |
| Tab switch | Inline skeleton in list area; filter bar persists |
| Load more | Spinner on button; append skeleton row |
| Inline status update | Button → loading spinner; card locked until response |

Pagination cursor preserved on back navigation from detail.

---

## Error States

| Error | Recovery |
|-------|----------|
| List fetch failed | Full-width inline error + retry; filters remain interactive |
| Status update failed | Toast error; card reverts to previous status |
| Realtime disconnect | Banner: "Live updates paused" + reconnect |
| Over-capacity | Warning banner linking to [Availability](./availability.md) — orders still visible |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| **Needs action — empty** | "You're all caught up" | Ghost link to Today tab |
| **Today — empty** | "No orders scheduled for today" | [Adjust availability](./availability.md) |
| **Upcoming — empty** | "No upcoming orders" | [Share storefront](./storefront-settings.md) |
| **Completed — empty** | "Completed orders will appear here" | — |
| **Filter — no match** | "No orders match these filters" | [Clear filters] |
| **Unverified** | "Complete verification to accept orders" | [Go to Compliance](./compliance.md) |

---

## Permissions

| Role | Capabilities |
|------|--------------|
| Owner | Full queue access; cancel/refund initiation |
| Staff — orders | View and advance status; no cancel/refund |
| Staff — read-only | View only; no status changes |
| Unverified | No new orders in queue; onboarding CTA |

---

## Analytics

| Event | Properties |
|-------|------------|
| `creator_orders_viewed` | `tab`, `filter_status`, `order_count` |
| `creator_orders_filter_applied` | `filter_type`, `filter_value` |
| `creator_orders_primary_action_clicked` | `order_id`, `action_type` |
| `creator_orders_inline_status_changed` | `order_id`, `from_status`, `to_status`, `source` (inline vs detail) |
| `creator_orders_search` | `query_length`, `result_count` |
| `creator_orders_allergen_filter_toggled` | `enabled` |

Operational metric: time from `confirmed` → `in_production` tracked per creator.

---

## Accessibility

- Filter controls labeled; segmented control uses `role="tablist"` / `role="tab"`
- Order cards: `<article>` with heading `Order #1042, Confirmed, pickup 4:30 PM`
- Allergen warnings: icon + text; `aria-label` includes full allergen summary
- List virtualized on desktop for performance — focus management preserves position
- Status changes announce via `aria-live="polite"`

---

## SEO

Not applicable — authenticated route, `noindex`.

---

## Future Improvements

- Batch production view (group by item/SKU for meal prep)
- Print kitchen ticket / production sheet
- Calendar view for caterers and pop-ups
- SLA indicators (time until pickup with color-neutral urgency labels)
- Integration with label printers
- Order notes pinned across lifecycle

---

## API Requirements

| Endpoint | Purpose |
|----------|---------|
| `GET /api/v1/creator/orders` | Paginated list with filters: `status`, `fulfillment_type`, `date_from`, `date_to`, `allergen_flag`, `q` |
| `GET /api/v1/creator/orders/next-action` | Single order for primary action bar |
| `PATCH /api/v1/creator/orders/{id}/status` | Lifecycle transitions |
| WebSocket `creator.{id}.orders` | Realtime insert/update |

Status transitions validated server-side per [marketplace mechanics](../../product/marketplace-mechanics.md#order-lifecycle).

---

## Related Pages

- [Dashboard](./dashboard.md) — overview and entry point
- [Order Detail](./order-detail.md) — full order workflow
- [Messages](./messages.md) — customer threads linked to orders
- [Availability](./availability.md) — capacity and pickup windows
- [Catalog](./catalog.md) — item reference for order line items
- [Analytics](./analytics.md) — order volume trends
- [Compliance](./compliance.md) — verification required to accept orders
