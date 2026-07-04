# Discovery Ranking

> Trust-weighted ranking for search, browse, and home surfaces. Optimizes for **fit and confidence**, not engagement bait — [Marketplace Mechanics](../product/marketplace-mechanics.md#discovery).

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** AI Platform  
**Service owner:** [Discovery Service](../engineering/services/discovery-service.md)

---

## Purpose

Discovery Ranking orders creators and listings on customer-facing surfaces — [Search](../pages/customer/search.md), [Browse](../pages/customer/browse.md), [Home](../pages/customer/home.md), and location-aware collections. It weights **verification status, review quality, and fulfillment reliability** above engagement manipulation.

Ranking is **explainable** to operators and auditable for trust compliance. Weights are **human-configurable** in [Platform Settings](../pages/admin/platform-settings.md) without code deploys.

The system does not hide verification status, boost expired compliance, or accept pay-for-rank that obscures trust signals per [Ranking principles](../product/marketplace-mechanics.md#ranking-principles) and [Anti-patterns](../product/marketplace-mechanics.md#anti-patterns-explicitly-rejected).

---

## Problem Statement

Marketplace discovery must connect customers with verified creators they can trust — not maximize clicks through engagement bait.

| Failure mode | Why rejected |
|--------------|--------------|
| Unverified creators ranked equally | Violates trust thesis |
| High click-through but unreliable fulfillment ranked first | Breaks customer confidence |
| Opaque algorithms | Cannot audit trust compliance |
| Engagement-only optimization | Rewards sensational listings over quality |
| Static manual curation only | Does not scale across geographies |

Discovery Ranking provides a documented, configurable scoring model with explicit trust gates and human-tunable weights.

---

## Inputs

### Entity types ranked

| Entity | Surfaces |
|--------|----------|
| **Creator** | Home featured, browse collections, search result cards |
| **Listing / menu item** | Search, creator storefront catalog order, collection items |
| **Collections** | Editorial + algorithmic groupings on browse/home |

### Trust signals (required)

| Signal | Source | Notes |
|--------|--------|-------|
| **Verification status** | Trust Service | Identity, kitchen, compliance — granular states |
| **Compliance freshness** | Trust Service | Expired docs → hard demote or exclude |
| **Review quality** | Order Service + moderation | Verified purchase only; moderated reviews excluded |
| **Fulfillment reliability** | Order Service | On-time rate, cancel rate, dispute rate |
| **Listing completeness** | Catalog Service | Photos, allergens, fulfillment config |

### Relevance signals

| Signal | Source |
|--------|--------|
| **Query match** | Search index — keyword + semantic |
| **Dietary / cuisine filters** | Catalog metadata |
| **Proximity** | Geo + service area |
| **Availability** | Real-time inventory and schedule |
| **Fulfillment fit** | Pickup window, delivery zone match |

### Personalization signals (opt-in where required)

| Signal | Constraint |
|--------|------------|
| **Order history** | Boost previously ordered creators — not hidden paywall |
| **Favorites** | Surface in "For you" modules |
| **Follow notifications** | Separate from organic rank |

### Explicitly excluded inputs

Per [Ranking principles](../product/marketplace-mechanics.md#ranking-principles):

| Excluded | Reason |
|----------|--------|
| **Raw click-through rate as primary signal** | Engagement bait |
| **Time-on-site manipulation** | Not trust-aligned |
| **Paid boost without verification badge visible** | Anti-pattern |
| **Review count without verified purchase weighting** | Fake social proof |
| **Creators with expired compliance** | Hard gate — not weight-adjustable |

---

## Outputs

### Ranking output

For each request, Discovery Service returns ordered entities with:

| Output | Description |
|--------|-------------|
| **Ranked list** | `{ entity_id, type, score, rank }` |
| **Explainability payload** | Top contributing factors per entity (internal + optional debug mode) |
| **Trust gate status** | `eligible` · `demoted` · `excluded` with reason code |
| **Model version** | `discovery-rank-v1.x` + weight profile ID |

### Customer-visible explainability (limited)

- Creator cards show trust badges, rating summary, fulfillment type — not raw scores
- "Why this result" debug panel: **staff-only** in v1; future customer-facing trust highlights ("Highly rated · Verified kitchen · Reliable fulfillment")

### Operator-visible explainability

[Platform Settings](../pages/admin/platform-settings.md) preview tool shows sample query results with factor breakdown before weight changes.

Example internal factor breakdown:

```json
{
  "creator_id": "cr_123",
  "final_score": 0.847,
  "factors": [
    { "name": "verification_complete", "weight": 0.30, "value": 1.0, "contribution": 0.30 },
    { "name": "review_quality", "weight": 0.25, "value": 0.92, "contribution": 0.23 },
    { "name": "fulfillment_reliability", "weight": 0.20, "value": 0.88, "contribution": 0.18 },
    { "name": "relevance", "weight": 0.15, "value": 0.95, "contribution": 0.14 },
    { "name": "proximity", "weight": 0.10, "value": 0.71, "contribution": 0.07 }
  ],
  "trust_gate": "eligible"
}
```

---

## Models

### Architecture

Discovery Ranking is primarily a **transparent scoring function** — not an opaque end-to-end neural ranker in v1.

| Layer | Approach |
|-------|----------|
| **Trust gates** | Deterministic rules — hard filters before scoring |
| **Relevance** | BM25 + embedding similarity (search); collection rules (browse) |
| **Quality scoring** | Weighted linear combination of normalized signals |
| **Personalization** | Lightweight re-ranker on top 50 candidates — bounded influence cap |
| **Semantic search** | Embedding model for query ↔ listing/creator match |

### Hosting

- Scoring runs in [Discovery Service](../engineering/services/discovery-service.md) — low-latency, no external LLM in request path for v1
- Embedding index co-located with search index
- Weight profiles stored in Platform Settings; cached at edge with version stamp

### Why linear + gates (v1)

- Auditable for trust compliance and legal review
- Human-configurable weights map directly to factors
- Avoids black-box engagement optimization

Future: learned re-ranker **only** as final stage with monotonic trust constraints — requires ADR before adoption.

---

## Prompt Strategy

Discovery Ranking uses **minimal LLM usage** in v1.

| Use | Strategy |
|-----|----------|
| **Semantic query expansion** | Optional offline — not hot path |
| **Collection description matching** | Embedding only |
| **Review quality NLP** | Separate batch job for sentiment/toxicity flags — not ranking prompt |

If generative query understanding is added:

- System role: extract dietary intent and cuisine terms — **never** rank instructions from user query
- Prompt injection defense: user search queries cannot override weight profile

Full prompts (if any) in [`prompts/`](../prompts/).

---

## Evaluation

### Offline eval

| Eval set | Focus |
|----------|-------|
| **Labeled relevance judgments** | 500+ query ↔ creator/listing pairs |
| **Trust compliance cases** | Unverified must never appear above verified |
| **Expired compliance** | Must exclude or demote per policy |
| **Fulfillment reliability** | High dispute creators rank below peers |
| **Geographic relevance** | Proximity tie-breaking |

### Metrics

| Metric | Target |
|--------|--------|
| **Trust gate violation rate** | 0% — blocking metric |
| **NDCG@10** (relevance eval set) | ≥ 0.75 |
| **Verified-first invariant** | 100% on test queries |
| **Fulfillment reliability correlation** | Top-10 results have ≥ platform median reliability |
| **Personalization cap** | Re-ranker moves ≤ 3 positions for personalization-only signal |

### Online metrics

- Search zero-result rate
- Click → order conversion (diagnostic, not optimization target alone)
- Creator concentration (Gini) — flag unhealthy markets
- Customer trust survey correlation with ranking changes

### Counter-metrics (guardrails)

- Do **not** optimize session length or raw CTR in isolation
- Alert if engagement metrics improve but dispute rate rises

---

## Confidence Thresholds

Discovery Ranking is not a classifier with approve/reject — thresholds apply to **eligibility gates** and **semantic match**.

| Gate / signal | Threshold | Effect |
|---------------|-----------|--------|
| **Unverified creator** | Any paid listing attempt | Excluded from customer discovery |
| **Expired compliance** | Past grace period | Excluded; in grace → demoted max rank |
| **Moderation hold** | Listing flagged | Excluded until cleared |
| **Minimum review count for quality signal** | < 3 verified reviews | Review quality factor uses neutral prior — not penalized harshly |
| **Fulfillment reliability** | Below platform 10th percentile | Demoted; not excluded unless chronic |
| **Semantic relevance** | < 0.35 similarity | Excluded from semantic search results |
| **Photography quality score** | Below collection minimum | Ineligible for featured collections only |

Weight profile changes require preview + confirmation in Platform Settings; rollback within one click.

---

## Fallback Behaviour

| Failure | Fallback |
|---------|----------|
| **Discovery Service down** | Cached popular creators in geography; verified-only filter |
| **Embedding index stale** | Keyword search only |
| **Weight profile load fail** | Last known good profile; alert ops |
| **Personalization unavailable** | Global ranking only |
| **Real-time availability fail** | Show with stale availability badge — deprioritize in sort |

Never fall back to including unverified creators in paid discovery surfaces.

---

## Security

### Manipulation resistance

- Creators cannot set ranking weights — read-only factor display in creator dashboard (future)
- No customer search input affects other users' rankings
- Featured collection slots require operator assignment + trust threshold

### Data

- Ranking logs: query hash, result IDs, weight profile version — not full PII
- Personalization uses customer ID scoped data — no cross-customer leakage

### Audit

- Weight profile changes logged in Platform Settings audit trail
- Monthly export of trust gate violations (should be zero)

---

## Human Approval

| Decision | Authority |
|----------|-----------|
| **Weight profile changes** | Ops lead or engineering — [Platform Settings](../pages/admin/platform-settings.md) |
| **Featured collections** | Editorial human curation + trust minimums |
| **Exclude creator from discovery** | Trust & Safety enforcement — not ranking AI |
| **Algorithm version promotion** | AI Platform + Product sign-off |

No fully autonomous weight self-tuning in v1. ML-suggested weight changes require human review and offline eval pass.

---

## Monitoring

### Operational

| Metric | Alert |
|--------|-------|
| Ranking latency p95 | > 150ms |
| Index freshness lag | > 5 min |
| Weight profile cache miss | > 1% |

### Trust

| Metric | Cadence |
|--------|---------|
| Trust gate violations | Real-time alert |
| Unverified in results sample | Daily audit |
| Expired compliance in results | Daily audit |
| Factor distribution drift | Weekly |

### Business (diagnostic)

| Metric | Use |
|--------|-----|
| Conversion by rank position | Sanity check — not sole KPI |
| Zero-result searches | Supply gap detection |
| Creator visibility Gini | Market health |

### Cost

- Embedding index size and query cost
- Cache hit rate for popular queries

---

## Continuous Improvement

### Weight tuning process

```
Ops hypothesis → Platform Settings preview → Offline eval → Shadow 5% traffic
    → Compare trust guardrails + conversion → Human approve → Rollout
```

### Signal additions

New signals require:
1. Documentation in this file
2. Explainability mapping
3. Offline eval impact on trust invariants
4. ADR if changes ranking philosophy

### Personalization

- Opt-in where regulations require
- Cap personalization influence — trust factors dominate
- Regular bias audits by geography and creator size

### Roadmap

- Customer-visible "trust highlights" on cards
- Learned re-ranker with monotonic trust constraints (ADR required)
- A/B testing framework with trust guardrails as hard stops

---

## Related Documents

- [Marketplace Mechanics — Discovery & Ranking](../product/marketplace-mechanics.md#discovery)
- [Founding Constitution — Trust Philosophy](../company/constitution.md#trust-philosophy)
- [Values — Trust Is the Product](../company/values.md#1-trust-is-the-product)
- [Platform Settings](../pages/admin/platform-settings.md)
- [Discovery Service](../engineering/services/discovery-service.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Verification Assist](verification-assist.md)
- [Moderation Assist](moderation-assist.md)
- [AI Platform README](README.md)
