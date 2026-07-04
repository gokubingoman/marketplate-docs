# Creator Dashboard (Overview)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Creator Dashboard is the **home base** of the Creator Operating System — the first screen a verified food entrepreneur sees after login. It answers three questions in under five seconds: *How is my business doing today? Am I in good standing? What do I need to do next?*

This page does not replace deep workflows (order queue, catalog, compliance). It **orients** the creator and routes them to the single most important action for the current moment.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| See today's orders and revenue at a glance | Increase daily creator engagement and order throughput |
| Understand verification and compliance standing immediately | Reduce trust incidents and expired-doc suspensions |
| Act on urgent items without hunting through menus | Improve order acceptance and fulfillment SLAs |
| Feel confident the business is under control | Improve creator retention and GMV per creator |

**Primary action on this screen:** Open the highest-priority action item (typically "Review new orders" or "Complete verification step").

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Independent Chef](../../product/personas.md#independent-chef) | Daily check-in between production blocks |
| **Secondary** | [Meal Prep Business](../../product/personas.md#meal-prep-business), [Baker](../../product/personas.md#baker), [Food Truck Operator](../../product/personas.md#food-truck-operator) | Batch-oriented and mobile contexts |
| **Anti-persona** | Enterprise restaurant manager | Not designed for multi-location franchise ops |

All creator sub-types share this dashboard; metric emphasis adapts by fulfillment model (e.g., pickup windows for bakers, location status for food trucks).

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Post-login redirect | Default landing for authenticated creators |
| [Sidebar nav](../../pages/navigation-model.md) | "Dashboard" / home icon — always first item |
| Mobile app open | Restores last session; dashboard if no deep link |
| Email/push deep link | "You have 3 new orders" → dashboard with orders module focused |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Orders](./orders.md) | "View all orders" / stat card tap / action item |
| [Order Detail](./order-detail.md) | Tap individual order in today's queue preview |
| [Compliance](./compliance.md) | Verification banner or action item |
| [Catalog](./catalog.md) | "Add menu item" action item |
| [Analytics](./analytics.md) | Revenue stat card "View details" |
| [Messages](./messages.md) | Unread message indicator |
| [Storefront Settings](./storefront-settings.md) | Profile completeness prompt |

### Breadcrumbs

None — this is the root of Creator OS. Page title: **Dashboard**.

---

## Layout

Calm, single-column-on-mobile / two-column-on-desktop layout. **Verification status** occupies the top band when not fully verified or when renewal is due.

```
┌─────────────────────────────────────────────────────────────────┐
│ [Sidebar Nav]  │  Dashboard                          [Avatar ▾] │
├────────────────┼────────────────────────────────────────────────┤
│                │  ┌─ Verification Status Banner ──────────────┐ │
│  Dashboard ●   │  │ Verified Creator ✓  ·  Kitchen ✓  · Doc ⚠ │ │
│  Orders        │  └───────────────────────────────────────────┘ │
│  Catalog       │                                                │
│  Availability  │  ┌─ Primary Action Card ─────────────────────┐ │
│  Analytics     │  │  3 new orders need confirmation           │ │
│  Messages      │  │  [ Review orders ]  ← PRIMARY CTA         │ │
│  Compliance    │  └───────────────────────────────────────────┘ │
│  Payouts       │                                                │
│  Reviews       │  ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  Settings      │  │ Today    │ │ Revenue  │ │ Rating   │       │
│                │  │ 12 orders│ │ $840     │ │ 4.8 ★    │       │
│                │  └──────────┘ └──────────┘ └──────────┘       │
│                │                                                │
│                │  Today's Orders (preview, max 5)                │
│                │  ┌ Order card ──────────────────────────────┐  │
│                │  └ Order card ──────────────────────────────┘  │
│                │  [ View all orders → ]                         │
│                │                                                │
│                │  Action Items (secondary list)                   │
│                │  · Food handler cert expires in 14 days        │
│                │  · 2 menu items missing allergen info          │
└────────────────┴────────────────────────────────────────────────┘
```

**Content hierarchy (top → bottom):**

1. Verification / compliance status strip — trust-first
2. Primary action card — one obvious next step
3. Key metrics row — scannable stat cards
4. Today's orders preview — operational context
5. Secondary action items — progressive disclosure

Whitespace between sections per [design principles](../../design-system/principles.md#2-whitespace-is-a-feature).

---

## Components

| Component | Usage on this page | DS reference |
|-----------|-------------------|--------------|
| **Sidebar nav** | Persistent Creator OS navigation | [Navigation — Sidebar](../../design-system/components-overview.md#navigation) |
| **Verification badge** | Status strip: Identity, Kitchen, Compliance layers | [Badges — Verification](../../design-system/components-overview.md#badges) |
| **Status badge** | Order status on preview cards | [Badges — Status](../../design-system/components-overview.md#badges) |
| **Dashboard stat card** | Today orders, revenue, rating summary | [Cards — Dashboard stat](../../design-system/components-overview.md#cards) |
| **Order card** | Today's queue preview (compact variant) | [Cards — Order card](../../design-system/components-overview.md#cards) |
| **Primary button** | Primary action card CTA | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | "View all orders," secondary links | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Avatar** | Account menu in header | [Avatars](../../design-system/components-overview.md#avatars) |
| **Warning toast** | Non-blocking renewal reminders on load | [Toasts — Warning](../../design-system/components-overview.md#toasts) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Primary action card** | Entire card clickable; primary button duplicates action. Navigates to contextual destination (usually [Orders](./orders.md) with filter applied). |
| **Stat cards** | Tap/click navigates to relevant detail: Orders → [Orders](./orders.md); Revenue → [Analytics](./analytics.md); Rating → [Reviews](./reviews.md). |
| **Order preview row** | Tap opens [Order Detail](./order-detail.md). Swipe left on mobile reveals quick "Mark in production" if confirmed. |
| **Verification strip** | Tap any incomplete layer → [Compliance](./compliance.md) filtered to that requirement. |
| **Action items list** | Each row links to resolving page with context pre-selected. |
| **Refresh** | Pull-to-refresh on mobile; subtle auto-refresh every 60s when tab focused (orders count only). |
| **Keyboard** | `Tab` order: skip link → nav → verification strip → primary CTA → stats → order list. `Enter` activates focused card. |

**One primary action rule:** Only the primary action card uses filled button styling. All other CTAs are ghost or text links — [design principles](../../design-system/principles.md#4-one-primary-action-per-screen).

---

## Animations

| Trigger | Motion | Duration |
|---------|--------|----------|
| Page load | Stat cards fade-up stagger (50ms offset) | 200ms ease-out |
| New order arrives (realtime) | Primary action card pulse + count increment | 300ms |
| Order status change in preview | Status badge color crossfade | 150ms |
| Pull-to-refresh | Standard spinner; content slides down | 200ms |
| Verification banner dismiss (info only) | Slide up collapse | 250ms |

Respect `prefers-reduced-motion`: instant state changes, no stagger — [accessibility standards](../../design-system/accessibility-standards.md).

---

## Responsive Behaviour

| Breakpoint | Layout changes |
|------------|----------------|
| **Mobile (320–767px)** | Sidebar collapses to hamburger; single column; stat cards 2×2 grid then stack; order preview full-width; primary action card sticky below header when scrolling |
| **Tablet (768–1023px)** | Collapsible sidebar; stat cards 3-across; two-column for orders + action items |
| **Desktop (1024px+)** | Persistent sidebar; stat cards inline row; orders preview + action items side-by-side |

Content parity: verification status and primary action visible on all breakpoints without horizontal scroll.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| **Full page (first visit)** | Skeleton: verification strip bar, primary action card block, three stat card rectangles, five order row skeletons |
| **Stat cards** | Shimmer placeholders; resolve independently as metrics API returns |
| **Orders preview** | Skeleton list; replaces with empty or populated state |
| **Background refresh** | No full-page spinner; subtle opacity pulse on stat numbers only |

Never show skeleton longer than 3s without inline "Taking longer than usual" message + retry link.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| **Metrics API failure** | "Couldn't load today's numbers" | Inline retry on stat cards; rest of page functional |
| **Orders preview failure** | "Orders unavailable right now" | Retry button; link to [Orders](./orders.md) full page |
| **Verification status unavailable** | Warning banner: "Verification status couldn't be loaded" | Retry; creator can still access other sections |
| **Session expired** | Redirect to auth with return URL | Standard auth recovery |
| **Account suspended** | Full-page blocked state with support link | No dashboard access; compliance context shown |

Critical errors (suspension) use modal, not toast — [components overview](../../design-system/components-overview.md#toasts).

---

## Empty States

| Scenario | Display | Primary action |
|----------|---------|----------------|
| **New creator, verification incomplete** | Verification strip expanded; primary action = "Complete verification" → [Compliance](./compliance.md) | [Complete verification] |
| **Verified, zero orders today** | Stat cards show 0; calm illustration; "No orders yet today" | [Share storefront link] → [Storefront Settings](./storefront-settings.md) |
| **Verified, zero orders ever** | Onboarding checklist replaces order preview: profile photo, first menu item, availability | [Add your first menu item] → [Catalog](./catalog.md) |
| **All action items complete** | Action items section hidden — whitespace intentional | N/A |

Empty states are not errors — generous whitespace, encouraging copy per [design principles](../../design-system/principles.md#2-whitespace-is-a-feature).

---

## Permissions

| Role | Access |
|------|--------|
| **Creator owner** | Full dashboard; all metrics and actions |
| **Creator staff — orders** | Dashboard without revenue/payout stats; orders preview + action items for orders only |
| **Creator staff — kitchen** | Orders preview + production action items only |
| **Unverified creator** | Dashboard in limited mode: verification-focused; no live order acceptance |
| **Suspended creator** | Blocked; redirect to compliance resolution |

Team permissions defined in engineering access docs; UI hides unauthorized stat cards entirely (not disabled).

---

## Analytics

| Event | Properties | Purpose |
|-------|------------|---------|
| `creator_dashboard_viewed` | `creator_id`, `verification_status`, `pending_orders_count` | Engagement baseline |
| `creator_dashboard_primary_action_clicked` | `action_type` (review_orders, complete_verification, share_storefront) | Action prioritization effectiveness |
| `creator_dashboard_stat_card_clicked` | `stat_type` | Navigation patterns |
| `creator_dashboard_order_preview_clicked` | `order_id`, `order_status` | Queue funnel |
| `creator_dashboard_action_item_clicked` | `item_type`, `item_priority` | Proactive task completion |
| `creator_dashboard_refresh` | `manual` (bool) | Realtime needs |

Funnel: dashboard view → primary action → order confirmed within session.

---

## Accessibility

| Requirement | Implementation |
|-------------|----------------|
| **Page title** | `<h1>Dashboard</h1>` — unique, descriptive |
| **Verification strip** | `role="status"` with `aria-live="polite"` on status changes |
| **Stat cards** | Each card is a single focusable link with `aria-label`: "Today's orders: 12. View all orders." |
| **Primary action** | `aria-describedby` links to urgency context ("3 new orders") |
| **Order preview** | List semantics (`<ul>`/`<li>`); status badge text not color-only |
| **Focus order** | Logical top-to-bottom; skip link to main content |
| **Touch targets** | Minimum 44×44px on all interactive elements |
| **Contrast** | WCAG 2.2 AA — token-driven colors |

Screen reader announcement on new order: "You have 3 new orders needing confirmation."

---

## SEO

Not applicable — authenticated creator surface. `noindex, nofollow` on all `/creator/*` routes.

---

## Future Improvements

- Customizable dashboard widgets (reorder/hide stat cards)
- Production calendar mini-view for bakers and meal prep
- Food truck "Open now" toggle on dashboard
- AI-generated daily briefing ("Expect a busy Saturday based on last month")
- Multi-location support for operators with multiple pickup points
- Benchmark metrics ("You're in the top 20% for repeat customers in your area")

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `GET /api/v1/creator/dashboard/summary` | GET | Aggregated metrics: today orders, revenue, rating, pending counts |
| `GET /api/v1/creator/dashboard/action-items` | GET | Prioritized task list with deep-link targets |
| `GET /api/v1/creator/orders` | GET | Preview query: `?date=today&limit=5&sort=created_at_desc` |
| `GET /api/v1/creator/verification/status` | GET | Trust layer statuses for banner |
| `GET /api/v1/creator/messages/unread-count` | GET | Badge on nav and optional dashboard chip |
| WebSocket / SSE `creator.{id}.orders` | Subscribe | Realtime new order notifications |

Response SLA target: summary endpoint < 300ms p95.

---

## Related Pages

- [Orders](./orders.md) — full order queue
- [Order Detail](./order-detail.md) — single order workflow
- [Compliance](./compliance.md) — verification and document management
- [Catalog](./catalog.md) — menu management
- [Analytics](./analytics.md) — detailed business metrics
- [Storefront Settings](./storefront-settings.md) — brand and profile completeness
- [Availability](./availability.md) — schedule and capacity
- [Messages](./messages.md) — customer communication
- [Reviews](./reviews.md) — reputation management
- [Payouts](./payouts.md) — earnings visibility
