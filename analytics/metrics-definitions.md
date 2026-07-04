# Metrics Definitions

> Canonical metric definitions — one source of truth for formulas, data sources, and segmentation.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Analytics · Product

---

## Purpose

This document is the **authoritative implementation reference** for every KPI reported on Marketplate dashboards. [Success Metrics Overview](../product/success-metrics-overview.md) defines strategy and targets; this document defines **exact formulas**, **data sources**, **filters**, and **edge cases** so dashboards do not drift.

[Customer Success Metrics](../docs/customer-success/success-metrics.md) adds CS operational targets — it references definitions here, never redefines formulas.

**Rule:** If a metric appears on a dashboard, it must link to a definition in this document.

---

## Conventions

### Time windows

| Window | Definition |
|--------|------------|
| **Daily** | UTC midnight to midnight |
| **Weekly (WBR)** | Monday 00:00 UTC – Sunday 23:59 UTC |
| **Monthly** | Calendar month UTC |
| **Rolling 30-day** | Trailing 30 × 24 hours from report timestamp |
| **Cohort** | Anchor event date (e.g., verification date, first order date) |

### Segmentation dimensions

All metrics support these cuts where volume permits:

| Dimension | Source | Notes |
|-----------|--------|-------|
| `persona` | `creators.persona_type` | See [Personas](../product/personas.md) |
| `geography` | `creators.market_id` / customer address | `TODO(decision):` launch market |
| `surface` | Event property `surface` | `customer`, `creator`, `admin` |
| `acquisition_channel` | First-touch attribution | Organic, paid, creator-referral |
| `verification_status` | Point-in-time snapshot | Critical for Verified GMV |

### Status filters (orders)

| Status | Included in GMV | Included in funnel denominators |
|--------|-----------------|--------------------------------|
| `completed` | ✓ | ✓ (success) |
| `confirmed` (not yet completed) | ✗ | ✓ (in-progress funnel) |
| `cancelled` (platform) | Excluded from GMV sum | ✓ (cancellation rate) |
| `cancelled` (customer, pre-fulfillment) | ✗ | ✓ |
| `refunded` (full) | Excluded if previously counted | ✓ (refund rate) |
| `disputed` | Per refund outcome | ✓ (dispute rate) |

Disputed or refunded orders are **excluded from creator-facing revenue metrics** per [Creator Analytics page](../pages/creator/analytics.md).

---

## North Star

### Verified GMV

**ID:** `metric.verified_gmv`  
**Owner:** Product · Analytics  
**Cadence:** Daily aggregate; weekly executive reporting

**Definition:** Total value of orders completed on Marketplate where the selling creator held **active verified status** (identity + kitchen + compliance) at the time of order placement.

**Formula:**

```sql
SELECT SUM(o.subtotal_cents + o.fee_cents - o.platform_cancelled_cents) / 100.0
FROM orders o
JOIN creators c ON o.creator_id = c.id
WHERE o.status = 'completed'
  AND o.creator_verification_status_at_order = 'verified'
  AND o.completed_at BETWEEN :start AND :end
```

**Equivalent event derivation:** Sum `order.completed` domain events where `payload.creator_verification_status = verified` and `payload.subtotal + payload.fees - payload.platform_cancellations`.

**Why unverified supply is excluded:** Aligns with [Marketplace Mechanics — Verified to sell](../product/marketplace-mechanics.md#marketplace-model-overview). GMV from unverified creators is tracked separately as a **diagnostic only** — never reported as success.

**Supporting north star inputs (weekly):**

| Input | ID | Formula summary |
|-------|-----|-----------------|
| Active verified creators with ≥1 order | `metric.active_verified_creators_with_orders` | Distinct `creator_id` with completed order in period AND verified at order time |
| Repeat customer rate (30-day) | `metric.repeat_customer_rate_30d` | See [Customer Retention](#repeat-purchase-rate-30-day) |
| Order completion rate | `metric.order_completion_rate` | See [Creator Quality](#order-completion-rate) |
| Trust incident rate | `metric.trust_incident_rate` | See [Trust Metrics](#trust-incident-rate) |

**Crisis rule:** If Verified GMV ↑ while trust incident rate ↑ or order completion rate ↓, flag as **integrity crisis** on executive dashboard — not success.

→ Dashboard: [Executive Dashboard](dashboards.md#executive-dashboard)

---

## Funnel Metrics

Funnel metrics measure conversion through defined user journeys. Each funnel specifies entry event, success event, and allowed maximum window.

### Customer purchase funnel

**Purpose:** Measure demand quality from discovery to completed order.  
**Page specs:** [Customer Purchase Flow](../pages/flows/customer-purchase-flow.md), [Checkout](../pages/customer/checkout.md), [Cart](../pages/customer/cart.md)

| Step | Metric ID | Numerator | Denominator | Window | Events |
|------|-----------|-----------|-------------|--------|--------|
| Search success | `funnel.search_success_rate` | Searches with ≥1 result click | Total searches | Session | `search_executed` → `search_result_clicked` |
| Profile → cart | `funnel.profile_to_cart_rate` | Sessions with add-to-cart | Creator profile views | Session | `page_view` (storefront) → `item_add_to_cart` |
| Cart → checkout | `funnel.cart_to_checkout_rate` | Checkouts started | Carts with ≥1 item | 7 days | `cart_checkout_started` / `page_view` (cart) |
| Checkout → order | `funnel.checkout_to_order_rate` | Orders placed | Checkouts started | Session | `checkout_order_placed` / `cart_checkout_started` |
| Fulfillment abandonment | `funnel.fulfillment_abandonment_rate` | Checkout abandoned at fulfillment step | Checkouts reaching fulfillment step | Session | `checkout_abandoned` where `last_step = fulfillment` |
| End-to-end browse → order | `funnel.browse_to_order_rate` | Completed orders | Unique browse sessions | 7 days | Market-level liquidity metric |

**Registered → first order rate:**

```sql
-- 30-day cohort from registration
SELECT COUNT(DISTINCT u.id) FILTER (WHERE first_order.completed_at <= u.created_at + INTERVAL '30 days')
     / COUNT(DISTINCT u.id)::float
FROM users u
LEFT JOIN LATERAL (
  SELECT MIN(completed_at) AS completed_at
  FROM orders WHERE customer_id = u.id AND status = 'completed'
) first_order ON true
WHERE u.role = 'customer'
  AND u.created_at BETWEEN :cohort_start AND :cohort_end
```

→ Events: [Event Taxonomy — Customer](event-taxonomy.md#customer-marketplace-events)

### Creator activation funnel

**Purpose:** Measure supply activation from application to first revenue.  
**Page specs:** [Creator Onboarding Flow](../pages/flows/creator-onboarding-flow.md), [Compliance](../pages/creator/compliance.md), [Catalog](../pages/creator/catalog.md)

| Step | Metric ID | Numerator | Denominator | Window | At-risk threshold |
|------|-----------|-----------|-------------|--------|-------------------|
| Application submitted | `funnel.creator_applications_submitted` | Applications with all required fields | — | — | — |
| Verification completion | `funnel.verification_completion_rate` | Creators fully verified | Applications submitted | 30 days | <70% CS target |
| First listing published | `funnel.first_listing_published_rate` | Verified creators with ≥1 live listing | Verified creators | 14 days | **At-risk:** no listing at day 14 |
| First order received | `funnel.first_order_received_rate` | Verified creators with ≥1 completed order | Verified creators | 30 days | **At-risk:** no order at day 30 |
| Payout readiness | `funnel.payout_setup_completion_rate` | Creators with Connect account active | Creators with ≥1 completed order | 30 days from first order | — |

**Verification drop-off by step:**

Track session-level progression through onboarding steps. Denominator = users entering step; numerator = users who abandon without completing next step within 7 days.

| Step | Entry event | Abandon signal |
|------|-------------|----------------|
| Identity | `onboarding.identity.page_view` | No `onboarding.identity.submit` within 7d |
| Kitchen | `onboarding.kitchen.page_view` | No `onboarding.kitchen.submit` within 7d |
| Compliance | `compliance.center.page_view` | No `compliance.item.submit` within 7d |
| First catalog item | `creator_catalog_viewed` | No `creator_menu_item_saved` (publish) within 14d of verification |

→ CS actions: [Customer Lifecycle — Creator stage gates](../docs/customer-success/customer-lifecycle.md#creator-stage-gates)

### Trust verification funnel (ops)

**Purpose:** Measure ops throughput on human approval workflows.  
**Page specs:** [Verification Queue](../pages/admin/verification-queue.md), [Trust Verification Flow](../pages/flows/trust-verification-flow.md)

| Metric ID | Formula | Target direction |
|-----------|---------|------------------|
| `funnel.verification_sla_adherence` | Applications reviewed within SLA / total applications | ↑ |
| `funnel.verification_median_time` | Median hours: submit → decision | ↓ |
| `funnel.verification_appeal_overturn_rate` | Appeals granted / total appeals | Monitor |

---

## Creator Metrics

Canonical definitions from [Success Metrics — Creator](../product/success-metrics-overview.md#creator-metrics). Formulas below add implementation detail.

### Acquisition & onboarding

| Metric ID | Definition | Data source |
|-----------|------------|-------------|
| `metric.creator_applications_started` | Unique users beginning onboarding (`auth.creator_signup.page_view` or application record created) | Identity + events |
| `metric.creator_applications_submitted` | Applications with all required fields submitted | Trust module |
| `metric.verification_completion_rate` | `verified_creators / submitted_applications` within 30 days | Trust + cohort |
| `metric.time_to_verified` | Median hours: application submit → full verification | Trust timestamps |
| `metric.verification_dropoff_by_step` | % abandoning at each onboarding step | Funnel events |

### Activation

| Metric ID | Definition | Target |
|-----------|------------|--------|
| `metric.first_listing_published_rate` | Creators with ≥1 live listing / verified creators within 14 days | ≥80% (CS internal) |
| `metric.first_order_received_rate` | Creators with ≥1 completed order / verified within 30 days | ≥50% (CS internal) |
| `metric.time_to_first_order` | Median days: verification → first completed order | ≤21 days (CS internal) |
| `metric.profile_completeness_score` | Weighted: photo (20%), story (20%), catalog depth (30%), fulfillment config (30%) | ≥80% at activation |

### Productivity

| Metric ID | Formula |
|-----------|---------|
| `metric.gmv_per_active_creator` | Verified GMV / creators with ≥1 completed order in period |
| `metric.orders_per_active_creator` | Completed orders / active creators in period |
| `metric.aov` | Verified GMV / completed order count |
| `metric.catalog_breadth` | Median active SKUs per active creator |
| `metric.capacity_utilization` | `orders_placed / capacity_available` where capacity tracked |

### Retention

| Metric ID | Formula |
|-----------|---------|
| `metric.creator_retention_monthly` | Creators with order in month M who also have order in M+1 / creators with order in M |
| `metric.creator_churn` | 1 − creator retention |
| `metric.creator_reactivation_rate` | Previously churned creators returning to ≥1 order / churned cohort |
| `metric.wac` | Creators with ≥1 login or order action in 7 days |

### Creator quality

#### Order completion rate

**ID:** `metric.order_completion_rate`  
**Platform target:** ≥98%

```sql
SELECT COUNT(*) FILTER (WHERE status = 'completed')
     / COUNT(*) FILTER (WHERE status IN ('confirmed', 'completed', 'cancelled'))::float
FROM orders
WHERE confirmed_at BETWEEN :start AND :end
```

**Excludes:** Orders cancelled before creator confirmation.

| Metric ID | Formula | Target |
|-----------|---------|--------|
| `metric.on_time_ready_rate` | Orders marked ready by promised time / orders with time promise | ≥95% |
| `metric.creator_cancellation_rate` | Creator-initiated cancellations / confirmed orders | ↓ |
| `metric.creator_avg_review_score` | Mean review rating for creator's completed orders | ≥4.5 (CS) |
| `metric.dispute_rate_creator_attributed` | Disputes lost or mediated against creator / completed orders | ↓ |

→ Events: `creator_order_status_changed`, `admin.dispute.resolve`

---

## Customer Metrics

### Discovery & conversion

| Metric ID | Definition | Events / source |
|-----------|------------|-----------------|
| `metric.search_success_rate` | Searches yielding ≥1 click / total searches | `search_executed`, `search_result_clicked` |
| `metric.zero_result_search_rate` | Searches with no results / total searches | `search_zero_results` |
| `metric.profile_to_cart_rate` | Sessions adding to cart / creator profile views | Storefront + cart events |
| `metric.cart_to_checkout_rate` | Checkouts started / carts created | `cart_checkout_started` |
| `metric.checkout_to_order_rate` | Orders placed / checkouts started | `checkout_order_placed` |
| `metric.fulfillment_step_abandonment` | Drop-off at scheduling/pickup selection | `checkout_abandoned` |

### Retention

#### Repeat purchase rate (30-day)

**ID:** `metric.repeat_customer_rate_30d`

```sql
WITH first_orders AS (
  SELECT customer_id, MIN(completed_at) AS first_order_at
  FROM orders WHERE status = 'completed'
  GROUP BY customer_id
)
SELECT COUNT(*) FILTER (
         WHERE EXISTS (
           SELECT 1 FROM orders o2
           WHERE o2.customer_id = fo.customer_id
             AND o2.status = 'completed'
             AND o2.completed_at > fo.first_order_at
             AND o2.completed_at <= fo.first_order_at + INTERVAL '30 days'
         )
       ) / COUNT(*)::float
FROM first_orders fo
WHERE fo.first_order_at BETWEEN :cohort_start AND :cohort_end
```

| Metric ID | Window |
|-----------|--------|
| `metric.repeat_customer_rate_90d` | Same formula, 90-day window |
| `metric.purchase_frequency` | Orders / active customer / month |
| `metric.cross_creator_purchase_rate` | Customers buying from ≥2 creators in period |
| `metric.customer_retention_monthly` | Order in M and M+1 / order in M |

### Satisfaction

| Metric ID | Definition | Source |
|-----------|------------|--------|
| `metric.csat` | Post-order survey mean (1–5) | Survey pipeline |
| `metric.nps` | Standard NPS | Survey pipeline |
| `metric.support_contact_rate` | Support tickets / completed orders | Support system |
| `metric.refund_request_rate` | Customer-initiated refund requests / completed orders | Order + Payment |

---

## Trust Metrics

Trust metrics are **non-negotiable guardrails**. They appear on executive dashboards **equal to GMV**.

### Verification integrity

| Metric ID | Definition | Target |
|-----------|------------|--------|
| `metric.verified_creator_ratio` | Active creators with full verification / all creators attempting to sell | ↑ |
| `metric.compliance_doc_currency_rate` | Creators with all docs valid / verified creators | ~100% |
| `metric.verification_sla_adherence` | Applications reviewed within SLA / total applications | ↑ |
| `metric.verification_appeal_overturn_rate` | Appeals granted / total appeals | Monitor |

### Review integrity

| Metric ID | Definition |
|-----------|------------|
| `metric.review_submission_rate` | Reviews submitted / review prompts sent |
| `metric.verified_purchase_review_ratio` | Reviews linked to completed orders / total reviews |
| `metric.review_fraud_detection_rate` | Reviews flagged or removed / total reviews |
| `metric.platform_avg_review_score` | Mean rating across marketplace — monitor for sudden shifts |

### Safety & incidents

#### Trust incident rate

**ID:** `metric.trust_incident_rate`  
**Owner:** Trust & Safety · Analytics

```sql
SELECT (COUNT(*) * 1000.0) / NULLIF(order_count, 0)
FROM trust_incidents ti
CROSS JOIN (
  SELECT COUNT(*) AS order_count FROM orders
  WHERE status = 'completed' AND completed_at BETWEEN :start AND :end
) o
WHERE ti.status = 'confirmed'
  AND ti.confirmed_at BETWEEN :start AND :end
```

**Incident types (confirmed only):** allergen mislabel, unlicensed operation, food safety complaint. See [Food Safety Incident SOP](../operations/food-safety-incident-sop.md).

| Metric ID | Definition |
|-----------|------------|
| `metric.time_to_trust_incident_resolution` | Median hours: report → resolution |
| `metric.account_suspension_rate` | Creators suspended / active verified creators |
| `metric.dispute_rate` | Disputes opened / completed orders |
| `metric.dispute_resolution_sla` | Disputes resolved within SLA / total disputes |

### Transparency compliance

| Metric ID | Definition |
|-----------|------------|
| `metric.listing_completeness_rate` | Listings meeting ingredient/allergen/fulfillment standards / live listings |
| `metric.pre_checkout_policy_ack_rate` | Orders with required policy ack / orders requiring ack |

→ Events: `checkout_policy_acknowledged`, `checkout_allergen_acknowledged`

---

## Platform Health Metrics

### Marketplace liquidity

| Metric ID | Definition |
|-----------|------------|
| `metric.supply_demand_ratio` | Active verified creators / active customers in geography |
| `metric.browse_to_order_rate` | Marketplace orders / unique browse sessions |
| `metric.geographic_coverage` | % of target launch area with verified creator within X miles |

### Unit economics

| Metric ID | Definition | Notes |
|-----------|------------|-------|
| `metric.take_rate` | Platform revenue / Verified GMV | `TODO(decision):` commission structure |
| `metric.contribution_margin_per_order` | `(platform_revenue − variable_costs) / order` | |
| `metric.creator_cac` | Sales/marketing spend / new verified creators | |
| `metric.customer_cac` | Spend / new first-time ordering customers | |
| `metric.creator_ltv` | Projected lifetime platform revenue from creator | |
| `metric.customer_ltv` | Projected lifetime platform revenue from customer | |
| `metric.ltv_cac_ratio` | LTV / CAC by segment | Target >3:1 at maturity |

### Payments & payouts

| Metric ID | Target |
|-----------|--------|
| `metric.payment_success_rate` | ≥99% |
| `metric.payout_success_rate` | ↑ |
| `metric.payout_latency` | Median time: order completion → funds available |
| `metric.refund_processing_time` | Median time: refund initiated → customer credited |

### Reliability

| Metric ID | Target | Source |
|-----------|--------|--------|
| `metric.platform_uptime` | 99.9%+ | Infrastructure observability |
| `metric.checkout_error_rate` | ↓ | `checkout_failed` / checkout attempts |
| `metric.notification_delivery_rate` | ↑ | Notification service |
| `metric.search_latency_p95` | ↓ | Discovery service |

→ Infrastructure metrics stay in observability stack; business-facing derivatives defined here. See [Infrastructure Overview](../engineering/infrastructure-overview.md#observability-stack).

### Internal operations efficiency

| Metric ID | Definition |
|-----------|------------|
| `metric.verification_queue_depth` | Pending applications awaiting review |
| `metric.moderation_queue_depth` | Pending review/dispute items |
| `metric.ai_assist_acceptance_rate` | AI recommendations accepted / AI recommendations |
| `metric.cost_per_verification` | Total verification ops cost / verifications completed |

→ Ops SLAs: [Operations](../operations/)

---

## Creator-Facing Metrics (In-App)

Metrics displayed on [Creator Analytics](../pages/creator/analytics.md) — subset of platform definitions, scoped to individual creator:

| Display name | Underlying metric ID | Scope |
|--------------|---------------------|-------|
| Revenue | Creator-scoped GMV | Completed orders only; excludes disputes/refunds |
| Orders | Order count | Completed |
| Average order value | `metric.aov` | Creator-scoped |
| Repeat customer rate | Repeat buyers / unique buyers | Creator-scoped |
| Pickup on time | `metric.on_time_ready_rate` | Creator-scoped |
| Top menu items | Revenue/units by SKU | Creator-scoped |

Cached 15 minutes. Revenue fields omitted for staff roles without permission.

---

## Anti-Metrics

Do not build dashboards or OKRs around these — see [Product Anti-Metrics](../product/success-metrics-overview.md#anti-metrics-do-not-optimize):

| Anti-metric | Track as diagnostic only? |
|-------------|---------------------------|
| Total unverified signups | Yes — ops diagnostic, not success |
| Raw page views | No |
| Review volume (without integrity) | No |
| GMV including unverified creators | Yes — flagged red if growing |
| Short-term take rate maximization | No |

---

## Metric Review Rituals

| Ritual | Metrics reviewed | Owner |
|--------|------------------|-------|
| Weekly business review | Verified GMV + 4 north star inputs | Leadership |
| Monthly trust review | All trust metrics — QoQ degradation requires acceptance | Trust & Safety |
| Quarterly persona segmentation | Creator metrics re-cut by persona and geography | Product · Analytics |
| Incident post-mortem | Relevant metrics + definition updates if needed | Trust & Safety |

→ Dashboard assignments: [Dashboards](dashboards.md)

---

## Open Decisions

| Decision | Metric impact |
|----------|---------------|
| `TODO(decision):` Geographic launch market | Liquidity targets, segmentation baselines |
| `TODO(decision):` Commission structure | Take rate, contribution margin |
| `TODO(decision):` Pricing model | LTV model inputs |

---

## Related Documents

- [Success Metrics Overview](../product/success-metrics-overview.md)
- [Customer Success Metrics](../docs/customer-success/success-metrics.md)
- [Event Taxonomy](event-taxonomy.md)
- [Dashboards](dashboards.md)
- [Data Governance](data-governance.md)
- [Core Entities](../engineering/data/core-entities.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
