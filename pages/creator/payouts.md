# Creator Payouts (Earnings & Payout Schedule)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/payouts`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Payouts page shows creators **what they've earned, what's pending, and when money arrives** — gross revenue, platform fees, adjustments, and payout history linked to their connected bank account. It closes the loop between [Orders](./orders.md) fulfillment and getting paid.

Transparent earnings build creator trust and reduce "where's my money?" support volume. Payout holds tie to [Compliance](./compliance.md) and dispute status visible in summary banners.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| See current balance and next payout date | Reduce payout-related support tickets |
| Understand platform fees and net earnings | Transparent economics per marketplace model |
| Review payout history and individual transfers | Bookkeeping and tax preparation |
| Know why a payout is delayed or held | Clear enforcement — no silent holds |

**Primary action on this screen:** View payout details for the current or most recent period — or complete payout setup if not yet connected.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Independent Chef](../../product/personas.md#independent-chef) | Side income tracking |
| **Secondary** | [Meal Prep Business](../../product/personas.md#meal-prep-business) | Regular weekly payouts |
| **Secondary** | [Caterer](../../product/personas.md#caterer) | Large single-event payouts |
| **Anti-persona** | Platform finance team | Internal reconciliation uses separate admin tools |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Sidebar nav | "Payouts" — badge if pending setup or hold |
| [Dashboard](./dashboard.md) | Revenue context (no raw payout on dashboard for staff) |
| [Analytics](./analytics.md) | "View net earnings" / fee breakdown link |
| Email | "Your payout of $842.50 is on the way" |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Analytics](./analytics.md) | Gross revenue comparison |
| [Orders](./orders.md) | Order line in payout period drill-down |
| [Compliance](./compliance.md) | Payout hold banner — compliance issue |
| External Stripe Express | "Manage payout account" — `TODO(decision):` payment provider |

### Breadcrumbs

`Dashboard → Payouts`

---

## Layout

Summary-first layout: **balance card** at top, **payout schedule**, **transaction ledger** below.

```
┌─────────────────────────────────────────────────────────────────┐
│ Dashboard → Payouts                                             │
├─────────────────────────────────────────────────────────────────┤
│ ┌─ Balance summary ─────────────────────────────────────────────┐│
│ │ Available for payout      $842.50                           ││
│ │ Pending (in transit)      $0.00                             ││
│ │ On hold                   $120.00  ⓘ dispute #8821          ││
│ │ Next payout: Jul 7, 2026 (weekly schedule)                  ││
│ │ Bank account ···· 4521 ✓          [ Manage account ]        ││
│ └───────────────────────────────────────────────────────────────┘│
├─────────────────────────────────────────────────────────────────┤
│ This period (Jun 26 – Jul 2)                                    │
│ Gross sales    $980.00                                          │
│ Platform fee   −$98.00  (10%)                                   │
│ Adjustments    −$39.50  (refund #1039)                          │
│ Net earnings   $842.50                                          │
│ [ View in analytics → ]                                         │
├─────────────────────────────────────────────────────────────────┤
│ Payout history                                                  │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ Jul 7 · Scheduled · $842.50 · Processing                    │ │
│ │ Jun 30 · Paid · $756.20 · Bank ···· 4521                    │ │
│ │ Jun 23 · Paid · $612.00 · Bank ···· 4521                    │ │
│ └─────────────────────────────────────────────────────────────┘ │
│ [ Load more ]                                                   │
└─────────────────────────────────────────────────────────────────┘
```

**Content hierarchy:**

1. Balance summary — available, pending, holds
2. Current period breakdown — gross, fees, net
3. Payout history — chronological transfers
4. Account management link

---

## Components

| Component | Usage on this page | DS reference |
|-----------|-------------------|--------------|
| **Sidebar nav** | Creator OS navigation | [Navigation — Sidebar](../../design-system/components-overview.md#navigation) |
| **Dashboard stat card** | Balance, pending, on-hold amounts | [Cards — Dashboard stat](../../design-system/components-overview.md#cards) |
| **Status badge** | Paid, processing, scheduled, failed, on hold | [Badges — Status](../../design-system/components-overview.md#badges) |
| **Data table / list** | Payout history rows | [Tables](../../design-system/components-overview.md#tables) |
| **Info tooltip** | Fee explanation, hold reasons | [Tooltips](../../design-system/components-overview.md#tooltips) |
| **Warning banner** | Payout hold — compliance or dispute | [Banners](../../design-system/components-overview.md#banners) |
| **Primary button** | Complete payout setup (first time) | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | Manage account, view analytics | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Empty state** | No payouts yet | [Empty states](../../design-system/components-overview.md#empty-states) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Manage account** | Opens payment provider onboarding/dashboard (Stripe Connect Express) |
| **Payout row expand** | Show order IDs included, fee line items, transfer ID |
| **Hold info icon** | Tooltip + link to [Compliance](./compliance.md) or dispute context |
| **Period breakdown** | Static for current open period; links to [Analytics](./analytics.md) |
| **Load more** | Paginate history |
| **Export** | CSV of payout history for date range — ghost link |
| **First-time setup** | Primary CTA "Connect bank account" until onboarding complete |

**Payout schedule:** Weekly by default (configurable platform-wide in [Platform Settings](../admin/platform-settings.md)); displayed prominently, not buried.

---

## Animations

| Trigger | Motion | Duration |
|---------|--------|----------|
| Page load | Balance card fade-up | 200ms |
| Status change (paid) | Badge crossfade | 200ms |
| Row expand | Accordion | 250ms |
| Setup complete return | Success toast | 300ms |

Minimal motion — financial clarity over delight.

---

## Responsive Behaviour

| Breakpoint | Layout changes |
|------------|----------------|
| **Mobile (320–767px)** | Balance cards stacked; history full-width rows |
| **Tablet (768–1023px)** | Balance 2×2 grid |
| **Desktop (1024px+)** | Balance inline row; wider breakdown table |

Numbers never truncate — use responsive font scaling before ellipsis.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| **Balance summary** | Skeleton stat cards |
| **Period breakdown** | Skeleton lines |
| **History** | Skeleton rows (5) |
| **Manage account** | External redirect spinner |

Never show $0.00 for balance during load — use shimmer placeholders.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| **Payout data failed** | "Earnings couldn't load. Try again." | Retry |
| **Account disconnected** | Banner: "Reconnect your bank account to receive payouts" | [Manage account] |
| **Payout failed** | Row status "Failed" with reason from provider | Retry via manage account |
| **Hold unexplained** | "Payout on hold — contact support" with case ID | Support link |
| **Export failed** | Toast: "Export failed" | Retry |

---

## Empty States

| Scenario | Display | Primary action |
|----------|---------|----------------|
| **No bank connected** | "Connect your bank to get paid" | [Connect bank account] |
| **No orders yet** | "Earnings appear after your first completed order" | [View orders] |
| **No payout history** | "Your first payout arrives {date}" after first period | — |
| **Zero balance, account connected** | "No earnings this period" | [View analytics] |

---

## Permissions

| Role | Access |
|------|--------|
| **Creator owner** | Full payouts, account management, export |
| **Creator staff — orders** | No payouts access — nav hidden |
| **Creator staff — kitchen** | No access |
| **Unverified creator** | Setup allowed; payouts release after verification + first eligible orders |
| **Suspended creator** | Read-only history; new payouts held |

Financial data never exposed to staff roles in v1.

---

## Analytics

| Event | Properties | Purpose |
|-------|------------|---------|
| `creator_payouts_viewed` | `has_account`, `balance_cents`, `hold_cents` | Engagement |
| `creator_payouts_setup_started` | — | Activation funnel |
| `creator_payouts_setup_completed` | — | Time to first payout readiness |
| `creator_payouts_history_expanded` | `payout_id`, `status` | Detail interest |
| `creator_payouts_export` | `range` | Tax/bookkeeping behavior |
| `creator_payouts_hold_info_clicked` | `hold_reason` | Support deflection |

Funnel: first order completed → bank connected → first payout received.

---

## Accessibility

| Requirement | Implementation |
|-------------|----------------|
| **Page title** | `<h1>Payouts</h1>` |
| **Currency** | Screen reader friendly: "Available for payout: eight hundred forty-two dollars and fifty cents" |
| **Status badges** | Text labels: "Paid", "Processing", not color-only |
| **Hold banner** | `role="alert"` with actionable link |
| **History table** | Proper `<table>` semantics or list with labeled rows |
| **Manage account** | Opens external link with warning announced |

---

## SEO

Not applicable — authenticated creator surface. `noindex, nofollow`.

---

## Future Improvements

- Instant payout option (fee disclosed)
- Tax document center (1099)
- Multi-currency support for future markets
- Payout forecasting based on open orders
- Split payouts for multi-operator businesses
- Integration with accounting tools (QuickBooks export)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `GET /api/v1/creator/payouts/summary` | GET | Balance, pending, holds, next payout date |
| `GET /api/v1/creator/payouts/period` | GET | Current period gross/fees/net breakdown |
| `GET /api/v1/creator/payouts/history` | GET | Paginated payout transfers |
| `GET /api/v1/creator/payouts/history/{id}` | GET | Line items: orders, fees, adjustments |
| `GET /api/v1/creator/payouts/account-link` | GET | URL to payment provider dashboard |
| `POST /api/v1/creator/payouts/account/onboard` | POST | Start Connect onboarding |
| `GET /api/v1/creator/payouts/export` | GET | CSV history |

Holds sync from [Compliance](./compliance.md) status and open [Dispute Detail](../admin/dispute-detail.md) cases — exposed in summary `holds[]` with reason codes.

---

## Related Pages

- [Dashboard](./dashboard.md) — revenue overview (owner only)
- [Analytics](./analytics.md) — gross revenue and trends
- [Orders](./orders.md) — orders in payout periods
- [Compliance](./compliance.md) — compliance-related payout holds
- Admin: [Creator Admin Detail](../admin/creator-admin-detail.md) — payout hold operator view
- Admin: [Dispute Detail](../admin/dispute-detail.md) — dispute holds
- Admin: [Platform Settings](../admin/platform-settings.md) — fee rates and payout schedule
