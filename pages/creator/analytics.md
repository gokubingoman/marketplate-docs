# Creator Analytics (Business Metrics)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/analytics`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Analytics page gives creators a **clear picture of business performance** — revenue, order volume, repeat customers, average order value, and fulfillment trends — without exporting to spreadsheets. It answers: *Is my business growing? Who comes back? What's working?*

Metrics link to actionable destinations ([Catalog](./catalog.md), [Reviews](./reviews.md), [Availability](./availability.md)) rather than displaying vanity numbers. Data reflects completed orders only; disputed or refunded orders excluded per [Marketplace Mechanics](../../product/marketplace-mechanics.md#commerce).

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| Track revenue and order trends over time | Increase GMV per creator |
| Identify repeat vs. new customers | Improve retention and LTV |
| Compare periods (this week vs. last) | Surface growth or decline early |
| See top-performing menu items | Guide catalog optimization |
| Understand fulfillment performance | Reduce late pickups and cancellations |

**Primary action on this screen:** Contextual — "View top items in catalog" when item data available, or "Share storefront" when traffic low but conversion healthy.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Meal Prep Business](../../product/personas.md#meal-prep-business) | Batch metrics; weekly cadence |
| **Secondary** | [Independent Chef](../../product/personas.md#independent-chef) | Revenue and repeat rate focus |
| **Secondary** | [Baker](../../product/personas.md#baker) | Seasonal trend awareness |
| **Anti-persona** | Platform ops analyst | Internal metrics live in [Admin Dashboard](../admin/admin-dashboard.md) |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Sidebar nav | "Analytics" |
| [Dashboard](./dashboard.md) | Revenue stat card "View details" |
| [Payouts](./payouts.md) | "See revenue breakdown" link |
| [Catalog](./catalog.md) | Item performance link (future) |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Catalog](./catalog.md) | Top items row tap |
| [Orders](./orders.md) | Order volume drill-down |
| [Reviews](./reviews.md) | Rating trend link |
| [Payouts](./payouts.md) | Net revenue vs. payout comparison |
| [Storefront Settings](./storefront-settings.md) | Low traffic → improve profile prompt |

### Breadcrumbs

`Dashboard → Analytics`

---

## Layout

Dashboard-style metrics with time range control and drill-down cards.

```
┌─────────────────────────────────────────────────────────────────┐
│ Dashboard → Analytics                                           │
├─────────────────────────────────────────────────────────────────┤
│ [ 7 days ] [ 30 days ] [ 90 days ] [ Custom ▾ ]    Export CSV   │
├─────────────────────────────────────────────────────────────────┤
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐            │
│ │ Revenue  │ │ Orders   │ │ Avg order│ │ Repeat   │            │
│ │ $4,280   │ │ 86       │ │ $49.77   │ │ 34%      │            │
│ │ ↑ 12%    │ │ ↑ 8%     │ │ ↓ 2%     │ │ ↑ 5 pts  │            │
│ └──────────┘ └──────────┘ └──────────┘ └──────────┘            │
├─────────────────────────────────────────────────────────────────┤
│ Revenue over time                                               │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ [area chart — daily revenue]                                │ │
│ └─────────────────────────────────────────────────────────────┘ │
├──────────────────────────────┬──────────────────────────────────┤
│ Top menu items               │ Customer mix                      │
│ 1. Sourdough loaf    $840    │ [donut] New 66% · Repeat 34%     │
│ 2. Meal prep box     $620    │                                   │
│ 3. ...                       │ Fulfillment                       │
│ [ View in catalog → ]        │ Pickup on time: 94%              │
│                              │ Avg prep time: 2.1 hrs           │
└──────────────────────────────┴──────────────────────────────────┘
```

**Content hierarchy:**

1. Time range selector — scopes all metrics
2. KPI stat cards — headline numbers with period comparison
3. Revenue chart — primary trend visualization
4. Top items + customer/fulfillment breakdown — actionable detail

---

## Components

| Component | Usage on this page | DS reference |
|-----------|-------------------|--------------|
| **Sidebar nav** | Persistent Creator OS navigation | [Navigation — Sidebar](../../design-system/components-overview.md#navigation) |
| **Segmented control** | Time range: 7d / 30d / 90d / custom | [Segmented control](../../design-system/components-overview.md#segmented-control) |
| **Dashboard stat card** | KPI metrics with delta indicators | [Cards — Dashboard stat](../../design-system/components-overview.md#cards) |
| **Chart — area** | Revenue over time | [Charts](../../design-system/components-overview.md#charts) |
| **Chart — donut** | New vs. repeat customer mix | [Charts](../../design-system/components-overview.md#charts) |
| **Data table** | Top items ranked list | [Tables](../../design-system/components-overview.md#tables) |
| **Ghost button** | Export CSV, drill-down links | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Date picker** | Custom range selection | [Inputs — Date](../../design-system/components-overview.md#inputs) |
| **Tooltip** | Metric definitions on hover | [Tooltips](../../design-system/components-overview.md#tooltips) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Time range toggle** | Refetch all metrics; update URL query `?range=30d` |
| **Custom range** | Date picker modal; max 365 days |
| **Stat card tap** | Scroll to relevant chart section or navigate to detail page |
| **Top item row** | Navigate to [Menu Item Editor](./menu-item-editor.md) for that item |
| **Export CSV** | Download current range data; includes revenue, orders, items — logged event |
| **Chart hover** | Tooltip with exact date and value |
| **Comparison deltas** | Green/red/neutral based on direction; tooltip explains calculation |
| **Keyboard** | Arrow keys on chart data points (table fallback for screen readers) |

**Data freshness:** Metrics cached 15 minutes; "Last updated" timestamp visible. Manual refresh via pull-to-refresh on mobile.

---

## Animations

| Trigger | Motion | Duration |
|---------|--------|----------|
| Page load | Stat cards fade-up stagger | 200ms |
| Range change | Chart crossfade | 300ms |
| Delta update | Number tick animation | 200ms |
| Export complete | Toast slide in | 250ms |

Respect `prefers-reduced-motion`: instant chart swap, no number tick.

---

## Responsive Behaviour

| Breakpoint | Layout changes |
|------------|----------------|
| **Mobile (320–767px)** | Stat cards 2×2 grid; chart full-width; sections stack |
| **Tablet (768–1023px)** | Stat cards 4-across; chart + breakdown side-by-side |
| **Desktop (1024px+)** | Full layout as wireframe |

Chart remains readable at 320px width — simplified axis labels on mobile.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| **Full page** | Skeleton stat cards + chart rectangle |
| **Range change** | Opacity pulse on updating cards; chart skeleton overlay |
| **Export** | Button spinner; disable duplicate export |
| **Partial failure** | Show available metrics; failed cards show retry |

Never show zero during load — use skeleton, not "0".

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Metrics API failure | "Analytics couldn't load right now" | Page-level retry |
| Partial metric failure | Failed card shows "—" with retry icon | Per-card retry |
| Export failed | "Export failed. Try again." | Retry button |
| Insufficient data for range | "Not enough data for this period" | Suggest wider range |
| Staff without revenue permission | Revenue cards hidden; message explains | Contact owner |

---

## Empty States

| Scenario | Display | Primary action |
|----------|---------|----------------|
| **Zero completed orders** | Illustration; "Analytics appear after your first completed order" | [View orders](./orders.md) |
| **New creator, orders in progress** | "You have 3 active orders — stats update when they complete" | [Orders](./orders.md) |
| **Range with no data** | "No orders in this period" | Widen range selector |
| **Single order only** | Show data with note: "More trends visible after 5+ orders" | — |

---

## Permissions

| Role | Access |
|------|--------|
| **Creator owner** | Full analytics including revenue |
| **Creator staff — orders** | Order volume and fulfillment metrics only; no revenue |
| **Creator staff — kitchen** | Fulfillment metrics only |
| **Unverified creator** | Empty state until first completed order |
| **Suspended creator** | Read-only historical data |

Revenue visibility enforced server-side — UI hides cards entirely for unauthorized roles.

---

## Analytics

| Event | Properties | Purpose |
|-------|------------|---------|
| `creator_analytics_viewed` | `range`, `order_count_in_range` | Engagement |
| `creator_analytics_range_changed` | `range`, `custom` (bool) | Usage patterns |
| `creator_analytics_stat_clicked` | `stat_type` | Drill-down interest |
| `creator_analytics_top_item_clicked` | `item_id`, `rank` | Catalog optimization funnel |
| `creator_analytics_exported` | `range`, `format` | Export demand |
| `creator_analytics_drilldown` | `destination` | Cross-page navigation |

Meta-analytics only — page itself is the analytics product for creators.

---

## Accessibility

| Requirement | Implementation |
|-------------|----------------|
| **Page title** | `<h1>Analytics</h1>` |
| **Charts** | Text summary below each chart; data table toggle |
| **Stat cards** | `aria-label` includes value and delta direction |
| **Color** | Deltas not color-only — include ↑/↓ text |
| **Export** | Announces download start via `aria-live="polite"` |
| **Time range** | Segmented control with `aria-pressed` states |

---

## SEO

Not applicable — authenticated creator surface. `noindex, nofollow`.

---

## Future Improvements

- Item-level performance deep dive from [Catalog](./catalog.md)
- Cohort analysis (customers who ordered 2+ times)
- Benchmark vs. platform average (anonymized)
- Traffic sources when storefront analytics integrated
- Goal setting ("Target $5k this month")
- AI insights: "Sourdough sells best on Saturdays"
- `TODO(decision):` Tier-gated advanced analytics per [IA open decisions](../information-architecture.md#open-decisions)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `GET /api/v1/creator/analytics/summary` | GET | KPI cards: revenue, orders, AOV, repeat rate + deltas |
| `GET /api/v1/creator/analytics/revenue` | GET | Time series: `?range=30d&granularity=day` |
| `GET /api/v1/creator/analytics/top-items` | GET | Ranked items by revenue/units: `?range=&limit=10` |
| `GET /api/v1/creator/analytics/customers` | GET | New vs. repeat breakdown |
| `GET /api/v1/creator/analytics/fulfillment` | GET | On-time rate, avg prep time |
| `GET /api/v1/creator/analytics/export` | GET | CSV download for range |

All endpoints respect role permissions (revenue fields omitted for staff). Cached 15 minutes.

---

## Related Pages

- [Dashboard](./dashboard.md) — summary stat cards
- [Payouts](./payouts.md) — net earnings and payout schedule
- [Orders](./orders.md) — order-level detail
- [Catalog](./catalog.md) — menu item management
- [Reviews](./reviews.md) — rating trends
- [Availability](./availability.md) — capacity vs. demand
- [Storefront Settings](./storefront-settings.md) — discovery optimization
