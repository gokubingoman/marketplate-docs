# Order History

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/orders`  
**Surface:** Customer marketplace (web + mobile)  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Order History page is the customer's repeat-purchase hub — active orders pinned for tracking, past orders grouped for reference, and one-tap paths to reorder or review. It answers: *What have I ordered? What's in progress? Can I get that again?*

This page connects post-purchase retention to discovery — every completed order links back to verified creators on [Creator Storefront](creator-storefront.md) and pre-populates [Cart](cart.md) for frictionless reorder.

---

## Goals

### User goals

- See all active orders with status at a glance
- Browse past orders by date with creator and item summaries
- Tap any order for full detail and tracking
- Reorder favorite meals quickly when available
- Leave reviews for completed orders within the review window

### Business goals

- Drive repeat purchase rate via reorder and creator re-engagement
- Reduce support load by surfacing order status without contact
- Capture reviews post-completion
- Personalize [Home](home.md) "Order again" module from history data
- Measure reorder conversion and review submission rates

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Returning buyer with purchase history |
| **Secondary** | First-time buyer post-first-order | Single active order state |
| **Anti-persona** | Guest without account | Redirect to login — history requires auth |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| Tab bar "Orders" (mobile) | Primary entry |
| [Home](home.md) | Active order banner, "Order again" |
| [Order Confirmation](order-confirmation.md) | "View order history" fallback |
| [Order Detail](order-detail.md) | Breadcrumb "Orders" |
| Top nav account menu | "Your orders" |
| Direct URL | `/orders` |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Order Detail](order-detail.md) | Order card tap, active order CTA |
| [Cart](cart.md) | Reorder action |
| [Creator Storefront](creator-storefront.md) | Creator name on order card |
| [Home](home.md) | Logo, empty state CTA |
| [Browse](browse.md) | Empty state "Discover creators" |
| [Help](help.md) | Footer link |

### Global chrome

- **Top nav bar:** Logo, search, cart, account menu
- **Tab bar (mobile):** Orders tab active
- **Page header:** "Your orders" (h1)

---

## Layout

### Content hierarchy (top to bottom)

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — logo, search, cart, account                  │
├─────────────────────────────────────────────────────────────┤
│  Page header — "Your orders" (h1)                           │
├─────────────────────────────────────────────────────────────┤
│  Active orders section (if any) — "In progress"             │
│  ┌─ Order card (compact, elevated) ──────────────────────┐  │
│  │  Status badge · Creator · ETA · "Track order" link    │  │
│  └───────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│  Past orders — grouped by month                             │
│  "July 2026"                                                │
│  ┌─ Order card (compact) ────────────────────────────────┐  │
│  │  Creator avatar, name, verification badge             │  │
│  │  Item summary · date · total · Status badge           │  │
│  │  Actions: View · Reorder · Review (if eligible)       │  │
│  └───────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│  Pagination — load more (12 orders per page)                │
└─────────────────────────────────────────────────────────────┘
```

### Grid

| Breakpoint | Layout |
|------------|--------|
| Mobile (320–767px) | Single column full-width cards |
| Tablet (768–1023px) | Single column max-width 720px centered |
| Desktop (1024px+) | Single column max-width 800px; active orders 2-col if multiple |

---

## Components

| Component | Usage on this page |
|-----------|-------------------|
| **Top nav bar** | Global navigation |
| **Tab bar (mobile)** | Orders tab active |
| **Order card** (compact) | Active and past order rows |
| **Status badge** | Order status on every card |
| **Creator avatar** | Order card header |
| **Verification badge** | Creator row on card |
| **Primary button** | "Track order" on active cards |
| **Secondary button** | "Reorder" |
| **Ghost button** | "View order", "Leave review" |
| **Pagination** | Load more past orders |
| **Toast** (Success) | Reorder added to cart |
| **Toast** (Warning) | Partial reorder — some items unavailable |
| **Toast** (Error) | Reorder failure |

---

## Interactions

### Active orders

- Pinned above past orders — sorted by nearest fulfillment window
- **Status badge** with live status (poll every 60s when page visible)
- Card tap → [Order Detail](order-detail.md)
- **Primary button** "Track order" → same destination
- Multiple active orders: each card independent

### Past orders

- Grouped by month headers (e.g., "July 2026")
- Sorted reverse chronological within group
- Card tap → [Order Detail](order-detail.md)
- Creator name → [Creator Storefront](creator-storefront.md) (does not navigate card)

### Reorder

- **Secondary button** "Reorder" → POST reorder API → [Cart](cart.md) on success
- Partial availability → **Warning toast** listing unavailable items; available items in cart
- Creator not accepting → **Error toast**: "This creator isn't taking orders." + link to storefront
- Does not bypass [Cart](cart.md) review — customer confirms before checkout

### Review

- **Ghost button** "Leave review" visible when `review_eligible` and not submitted
- Tap → [Order Detail](order-detail.md)#review or inline **Form modal** on desktop
- Expired window → button hidden

### Load more

- **Pagination** appends next 12 orders; focus moves to first new card
- No infinite scroll — explicit load per [design principles](../../design-system/principles.md)

### Keyboard

- Tab through active orders first, then past orders chronologically
- Enter on focused card opens order detail
- Reorder and review buttons in tab order after card link

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Page load | Active orders fade-in first; past orders stagger 50ms |
| Status update | **Status badge** crossfade 150ms |
| Load more | New cards slide-up 200ms |
| Reorder success | Brief cart badge bounce on nav |
| Empty → first order | N/A — user navigates away to shop |

Respect `prefers-reduced-motion`.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Full-width cards; tab bar Orders active; swipe-friendly card tap targets |
| **Tablet** | Centered list; inline action buttons on card footer |
| **Desktop** | Wider cards with horizontal action row; 2-column active orders if 2+ active |

**Content parity:** Verification badges and status on every card — all breakpoints.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Initial page | 1 active order skeleton + 6 past order card skeletons |
| Load more | Inline spinner below list; existing orders persist |
| Reorder | **Secondary button** loading on affected card only |
| Status refresh | Silent badge update — no skeleton flash |

Active orders fetched first in parallel with first page of history.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| History API failure | "We couldn't load your orders." | **Primary button** "Try again" |
| Reorder failure | **Error toast**: "Couldn't reorder. Try again." | Retry |
| Partial reorder | **Warning toast** with unavailable item names | **Secondary button** "View cart" |
| Auth expired | Redirect to login with return URL `/orders` | Re-auth |
| Network offline | **Info toast**: "Showing cached orders." | Cached list with stale indicator |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| No orders ever | "You haven't placed an order yet." | **Primary button** "Discover creators" → [Browse](browse.md) |
| No active, has past | Active section omitted — not shown | — |
| Search/filter no match (future) | "No orders match your search." | **Ghost button** "Clear search" |

Empty state reinforces discovery — no guilt language per [voice and tone](../../brand/voice-and-tone.md).

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| View order history | ✗ (redirect login) | ✓ |
| View active orders | ✗ | ✓ |
| Reorder | ✗ | ✓ |
| Leave review | ✗ | ✓ (eligible orders) |

Page requires authentication. Guest redirect preserves return URL.

---

## Analytics

### Page events

| Event | Properties |
|-------|------------|
| `page_view` | `page: order_history`, `active_count`, `past_count` |
| `order_history_card_clicked` | `order_id`, `status`, `section: active | past` |
| `order_history_track_clicked` | `order_id`, `status` |
| `order_history_reorder_clicked` | `order_id`, `creator_id` |
| `order_history_reorder_completed` | `order_id`, `items_added`, `items_unavailable` |
| `order_history_review_clicked` | `order_id` |
| `order_history_creator_clicked` | `order_id`, `creator_id` |
| `order_history_load_more` | `page`, `orders_loaded` |
| `order_history_empty_cta` | `destination: browse | home` |

### Funnel metrics

- Order history → reorder rate
- Active order → detail CTR
- Review initiation rate from history

→ [Customer Metrics](../../product/success-metrics-overview.md#customer-metrics)

---

## Accessibility

- **Landmark regions:** `banner`, `main`
- **Page header:** `h1` "Your orders"
- **Active section:** `section` with `aria-label="Orders in progress"`
- **Past orders:** `section` with `aria-label="Past orders"`; month headers `h2`
- **Order cards:** `article` with `aria-label="Order from [creator] on [date], [status], total [amount]"`
- **Status badge:** Text label always present in accessible name
- **Load more:** Announces new order count via `aria-live="polite"`
- **Empty state:** Focus moves to primary CTA on render

→ [Accessibility Standards](../../design-system/accessibility-standards.md)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Your Orders | Marketplate |
| `<meta name="description">` | View and track your orders from verified local food creators. |
| `robots` | `noindex, nofollow` |

Order history is not indexable.

---

## Future Improvements

- Filter by creator, status, or date range
- Search order history
- Export order receipts (PDF)
- Favorite orders pin
- Subscription management for recurring meal prep orders
- Order again carousel at top personalized from ML

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/customers/me/orders` | GET | Paginated list; params: `status`, `page`, `limit` |
| `/api/v1/customers/me/orders/active` | GET | Active orders only (may be filter on main endpoint) |
| `/api/v1/customers/me/orders/:orderId/reorder` | POST | Pre-populate cart |

List response per order:
- `id`, `number`, `status`, `created_at`, `total`
- `creator` (id, slug, name, avatar, verification)
- `item_summary` (count, first_item_name, thumbnail_url)
- `fulfillment` (type, window_start — for active)
- `review_eligible`, `review_submitted`

Active orders endpoint used by [Home](home.md) banner — shared cache.

---

## Related Pages

- [Order Detail](order-detail.md) — Single order tracking and actions
- [Order Confirmation](order-confirmation.md) — Latest order entry
- [Cart](cart.md) — Reorder destination
- [Creator Storefront](creator-storefront.md) — Creator re-engagement
- [Home](home.md) — Order again module source
- [Browse](browse.md) — Empty state discovery
- [Help](help.md) — Order and refund FAQs
