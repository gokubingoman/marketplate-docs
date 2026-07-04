# ADR-001: Geographic Launch Market

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Legal · Growth · Trust & Safety

---

## Decision

**Pending founder approval.**

Select the **founding geographic market** — the first city or metro region where Marketplate launches with full verification, compliance, GTM, and support coverage.

---

## Background

Marketplate cannot publish enforceable legal text, cottage food compliance templates, tax configuration, or local GTM until a launch geography is chosen. This decision cascades into:

- Governing law and dispute jurisdiction ([`legal/`](../legal/))
- Cottage food vs. commercial kitchen rules ([Food Commerce Compliance](../legal/food-commerce-compliance.md))
- SAM/SOM quantification ([Market Analysis](../research/market-analysis.md))
- Discovery defaults (geo radius, featured creators)
- Support hours and escalation contacts

Research identifies **cottage food operators, bakers, and meal prep businesses** as launch anchors — but the specific metro must be founder-selected.

---

## Options

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| **A — Single US metro** | One city + surrounding suburbs (e.g., Austin, Toronto, Atlanta) | Focused liquidity; simpler compliance; easier PR | Smaller TAM narrative; single-market risk |
| **B — US state-wide** | Launch across one US state with uniform cottage food rules | Larger supply pool; state-level PR | Compliance variance within state; harder ops staffing |
| **C — Canada first** | Canadian metro (e.g., Toronto, Vancouver) | Strong cottage food narrative; less US aggregator noise | Stripe/payment config; cross-border expansion later |
| **D — Dual city pilot** | Two metros simultaneously | Faster learning | Split liquidity; 2× ops/legal cost — **not recommended for Phase 1** |

---

## Reasoning (recommended direction)

**Recommend Option A — single metro** for Phase 1 soft launch:

1. **Supply-before-demand** requires geographic density — one metro maximizes creator-customer overlap.
2. Trust & Safety can staff verification for one jurisdiction before scaling.
3. Legal counsel can produce one jurisdiction annex before expansion.
4. [Launch Plan](../growth/launch-plan.md) liquidity thresholds assume `[Launch Market]` concentration.

Metro selection criteria (founder workshop):

| Criterion | Weight |
|-----------|--------|
| Cottage food law clarity and volume | High |
| Independent chef / meal prep density | High |
| Affluent trust-seeking buyer population | High |
| Stripe Connect availability | Required |
| Founder network for founding creator cohort | High |
| Competitive aggregator saturation (inverse) | Medium |

---

## Alternatives considered

- **Nationwide US launch** — rejected; destroys liquidity and compliance focus.
- **Wait for multi-market legal template** — rejected; blocks all launch execution.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Achievable marketplace liquidity | National brand narrative deferred |
| Counsel-efficient legal launch | Expansion playbook needed within 6–12 months |
| Ops excellence in one market | SAM slides show single-city numbers initially |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| `legal/*` | Governing law, tax, cottage food annex |
| `growth/*` | Replace `[Launch Market]` placeholders |
| `research/market-analysis.md` | Quantify SAM/SOM |
| `pages/` discovery defaults | Geo radius, featured content |
| `operations/*` | Support hours, regulatory contacts |
| Platform Settings admin page | Launch region config |

---

## Interim implementation

Engineering may stub:

- `platform.launch_region` config key (nullable)
- Geo filter in Discovery Service behind feature flag (disabled until ADR accepted)
- Legal docs retain `TODO(decision):` jurisdiction clauses

**Do not:** publish customer-facing legal text, run paid geo-targeted ads, or configure tax without accepted ADR.

---

## Related Documents

- [Market Analysis](../research/market-analysis.md)
- [Go-to-Market Strategy](../growth/go-to-market-strategy.md)
- [Launch Plan](../growth/launch-plan.md)
- [Food Commerce Compliance](../legal/food-commerce-compliance.md)
- [Launching a New Market](../docs/playbooks/launching-new-market.md)
