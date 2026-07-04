# ADR-003: Marketplace Commission Structure

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Finance · Product · Legal

---

## Decision

**Pending founder approval.**

Define the **platform take rate** (commission on GMV), whether payment processing fees pass through to creators or customers, and payout timing rules.

---

## Background

Commission structure affects:

- Checkout UX (fee transparency per [Marketplace Mechanics](../product/marketplace-mechanics.md#transparency))
- Creator unit economics and acquisition messaging
- Stripe Connect `application_fee_amount` implementation ([Payment Service](../engineering/services/payment-service.md))
- Legal fee disclosure ([Creator Agreement](../legal/creator-agreement.md), [Terms of Service](../legal/terms-of-service.md))

Competitive context: aggregators take 15–30%+; Shopify charges subscription + payment; cottage food creators are margin-sensitive ([Competitive Landscape](../research/competitive-landscape.md)).

---

## Options

| Component | Option A | Option B | Option C |
|-----------|----------|----------|----------|
| **Platform commission** | 10% of order subtotal | 8% + $0.30/order | Tiered: 12% New Chef → 8% Trusted Chef |
| **Payment processing** | Pass-through (creator pays Stripe) | Bundled in commission | Customer pays service fee at checkout |
| **Payout schedule** | Weekly (T+7) | Daily after hold period | Instant for Trusted Chef tier only |
| **Dispute hold** | Rolling 7-day reserve | Per-order hold until fulfillment + 48h | Flat % reserve |

---

## Reasoning (recommended direction)

**Recommend for Phase 1:**

| Component | Recommendation | Rationale |
|-----------|----------------|-----------|
| Commission | **10% flat** | Simple; competitive vs aggregators; easy legal disclosure |
| Payment processing | **Pass-through** | Transparent; creator sees true Stripe cost |
| Payout schedule | **Weekly T+7** | Standard Connect pattern; reduces fraud exposure |
| Dispute hold | **7-day rolling reserve on new creators; waived at Trusted Chef** | Balances creator cash flow vs chargeback risk |

Tiered commission (Option C) deferred until Trust Score and Chef Levels operational — avoids gaming.

---

## Alternatives considered

- **Customer service fee** (DoorDash model) — rejected; conflicts with trust-first transparent pricing thesis.
- **Zero commission launch promo** — acceptable for ≤30-day founding cohort only; must be ADR amendment with end date.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Simple implementation and legal copy | Less optimization for high-volume creators |
| Transparent creator economics | Lower short-term revenue vs bundled fees |
| Weekly payout reduces fraud | Creators wait vs daily payout competitors |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| Checkout page | Fee line items |
| Payment Service | `application_fee_amount`, payout cron |
| Creator payouts page | Schedule and fee breakdown |
| Analytics | Net revenue vs GMV reporting |
| Legal docs | Fee tables in Creator Agreement |

---

## Interim implementation

Engineering stub in Payment Service:

```yaml
platform_fee_bps: 1000  # ASSUMPTION — 10% until ADR accepted
payout_schedule: weekly
payment_fee_pass_through: true
```

Display "Fees subject to change before launch" in staging checkout.

---

## Related Documents

- [ADR-002 Pricing Model](adr-002-pricing-model.md)
- [ADR-006 Stripe Connect Model](adr-006-stripe-connect-model.md)
- [Payout Processing SOP](../operations/payout-processing-sop.md)
- [Creator Payouts page spec](../pages/creator/payouts.md)
