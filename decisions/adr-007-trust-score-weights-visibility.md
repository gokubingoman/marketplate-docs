# ADR-007: Trust Score Weights and Visibility

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Product · Trust & Safety · Data

---

## Decision

**Pending founder approval.**

Define (1) **component weights** for Trust Score v1 and (2) which signals are **public** (customer-facing) vs **internal-only** (ops/discovery).

---

## Background

Trust Score is Marketplate's composite creator reliability signal — the "Superhost equivalent" for food ([Company Phases](../roadmap/company-phases.md#trust-score)). It influences:

- Discovery ranking after hard gates ([Discovery Ranking](../ai/discovery-ranking.md))
- [Chef Levels](../roadmap/company-phases.md#chef-levels) progression
- [Marketplate Verified](../roadmap/company-phases.md#marketplate-verified) eligibility
- [Marketplate Collections](../roadmap/company-phases.md#marketplate-collections) placement thresholds

[Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md) and [Glossary — Trust Score](../company/glossary.md#trust-score) reference this ADR for resolution.

---

## Proposed weights (v1)

Hard gates (must pass — not weighted):

- Identity verification ✓
- Kitchen verification ✓
- Compliance current ✓
- Not suspended ✓

Weighted components (sum to 100 points internal):

| Component | Weight | Public visibility |
|-----------|--------|-------------------|
| Verified purchase review average | 25% | **Public** — star rating visible |
| Repeat customer rate | 20% | **Internal** — influences rank only |
| Order completion rate | 20% | **Internal** |
| Refund/dispute rate (inverse) | 15% | **Internal** — never show "refund score" to customers |
| Response time to orders/messages | 10% | **Partial** — "Responds quickly" badge if top quartile |
| Food safety incidents (inverse) | 10% | **Internal** — hard penalty; never public numeric |
| AI verification confidence | 0% public | **Internal assist only** — never customer-facing |

**Public summary:** customers see verification badges, star rating, review count, optional qualitative badges ("Responds quickly," "Top Chef") — **not a single public numeric Trust Score** at Phase 1.

---

## Options for public display

| Option | Customer sees | Pros | Cons |
|--------|---------------|------|------|
| **A — Badges only (recommended)** | Verification + reviews + qualitative badges | Avoids gamification anxiety; trust-first | Less "transparent algorithm" |
| **B — Public numeric score** | 0–100 Trust Score on storefront | Maximum transparency | Gaming; comparison toxicity |
| **C — Tier labels only** | Chef Level name (Verified, Trusted, Top) | Simple; ties to progression | Requires Chef Levels launch |

**Recommend Option A for Phase 1**, migrate toward Option C as Chef Levels ship.

---

## Reasoning

1. **Trust over gamification** — public numeric scores invite manipulation and creator anxiety.
2. Hard gates already communicate safety; reviews provide social proof.
3. Internal composite drives ranking — ops can tune weights without customer confusion.
4. Food safety incidents must never appear as a public score — liability and stigma.

Weight changes require Trust Lead approval + 30-day notice to creators if ranking impact >10% for cohort.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Reduced gaming surface | Less algorithmic transparency marketing |
| Clear customer trust signals | Creators don't see full formula initially |
| Ops can tune internally | Engineering must separate public/internal fields |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| Discovery Service | Weight config in ranking module |
| Creator dashboard | Internal score breakdown for creators |
| Storefront | Badge set only (no public number) |
| Analytics | Trust Score distribution metrics |
| Chef Levels | Threshold mapping |

---

## Interim implementation

- Discovery: hard gates only; soft ranking by review average until weights configured
- Creator dashboard: show component checklist, not composite score
- Config file `trust_score_weights_v1.yaml` with ASSUMPTION banner

---

## Related Documents

- [Trust & Safety Standards — Trust Score](../docs/standards/trust-and-safety-standards.md#trust-score)
- [Discovery Ranking](../ai/discovery-ranking.md)
- [Marketplace Mechanics — Trust Model](../product/marketplace-mechanics.md#trust-model)
- [Glossary — Trust Score](../company/glossary.md#trust-score)
