# Dashboards

> Dashboard specifications by audience — widgets, metrics, cadence, and data sources.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Analytics · Product

---

## Purpose

This document specifies **who sees what metrics, when, and from which sources**. Metric formulas live in [Metrics Definitions](metrics-definitions.md); events that feed dashboards live in [Event Taxonomy](event-taxonomy.md).

Dashboards are organized by **audience**, not by tool. Implementation may use a BI tool (`TODO(decision):`), Metabase on read replica, or embedded admin views — widget specs here are tool-agnostic.

**Design principle:** Trust metrics appear alongside growth metrics on every leadership-facing dashboard. No GMV-only views.

---

## Dashboard Index

| Dashboard | Primary audience | Cadence | Access tier |
|-----------|------------------|---------|-------------|
| [Executive](#executive-dashboard) | Leadership, Board | Weekly (+ daily trust alert) | Executive |
| [Trust & Safety](#trust--safety-dashboard) | Trust & Safety analysts | Daily | T&S, Leadership (read-only) |
| [Creator Success](#creator-success-dashboard) | CS, Creator Success | Weekly | CS, Product, T&S |
| [Product](#product-dashboard) | Product, Design | Weekly | Product, Engineering |
| [Platform Operations](#platform-operations-dashboard) | Engineering, Ops | Real-time + weekly | Engineering, Ops, T&S |
| [Creator (in-app)](#creator-in-app-analytics) | Verified creators | Self-serve | Creator owner/staff |

Reporting cadence aligns with [Success Metrics — Reporting Cadence](../product/success-metrics-overview.md#reporting-cadence) and [CS Reporting](../docs/customer-success/success-metrics.md#reporting-cadence).

---

## Executive Dashboard

**Audience:** CEO, COO, VP Product, Board (monthly export)  
**Cadence:** Weekly business review (Monday); daily trust incident email if threshold breached  
**Owner:** Analytics · Product  
**Tool:** `TODO(decision):` BI / executive summary doc

### Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  NORTH STAR                          TRUST GUARDRAILS (equal weight) │
│  ┌─────────────────┐  ┌──────────────┐ ┌──────────────┐ ┌─────────┐ │
│  │ Verified GMV    │  │ Trust incident│ │ Order compl. │ │ Dispute │ │
│  │ $XXX,XXX ↑12%   │  │ 0.4 / 1k ↓   │ │ 98.2%        │ │ 0.7%    │ │
│  └─────────────────┘  └──────────────┘ └──────────────┘ └─────────┘ │
├─────────────────────────────────────────────────────────────────────┤
│  NORTH STAR INPUTS (weekly)                                          │
│  Active verified creators w/ orders · Repeat rate 30d · Retention    │
├─────────────────────────────────────────────────────────────────────┤
│  [Verified GMV trend — 12 weeks]    [Supply vs demand by market]     │
├─────────────────────────────────────────────────────────────────────┤
│  ANOMALY FLAGS                                                       │
│  ⚠ GMV ↑ 15% WoW but trust incident rate ↑ 40% — INTEGRITY REVIEW   │
└─────────────────────────────────────────────────────────────────────┘
```

### Widgets

| Widget | Metric ID | Visualization | Comparison |
|--------|-----------|---------------|------------|
| Verified GMV | `metric.verified_gmv` | Big number + sparkline | WoW, YoY when available |
| Trust incident rate | `metric.trust_incident_rate` | Big number | WoW; **red if ↑ with GMV ↑** |
| Order completion rate | `metric.order_completion_rate` | Big number | WoW; target line at 98% |
| Dispute rate | `metric.dispute_rate` | Big number | WoW |
| Active verified creators with orders | `metric.active_verified_creators_with_orders` | Count | WoW |
| Repeat customer rate (30d) | `metric.repeat_customer_rate_30d` | Percentage | WoW |
| Creator retention (monthly) | `metric.creator_retention_monthly` | Percentage | MoM |
| Verified GMV trend | `metric.verified_gmv` | Area chart, 12 weeks | — |
| Supply-demand ratio | `metric.supply_demand_ratio` | Bar by market | Balanced band overlay |
| Integrity crisis flag | Derived | Alert banner | GMV ↑ + trust ↓ |

### Alerts

| Condition | Channel | Recipient |
|-----------|---------|-----------|
| Trust incident rate > 2× 4-week median | Email + Slack | Leadership, T&S |
| Order completion rate < 96% for 3 days | Slack | Leadership, CS, Engineering |
| Verified GMV WoW ↓ > 25% | Email | Leadership, Product |
| Any confirmed food safety incident | Immediate page | Leadership, T&S, Legal |

### Data sources

- Verified GMV, completion rate: `orders` fact table + domain events
- Trust incidents: `trust_incidents` + [Food Safety SOP](../operations/food-safety-incident-sop.md)
- Repeat rate: cohort query — [Metrics Definitions](metrics-definitions.md#repeat-purchase-rate-30-day)

---

## Trust & Safety Dashboard

**Audience:** Trust & Safety analysts, ops leads  
**Cadence:** Daily standup; real-time queue widgets  
**Owner:** Trust & Safety · Analytics  
**Page spec reference:** [Admin Dashboard](../pages/admin/admin-dashboard.md)

### Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  QUEUES (now)                                                        │
│  Verification: 47 ⚠ SLA  │  Moderation: 12  │  Disputes: 8 (2 urg) │
├─────────────────────────────────────────────────────────────────────┤
│  TRUST METRICS (7d / 30d toggle)                                     │
│  Incident rate · Dispute rate · Review fraud rate · Compliance %     │
├─────────────────────────────────────────────────────────────────────┤
│  SLA TRACKERS                                                        │
│  Verification turnaround · Dispute resolution · Moderation TTR     │
├─────────────────────────────────────────────────────────────────────┤
│  REQUIRES ATTENTION                                                  │
│  Past-SLA items · Expired compliance · Urgent disputes               │
└─────────────────────────────────────────────────────────────────────┘
```

### Widgets

| Widget | Metric ID | Drill-down |
|--------|-----------|------------|
| Verification queue depth | `metric.verification_queue_depth` | [Verification Queue](../pages/admin/verification-queue.md) |
| Moderation queue depth | `metric.moderation_queue_depth` | [Moderation Queue](../pages/admin/moderation-queue.md) |
| Open disputes | Count + urgent badge | [Dispute Detail](../pages/admin/dispute-detail.md) |
| Trust incident rate | `metric.trust_incident_rate` | Incident list by type |
| Dispute rate | `metric.dispute_rate` | By outcome, creator persona |
| Dispute resolution SLA | `metric.dispute_resolution_sla` | Past-SLA cases |
| Verification SLA adherence | `metric.verification_sla_adherence` | [Verification Review SOP](../operations/verification-review-sop.md) |
| Compliance doc currency | `metric.compliance_doc_currency_rate` | Creators with expired docs |
| Review fraud detection rate | `metric.review_fraud_detection_rate` | Flagged reviews |
| Verified-purchase review ratio | `metric.verified_purchase_review_ratio` | Non-linked reviews |
| Listing completeness rate | `metric.listing_completeness_rate` | Incomplete listings |
| Account suspension rate | `metric.account_suspension_rate` | [Creator Suspension SOP](../operations/creator-suspension-sop.md) |
| AI assist acceptance rate | `metric.ai_assist_acceptance_rate` | [Verification Assist](../ai/verification-assist.md) |

### Events (real-time)

| Admin event | Dashboard use |
|-------------|---------------|
| `admin.verification.approve` / `reject` | Queue count decrement |
| `admin.moderation.decision` | Moderation throughput |
| `admin.dispute.resolve` | Resolution time tracking |

Cache: 60 seconds for queue counts; audit feed near-real-time preferred.

---

## Creator Success Dashboard

**Audience:** Customer Success, Creator Success managers  
**Cadence:** Weekly CS review; daily at-risk monitor  
**Owner:** Customer Success · Analytics  
**CS context:** [Customer Success Metrics](../docs/customer-success/success-metrics.md)

### Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  ACTIVATION FUNNEL (14d / 30d cohorts)                               │
│  Verified → First listing → First order                              │
├─────────────────────────────────────────────────────────────────────┤
│  AT-RISK CREATORS                                                    │
│  No listing @ day 14: 23  │  Health score red: 15  │  By persona     │
├─────────────────────────────────────────────────────────────────────┤
│  QUALITY & RETENTION                                                 │
│  Completion rate · On-time ready · Creator retention · WAC           │
├─────────────────────────────────────────────────────────────────────┤
│  INTERVENTIONS                                                       │
│  Outreach SLA · Resolution rate · Reactivation                        │
└─────────────────────────────────────────────────────────────────────┘
```

### Widgets

| Widget | Metric ID | CS target | Action trigger |
|--------|-----------|-----------|----------------|
| Verification completion rate | `metric.verification_completion_rate` | ≥70% | Funnel review if ↓ |
| First listing published rate (14d) | `metric.first_listing_published_rate` | ≥80% | Day-14 outreach |
| First order received rate (30d) | `metric.first_order_received_rate` | ≥50% | Share coaching |
| Verification drop-off by step | `metric.verification_dropoff_by_step` | ↓ per step | Step-specific sequences |
| At-risk creator count | Health score <60 | ↓ | [Retention & Expansion](../docs/customer-success/retention-and-expansion.md) |
| Creator health distribution | Green / yellow / red % | ↑ green | Weekly review |
| Order completion rate | `metric.order_completion_rate` | ≥98% | Fulfillment coaching |
| On-time ready rate | `metric.on_time_ready_rate` | ≥95% | Capacity review |
| Creator retention (monthly) | `metric.creator_retention_monthly` | ↑ MoM | Persona-specific intervention |
| GMV per active creator | `metric.gmv_per_active_creator` | ↑ | Expansion motions |
| Intervention resolution rate | CS CRM | ≥40% | Process audit |
| Activation outreach SLA | CS ops | ≥95% | Ops escalation |

### Persona segmentation

All widgets filterable by [persona](../product/personas.md). Quarterly persona review mandatory.

→ Metric → action map: [CS Success Metrics](../docs/customer-success/success-metrics.md#metric--action-map)

---

## Product Dashboard

**Audience:** Product managers, designers, growth  
**Cadence:** Weekly product review  
**Owner:** Product · Analytics

### Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  CUSTOMER FUNNEL (weekly)                                            │
│  Search → Storefront → Cart → Checkout → Order                     │
├─────────────────────────────────────────────────────────────────────┤
│  CREATOR FUNNEL (weekly)                                             │
│  Signup → Verify → List → First order                              │
├─────────────────────────────────────────────────────────────────────┤
│  FEATURE ADOPTION & ENGAGEMENT                                       │
│  Creator analytics usage · Storefront shares · Review submission   │
├─────────────────────────────────────────────────────────────────────┤
│  COHORT RETENTION                                                    │
│  Customer 30d/90d repeat · Creator monthly retention                 │
└─────────────────────────────────────────────────────────────────────┘
```

### Widgets

| Widget | Metric / funnel | Source events |
|--------|-----------------|---------------|
| Search success rate | `metric.search_success_rate` | `search_executed`, `search_result_clicked` |
| Zero-result search rate | `metric.zero_result_search_rate` | `search_zero_results` |
| Profile → cart rate | `funnel.profile_to_cart_rate` | Storefront, cart events |
| Cart → checkout rate | `funnel.cart_to_checkout_rate` | [Cart](../pages/customer/cart.md) events |
| Checkout → order rate | `funnel.checkout_to_order_rate` | [Checkout](../pages/customer/checkout.md) events |
| Fulfillment step abandonment | `funnel.fulfillment_abandonment_rate` | `checkout_abandoned` |
| Registered → first order | CS metric | Registration cohort |
| Creator activation funnel | Full funnel visualization | Onboarding events |
| Feature: creator analytics adoption | `creator_analytics_viewed` / active creators | Meta-analytics |
| Feature: storefront share rate | `storefront_share`, `creator_storefront_link_copied` | Creator marketing |
| Review submission rate | `metric.review_submission_rate` | Post-order review flow |
| CSAT trend | `metric.csat` | Survey pipeline |
| Browse-to-order (market) | `metric.browse_to_order_rate` | Liquidity |

### Experiment overlay

When A/B tests run, product dashboard supports:

- Experiment ID filter on all funnel widgets
- Statistical significance indicator (95% default)
- Segment by persona and market

`TODO(decision):` Feature flag / experiment platform.

---

## Platform Operations Dashboard

**Audience:** Engineering, SRE, platform ops  
**Cadence:** Real-time for golden signals; weekly reliability review  
**Owner:** Engineering · Analytics

**Split rule:** Infrastructure metrics (latency, CPU, errors) live in **observability stack** — Datadog, Grafana, etc. This dashboard covers **business-technical hybrid metrics** only. See [Infrastructure Overview](../engineering/infrastructure-overview.md#observability-stack).

### Widgets

| Widget | Metric ID | SLO / target |
|--------|-----------|--------------|
| Platform uptime | `metric.platform_uptime` | 99.9% |
| Checkout error rate | `metric.checkout_error_rate` | ↓ |
| Payment success rate | `metric.payment_success_rate` | ≥99% |
| Payout success rate | `metric.payout_success_rate` | ↑ |
| Search latency p95 | `metric.search_latency_p95` | <300ms |
| Notification delivery rate | `metric.notification_delivery_rate` | ↑ |
| Event bus queue depth | Infrastructure | Alert on backlog |
| Webhook processing lag | Infrastructure SLO | <60s p99 |
| Checkout funnel failure breakdown | `checkout_failed` by `error_code` | Engineering triage |
| Failed verification gates | Trust module | Should be ~0 false positives |

### Alert routing

Per [Architecture Overview — Monitoring](../engineering/architecture-overview.md#monitoring):

| Severity | Condition | Route |
|----------|-----------|-------|
| P1 | Payment/trust/checkout outage | PagerDuty |
| P2 | Discovery degradation | Engineering Slack |
| P3 | Notification delay | Ops ticket |

---

## Creator In-App Analytics

**Audience:** Verified creators (self-serve)  
**Cadence:** On demand; 15-minute cache  
**Owner:** Product · Engineering  
**Page spec:** [Creator Analytics](../pages/creator/analytics.md)

Not an internal BI dashboard — implemented as Creator OS page with API-backed widgets.

| Widget | Data | Permission |
|--------|------|------------|
| Revenue | Creator-scoped completed order GMV | Owner only |
| Orders | Count | Owner + staff |
| Average order value | Derived | Owner only |
| Repeat customer rate | Creator-scoped | Owner only |
| Revenue chart | Time series | Owner only |
| Top menu items | By revenue/units | All roles |
| Fulfillment stats | On-time rate, avg prep | All roles |
| Customer mix | New vs repeat donut | Owner only |

Export: CSV via `GET /api/v1/creator/analytics/export` — logged as `creator_analytics_exported`.

Internal platform metrics **never** appear on creator dashboard — see [Admin Dashboard](../pages/admin/admin-dashboard.md) anti-persona note.

---

## Weekly Business Review Template

Used in executive and cross-functional reviews:

| Section | Metrics | Owner |
|---------|---------|-------|
| **North star** | Verified GMV + WoW | Product |
| **Trust guardrails** | Incident rate, completion rate, dispute rate | T&S |
| **Supply** | Active verified creators, activation funnel, retention | CS + Product |
| **Demand** | Repeat rate, customer funnel, CSAT | Product + CS |
| **Anomalies** | Flags from integrity crisis rule | Analytics |
| **Actions** | Decisions and owners | All |

---

## Dashboard Access Matrix

| Role | Executive | T&S | Creator Success | Product | Platform Ops | Creator in-app |
|------|-----------|-----|-----------------|---------|--------------|----------------|
| Leadership | ✓ | Read | Read | Read | — | — |
| Trust & Safety | Read | ✓ | Read | — | Read | — |
| Creator Success | — | Read | ✓ | Read | — | — |
| Product | Read | Read | Read | ✓ | Read | — |
| Engineering | — | Read | — | Read | ✓ | — |
| Creator owner | — | — | — | — | — | ✓ |
| Creator staff | — | — | — | — | — | Partial |

Access enforced via BI tool RBAC + row-level security on warehouse. See [Data Governance — Access control](data-governance.md#access-control).

---

## Implementation Notes

| Topic | Guidance |
|-------|----------|
| **Cache TTL** | Executive: 1 hour; T&S queues: 60s; Creator in-app: 15 min |
| **Timezone** | All internal dashboards UTC; creator in-app uses creator locale |
| **Historical data** | Launch day = day 0; no backfill of pre-launch test data |
| **Row-level security** | Creators see only own data; CS sees market-scoped aggregates |
| **Export** | Executive PDF weekly; CS CSV export; audit log on sensitive exports |

---

## Related Documents

- [Metrics Definitions](metrics-definitions.md)
- [Event Taxonomy](event-taxonomy.md)
- [Data Governance](data-governance.md)
- [Success Metrics Overview](../product/success-metrics-overview.md)
- [Customer Success Metrics](../docs/customer-success/success-metrics.md)
- [Admin Dashboard](../pages/admin/admin-dashboard.md)
- [Creator Analytics](../pages/creator/analytics.md)
- [Infrastructure Overview](../engineering/infrastructure-overview.md)
