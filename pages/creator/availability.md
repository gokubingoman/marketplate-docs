# Creator Availability (Schedule & Capacity)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/availability`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Availability page is where creators define **when and how much they can fulfill** — weekly schedules, pickup windows, order cut-offs, daily capacity limits, and special closures. Accurate availability prevents overselling, sets customer expectations at checkout, and feeds discovery signals ("pickup today," "open now") per [Marketplace Mechanics — Accurate availability](../../product/marketplace-mechanics.md#discovery).

This page is operational, not onboarding. Creators return here whenever production rhythm changes — seasonal hours, pop-up events, or capacity adjustments during busy periods.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| Set recurring weekly hours and pickup windows | Reduce missed pickups and scheduling disputes |
| Define order cut-offs and lead times per fulfillment type | Align customer expectations with production reality |
| Cap daily order volume to prevent overload | Protect fulfillment SLAs and creator burnout |
| Block dates for closures or events | Prevent orders when creator cannot fulfill |
| See how availability affects live storefront | Improve conversion via accurate "open" signals |

**Primary action on this screen:** Save and publish schedule changes — or "Set pickup windows" when none configured.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Baker](../../product/personas.md#baker) | Batch windows; strict cut-offs |
| **Primary** | [Meal Prep Business](../../product/personas.md#meal-prep-business) | Weekly batch cycles; capacity caps |
| **Secondary** | [Food Truck Operator](../../product/personas.md#food-truck-operator) | Location + "open now" toggle; event schedule |
| **Secondary** | [Independent Chef](../../product/personas.md#independent-chef) | Flexible pickup slots |
| **Anti-persona** | Customer choosing pickup time | Customer sees derived windows at checkout — not this editor |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Sidebar nav | "Availability" |
| [Dashboard](./dashboard.md) | Action item: "Set your pickup schedule" |
| [Orders](./orders.md) | Capacity warning banner when queue exceeds limits |
| [Catalog](./catalog.md) | Item-level availability link (future) |
| Onboarding checklist | First availability setup prompt |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Dashboard](./dashboard.md) | Sidebar home |
| [Orders](./orders.md) | "View orders for this window" from calendar day |
| [Storefront Settings](./storefront-settings.md) | Fulfillment defaults link |
| [Analytics](./analytics.md) | Capacity utilization insight (future) |

### Breadcrumbs

`Dashboard → Availability`

---

## Layout

Calendar-first editor with schedule sidebar. **Verification gate:** unverified creators can configure draft availability; changes do not affect live storefront until verified.

```
┌─────────────────────────────────────────────────────────────────┐
│ Dashboard → Availability                    [Preview on storefront]│
├─────────────────────────────────────────────────────────────────┤
│ Status: Live · Next pickup window: Today 4–6 PM · 8 slots left  │
├──────────────────────────────┬──────────────────────────────────┤
│ Weekly schedule              │  July 2026                        │
│                              │  ┌─ Su Mo Tu We Th Fr Sa ──────┐ │
│ Mon  [✓] 10 AM – 2 PM        │  │     1  2  3  4  5  6  7     │ │
│      Pickup: 4–6 PM          │  │  8  9 [10]11 12 13 14        │ │
│ Tue  [✓] ...                 │  │ 15 16 17 18 19 20 21        │ │
│ Wed  [ ] Closed              │  └──────────────────────────────┘ │
│ ...                          │  Jul 10: Pop-up @ Farmers Market  │
│                              │  Jul 15: Closed — vacation        │
│ Order cut-off: 24h before    │                                   │
│ Daily capacity: [ 20 ] orders│  Pickup windows (selected day)    │
│ Lead time min: [ 2 ] hours   │  ┌─────────────────────────────┐  │
│                              │  │ 4:00 PM – 6:00 PM · 12 max  │  │
│ Fulfillment:                 │  │ [+ Add window]              │  │
│ ● Pickup  ○ Delivery (future)│  └─────────────────────────────┘  │
├──────────────────────────────┴──────────────────────────────────┤
│                              [ Save changes ]  ← PRIMARY        │
└─────────────────────────────────────────────────────────────────┘
```

**Content hierarchy (top → bottom):**

1. Live status strip — current window and capacity remaining
2. Weekly recurring schedule — default production rhythm
3. Calendar — exceptions, closures, events
4. Day detail — pickup windows and per-day overrides
5. Global rules — cut-off, capacity, lead time, fulfillment type

---

## Components

| Component | Usage on this page | DS reference |
|-----------|-------------------|--------------|
| **Sidebar nav** | Persistent Creator OS navigation | [Navigation — Sidebar](../../design-system/components-overview.md#navigation) |
| **Status badge** | Live / draft / paused availability | [Badges — Status](../../design-system/components-overview.md#badges) |
| **Calendar** | Month view with exception markers | [Calendar](../../design-system/components-overview.md#calendar) |
| **Toggle** | Day open/closed; fulfillment type | [Toggles](../../design-system/components-overview.md#toggles) |
| **Time picker** | Window start/end, cut-off time | [Inputs — Time](../../design-system/components-overview.md#inputs) |
| **Number input** | Daily capacity, max per window | [Inputs — Number](../../design-system/components-overview.md#inputs) |
| **Primary button** | Save changes | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | Add window, add exception, preview | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Modal** | Confirm closure with active orders | [Modals](../../design-system/components-overview.md#modals) |
| **Warning banner** | Active orders conflict with closure | [Banners](../../design-system/components-overview.md#banners) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Day toggle** | Enable/disable recurring day; grey out pickup windows when closed |
| **Calendar day tap** | Select day; show exceptions and windows in detail panel |
| **Add exception** | Modal: closed, modified hours, pop-up location — date range supported |
| **Pickup window row** | Edit inline; drag to reorder; delete with confirm if orders exist |
| **Daily capacity** | Integer; validates against existing confirmed orders on save |
| **Save changes** | Validates conflicts; shows diff summary if orders affected; publishes to storefront |
| **Preview on storefront** | Opens [Creator Storefront](../customer/creator-storefront.md) in new tab with availability preview banner |
| **Food truck "Open now"** | Quick toggle in status strip — overrides schedule for current session only |
| **Keyboard** | Arrow keys navigate calendar; `Enter` opens day detail; form fields tab in logical order |

**Conflict rule:** Saving a closure that affects confirmed orders triggers modal — creator must contact customers via [Messages](./messages.md) or reschedule before confirm.

---

## Animations

| Trigger | Motion | Duration |
|---------|--------|----------|
| Page load | Calendar fade-in; schedule list slide from left | 200ms ease-out |
| Day select | Detail panel crossfade | 150ms |
| Save success | Status strip pulse green; toast | 300ms |
| Capacity warning | Banner slide down | 250ms |
| Window add | Accordion expand | 200ms |

Respect `prefers-reduced-motion`: instant state changes — [accessibility standards](../../design-system/accessibility-standards.md).

---

## Responsive Behaviour

| Breakpoint | Layout changes |
|------------|----------------|
| **Mobile (320–767px)** | Stack: status strip → weekly schedule accordion → calendar → day detail sheet (bottom drawer) |
| **Tablet (768–1023px)** | Schedule left column (40%); calendar + detail right |
| **Desktop (1024px+)** | Two-column layout as wireframe; sticky save bar on scroll |

Content parity: status strip and save action reachable on all breakpoints without horizontal scroll.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| **Full page (first visit)** | Skeleton: status strip, 7-day schedule rows, calendar grid |
| **Calendar month change** | Inline shimmer on grid cells |
| **Save** | Primary button spinner; disable form fields |
| **Day detail** | Skeleton window rows on first select |

Never show skeleton longer than 3s without inline retry.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Schedule fetch failed | "Couldn't load your availability" | Page-level retry |
| Save validation — capacity below orders | "You have 15 confirmed orders but capacity is set to 10" | Adjust capacity or cancel orders |
| Save validation — overlapping windows | "Pickup windows can't overlap" | Fix times inline |
| Save API failure | "Changes couldn't save. Try again." | Retry; preserve form state |
| Conflict with active orders on closure | Modal with affected order list | Link to [Orders](./orders.md) filtered by date |

---

## Empty States

| Scenario | Display | Primary action |
|----------|---------|----------------|
| **No schedule configured** | Illustration; "Customers can't order until you set pickup times" | [Set weekly schedule] — expands schedule editor |
| **No pickup windows on open day** | Warning inline on day: "Add at least one pickup window" | [Add window] |
| **No exceptions** | Calendar clean; subtle "+ Block dates or events" link | [Add exception] |
| **Paused availability** | Status strip: "Availability paused — storefront shows closed" | [Resume availability] |

Empty states are guidance, not errors — calm copy per [design principles](../../design-system/principles.md#2-whitespace-is-a-feature).

---

## Permissions

| Role | Access |
|------|--------|
| **Creator owner** | Full read/write; publish schedule |
| **Creator staff — orders** | Read-only schedule view |
| **Creator staff — kitchen** | Read-only; can see today's windows |
| **Unverified creator** | Configure draft schedule; not live on storefront |
| **Suspended creator** | Read-only; cannot publish changes |

---

## Analytics

| Event | Properties | Purpose |
|-------|------------|---------|
| `creator_availability_viewed` | `has_schedule`, `fulfillment_type` | Adoption baseline |
| `creator_availability_saved` | `days_open`, `window_count`, `daily_capacity` | Configuration patterns |
| `creator_availability_exception_added` | `exception_type` (closed, modified, event) | Exception frequency |
| `creator_availability_conflict_shown` | `conflict_type`, `affected_orders` | Friction tracking |
| `creator_availability_preview_clicked` | — | Storefront validation behavior |
| `creator_availability_open_now_toggled` | `enabled` | Food truck usage |

Funnel: first schedule save → first order within configured window.

---

## Accessibility

| Requirement | Implementation |
|-------------|----------------|
| **Page title** | `<h1>Availability</h1>` |
| **Calendar** | `role="grid"`; day buttons with `aria-label`: "July 10, closed, 2 exceptions" |
| **Schedule toggles** | Label includes day name and state |
| **Time pickers** | 24h or locale format; error text linked via `aria-describedby` |
| **Save button** | Announces unsaved changes via `aria-live="polite"` when form dirty |
| **Conflict modal** | Focus trap; first focus on summary; escape closes |
| **Touch targets** | Minimum 44×44px on calendar days and toggles |

---

## SEO

Not applicable — authenticated creator surface. `noindex, nofollow` on all `/creator/*` routes.

---

## Future Improvements

- Delivery zone editor and radius map
- Sync with external calendars (Google Calendar export)
- Smart capacity suggestions based on [Analytics](./analytics.md) order history
- Recurring pop-up event templates for food trucks
- Item-level availability overrides linked from [Catalog](./catalog.md)
- Customer waitlist when capacity full

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `GET /api/v1/creator/availability` | GET | Weekly schedule, rules, exceptions |
| `PUT /api/v1/creator/availability/schedule` | PUT | Recurring weekly schedule |
| `PUT /api/v1/creator/availability/rules` | PUT | Cut-off, capacity, lead time, fulfillment type |
| `POST /api/v1/creator/availability/exceptions` | POST | Closures, modified days, events |
| `DELETE /api/v1/creator/availability/exceptions/{id}` | DELETE | Remove exception |
| `GET /api/v1/creator/availability/conflicts` | GET | Preview conflicts before save (`?from=&to=`) |
| `PATCH /api/v1/creator/availability/open-now` | PATCH | Food truck session toggle |
| `GET /api/v1/creator/availability/public-preview` | GET | Storefront-facing availability snapshot |

Response SLA target: GET < 200ms p95. Save validates order conflicts server-side.

---

## Related Pages

- [Dashboard](./dashboard.md) — availability action items
- [Orders](./orders.md) — orders affected by schedule changes
- [Catalog](./catalog.md) — item-level availability (future)
- [Storefront Settings](./storefront-settings.md) — fulfillment defaults and pickup location
- [Analytics](./analytics.md) — capacity utilization trends
- [Messages](./messages.md) — notify customers of schedule changes
- [Creator Storefront](../customer/creator-storefront.md) — customer-facing availability display
