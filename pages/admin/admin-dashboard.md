# Admin Dashboard

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Admin (Internal)  
**Route:** `/admin`

---

## Purpose

The Admin Dashboard is the operational home for Marketplate internal teams — Trust & Safety, Creator Success, and Marketplace Operations. It surfaces queue counts, platform health metrics, and actionable alerts so operators can prioritize human approval work and maintain marketplace integrity.

This page exists because internal ops tooling must meet the same quality bar as customer-facing product per [Operational Excellence Is Respect](../../company/values.md#5-operational-excellence-is-respect). AI recommends; humans approve on verification and moderation.

---

## Goals

**User goals:**
- See at a glance what needs attention today (verification backlog, disputes, moderation)
- Monitor platform health trends without exporting to spreadsheets
- Jump directly into highest-priority queues
- Understand SLA status for trust-critical workflows

**Business goals:**
- Reduce verification and dispute resolution time
- Surface anomalies early (fraud spikes, compliance expirations)
- Provide executive-visible trust metrics snapshot
- Every metric links to auditable detail — not vanity numbers

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [Platform Operations (Internal)](../../product/personas.md#platform-operations-internal) | Trust & Safety analysts, ops leads |
| **Secondary:** Creator Success managers | Creator activation and verification support |
| **Secondary:** Leadership | Read-only health overview — `TODO(decision):` role-based widget visibility |
| **Anti-persona:** Creators and customers | No access — separate auth boundary |

---

## Navigation

**Arrival paths:**
- Post admin login default landing
- Global admin sidebar → "Dashboard"
- Bookmark `/admin`

**Exit paths:**
- Queue stat cards → [Verification Queue](verification-queue.md), [Moderation Queue](moderation-queue.md)
- Alert rows → [Dispute Detail](dispute-detail.md), [Creator Admin Detail](creator-admin-detail.md)
- Settings gear → [Platform Settings](platform-settings.md)
- Sidebar nav to all admin sections

---

## Layout

Full-width admin shell: left sidebar nav + main content grid.

```
┌──────────┬──────────────────────────────────────────────────────────┐
│ Admin    │  Dashboard                          Last updated: 2m ago  │
│ nav      │                                                          │
│          │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐        │
│ Dashboard│  │ Verif.  │ │ Modera- │ │ Disputes│ │ Creators│        │
│ Verif.   │  │ queue   │ │ tion    │ │ open    │ │ pending │        │
│ Modera-  │  │   47    │ │   12    │ │    8    │ │ activation│      │
│ Disputes │  │ ↑ SLA   │ │         │ │ 2 urgent│ │   23    │        │
│ Settings │  └─────────┘ └─────────┘ └─────────┘ └─────────┘        │
│          │                                                          │
│          │  Platform health (7 days)                                │
│          │  ┌────────────────────────────────────────────────────┐  │
│          │  │ [sparkline] Verification turnaround: 1.4 days    │  │
│          │  │ [sparkline] Dispute resolution: 2.1 days           │  │
│          │  │ [sparkline] Order dispute rate: 0.8%             │  │
│          │  └────────────────────────────────────────────────────┘  │
│          │                                                          │
│          │  Requires attention                                      │
│          │  ┌────────────────────────────────────────────────────┐│
│          │  │ ⚠ 5 identity reviews past SLA · View queue →        ││
│          │  │ ⚠ 3 compliance docs expired · View creators →       ││
│          │  │ ● 2 disputes flagged urgent · View →                ││
│          │  └────────────────────────────────────────────────────┘│
│          │                                                          │
│          │  Recent admin activity (audit feed)                       │
│          │  Jane approved kitchen verification · Creator #4821 · 2m│
└──────────┴──────────────────────────────────────────────────────────┘
```

**Hierarchy:** Action queues → health trends → alerts → audit feed.

Progressive disclosure — no dense default tables on dashboard per [design principles](../../design-system/principles.md).

---

## Components

| Component | Usage |
|-----------|-------|
| **Sidebar nav** | Admin section links |
| **Dashboard stat card** | Queue counts with SLA indicator |
| **Status badge** | SLA ok / warning / breached |
| **Cards** | Health metric groups, alert list |
| **Ghost / text links** | "View queue →" on each stat |
| **Badges** | Urgent dispute count, past-SLA count |
| **Pagination** | Audit feed (load more) |
| **Segmented control** | Time range: 24h / 7d / 30d for health charts |
| **Toast** | Real-time alert when new urgent item — optional |

Data tables deferred to queue pages — dashboard uses cards and links only.

---

## Interactions

| Action | Behavior |
|--------|----------|
| Stat card click | Navigate to filtered queue view |
| Alert row click | Deep link to specific case or filtered list |
| Time range toggle | Refetch health metrics |
| Audit feed item click | Open related [Creator Admin Detail](creator-admin-detail.md) or case |
| Refresh | Manual refresh + auto-refresh every 2 min when tab active |
| SLA badge hover | Tooltip with SLA definition and current median |

All operator actions elsewhere log to audit — dashboard feed is read-only mirror.

---

## Animations

| Element | Motion |
|---------|--------|
| Stat count update | Number tick 200ms on poll — subtle |
| New alert | Slide in 300ms; no sound |
| Chart range change | Crossfade 300ms |
| Page load | Stagger stat cards 50ms delay — disabled with reduced motion |

Functional motion only.

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Admin mobile supported but secondary; sidebar collapses to hamburger; stat cards 2×2 grid |
| **Tablet** | Sidebar collapsible; single column stats |
| **Desktop** | Full layout — primary ops context |

Ops workflows optimized for desktop 1280px+; mobile for urgent approvals only.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Initial load | Skeleton stat cards + alert list |
| Metric refresh | Subtle opacity pulse on updating cards |
| Partial failure | Show cached counts with warning: "Some metrics unavailable" |
| Audit feed | Infinite scroll skeleton rows |

Never show zero falsely — distinguish loading from empty.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Metrics API failure | "Platform health metrics couldn't load. Retry." | Retry button |
| Partial queue count failure | Show "—" for failed card with retry icon | Per-card retry |
| Unauthorized | Redirect to admin login | Re-auth |
| Session expired | Banner + redirect | Login |

Internal copy can be slightly more technical than creator-facing — still calm and precise.

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| All queues empty | Stat cards show "0" with green SLA badge — "All caught up" message in alerts section |
| No urgent items | "Requires attention" section: "No urgent items right now." |
| Audit feed empty | "No recent activity." — unlikely in production |

Empty queues are **positive state** — not styled as errors.

---

## Permissions

| Role | Access |
|------|--------|
| **Trust & Safety** | Full dashboard; all queue links |
| **Creator Success** | Verification + creator activation widgets; limited moderation — `TODO(decision):` RBAC matrix |
| **Read-only leadership** | Health metrics + audit feed; no queue actions |
| **Engineering admin** | May see platform health + link to [Platform Settings](platform-settings.md) |

Role-based widget visibility enforced server-side — not client-only hide.

---

## Analytics

| Event | Properties |
|-------|------------|
| `admin.dashboard.view` | `role` |
| `admin.dashboard.queue_click` | `queue_type` |
| `admin.dashboard.alert_click` | `alert_type` |
| `admin.dashboard.time_range_change` | `range` |

Internal analytics — not customer-facing tracking. Audit log for all admin sessions.

---

## Accessibility

- Stat cards are links with descriptive text: "Verification queue: 47 items, SLA warning"
- Charts have text alternatives / data table toggle
- Alert list uses semantic list; urgency not color-only
- Sidebar keyboard navigable; skip link to main content
- Auto-refresh announces via `aria-live="polite"` when counts change significantly

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Admin Dashboard — Marketplate |
| `meta robots` | `noindex, nofollow` |
| Auth | Internal SSO / VPN — `TODO(decision):` |

Not publicly discoverable.

---

## Future Improvements

- Customizable dashboard widgets per role
- Real-time websocket updates for urgent disputes
- Anomaly detection alerts (fraud clustering)
- Geographic breakdown when multi-market
- SLA configuration UI linked to [Platform Settings](platform-settings.md)
- Export daily ops report PDF

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/admin/dashboard/summary` | GET | Queue counts, SLA status |
| `/api/v1/admin/dashboard/health` | GET | Trend metrics with `?range=7d` |
| `/api/v1/admin/dashboard/alerts` | GET | Actionable alert list |
| `/api/v1/admin/audit/feed` | GET | Recent admin actions paginated |

**Response (summary):**
```json
{
  "queues": {
    "verification": { "count": 47, "sla_status": "warning", "median_age_hours": 36 },
    "moderation": { "count": 12, "sla_status": "ok" },
    "disputes": { "count": 8, "urgent": 2 },
    "creator_activation": { "count": 23 }
  }
}
```

Cached 60s; audit feed real-time preferred.

---

## Related Pages

- [Verification Queue](verification-queue.md)
- [Moderation Queue](moderation-queue.md)
- [Dispute Detail](dispute-detail.md)
- [Creator Admin Detail](creator-admin-detail.md)
- [Platform Settings](platform-settings.md)
- Creator-facing: [Identity Verification](../auth/identity-verification.md), [Kitchen Verification](../auth/kitchen-verification.md), [Compliance Center](../auth/compliance-center.md)
