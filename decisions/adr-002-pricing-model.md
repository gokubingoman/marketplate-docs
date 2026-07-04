# ADR-002: Creator Pricing Model

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Product · Finance · Growth

---

## Decision

**Pending founder approval.**

Select how Marketplate monetizes creators at Phase 1 launch: **transaction-only**, **subscription-only**, **hybrid (subscription + lower take rate)**, or **freemium with paid tiers**.

---

## Background

Pricing shapes creator acquisition messaging, feature gating, unit economics, and competitive positioning against Shopify/Etsy (subscription) and aggregators (take rate). [Value Propositions](../product/value-props.md) and [Market Analysis](../research/market-analysis.md) note creator price sensitivity — especially cottage food operators with thin margins.

Pricing must align with [ADR-003 Commission Structure](adr-003-commission-structure.md) if hybrid.

---

## Options

| Option | Model | Indicative structure | Best for |
|--------|-------|---------------------|----------|
| **A — Transaction-only** | No monthly fee; revenue from commission per order | 8–15% + payment processing | Low barrier; marketplace liquidity focus |
| **B — Subscription-only** | Flat monthly fee; low or zero commission | $29–79/mo tiers by features | Predictable revenue; creator OS positioning |
| **C — Hybrid** | Modest subscription + reduced commission | $19/mo + 5–8% | Balance of retention and GMV alignment |
| **D — Freemium tiers** | Free verified tier + paid Pro/Business | Free + $49 Pro + $149 Business | Feature-gated growth; Chef Levels tie-in |

---

## Reasoning (recommended direction)

**Recommend Option A (transaction-only) for Phase 1 soft launch**, with **Option D roadmap** for Phase 4 Chef OS:

1. Minimizes creator signup friction when supply is the bottleneck.
2. Aligns Marketplate revenue with **Verified GMV** — the north star metric.
3. Subscription tiers add complexity before liquidity is proven.
4. [Chef Levels](../roadmap/company-phases.md#chef-levels) can later gate analytics depth and Collections placement without pay-to-win ranking.

Introduce paid tiers only after: ≥50 active verified creators with orders and documented willingness-to-pay from founding cohort interviews.

---

## Alternatives considered

- **High subscription, zero commission** — rejected for Phase 1; mimics SaaS without proven chef OS depth.
- **Listing fees per item** — rejected; conflicts with quality-over-volume thesis.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Faster creator signup | Less predictable MRR early |
| GMV-aligned incentives | Higher dependence on commission ADR |
| Simple GTM story | Less revenue diversification until Phase 4 |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| Creator signup / billing UX | Pricing page, plan selection |
| Admin Platform Settings | Fee configuration |
| `legal/creator-agreement.md` | Fee disclosure clauses |
| Growth messaging | Competitive comparison tables |
| Feature flags | Tier-gated features if freemium |

---

## Interim implementation

- Payment Service: single `platform_fee_bps` config (ties to ADR-003)
- No subscription billing until ADR accepted
- Creator dashboard: hide "Plans" nav

---

## Related Documents

- [ADR-003 Commission Structure](adr-003-commission-structure.md)
- [Value Propositions](../product/value-props.md)
- [Marketplace Mechanics — Payment model](../product/marketplace-mechanics.md#payment-model)
- [Success Metrics Overview](../product/success-metrics-overview.md)
