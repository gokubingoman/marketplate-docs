# Retention & Expansion

> Retention strategy, health scoring, intervention tiers, and expansion motions for creators and buyers.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Customer Success

---

## Purpose

Retention at Marketplate means **sustained Verified GMV with trust guardrails intact** — not keeping inactive accounts on the platform. This document defines how CS identifies at-risk accounts, intervenes proactively, and expands productive relationships without compromising verification standards or buyer safety.

North star context: [Verified GMV](../../product/success-metrics-overview.md#north-star-metric). If Verified GMV grows while trust metrics degrade, treat as a crisis — not success.

---

## Retention Strategy

### Strategic frame

| Audience | Retention definition | Primary lever |
|----------|---------------------|---------------|
| **Creators** | Monthly order activity with high completion rate | OS depth — catalog, fulfillment, customer relationships on-platform |
| **Buyers** | Repeat purchase from verified creators | Trust compounding — favorites, order history, reliable fulfillment |

Retention levers align with [Value Propositions](../../product/value-props.md):

| Dimension | Creator retention mechanism | Buyer retention mechanism |
|-----------|----------------------------|---------------------------|
| **Trust** | Verified badge drives conversion; compliance prevents suspension | Confidence to reorder; no anonymous-seller risk |
| **Software** | Switching cost from operational data, catalog, order history | Seamless reorder, tracking, dietary filters |
| **Community** | Reviews compound reputation | Relationship with specific creators |
| **Economics** | Fair fees, reliable payouts | Fair value for quality — not discount hunting |

### What we do not do

| Anti-pattern | Why harmful |
|--------------|-------------|
| Waive verification to "save" a creator | Violates trust thesis; see [Anti-Metrics](../../product/success-metrics-overview.md#anti-metrics-do-not-optimize) |
| Discount-driven buyer reactivation | Attracts price shoppers, not trust-seeking buyers |
| Ignore completion rate drops while GMV rises | Leading indicator of churn and trust incidents |
| Generic blast emails | Low signal; erodes brand — see [Brand Voice](../../brand/voice-and-tone.md) |

---

## Creator Retention

### Retention metrics

| Metric | Definition | CS monitoring |
|--------|------------|---------------|
| **Creator retention (monthly)** | % of creators with order in M who also order in M+1 | Primary health indicator |
| **Creator churn** | Zero orders after prior active month | Win-back trigger |
| **Weekly active creators (WAC)** | ≥1 login or order action in 7 days | Engagement pulse |
| **Order completion rate** | Completed / confirmed orders | Quality guardrail (target ≥98%) |
| **Creator-initiated cancellation rate** | Creator cancellations / confirmed | Operational stress signal |
| **Creator reactivation rate** | Churned creators returning | Win-back effectiveness |

→ Full definitions: [Creator Metrics](../../product/success-metrics-overview.md#retention)

### Creator churn root causes

| Root cause | Signals | Intervention |
|------------|---------|--------------|
| **Activation failure** | Verified, no listing or no first order | Activation playbook — [Education Playbooks](education-playbooks.md#seller-education) |
| **Operational overwhelm** | Rising cancellations, late ready rate | Fulfillment coaching; capacity configuration |
| **Low demand** | Listings live, zero profile views | Share-link strategy; discovery optimization |
| **Platform friction** | Support tickets, login drop-off | Product feedback loop; workaround guidance |
| **Economics dissatisfaction** | Payout complaints, off-platform migration hints | Transparent fee communication; GMV growth coaching |
| **Compliance stress** | Expired docs, category blocks | Compliance center walkthrough |
| **Trust incident** | Dispute lost, review drop | Trust team coordination; recovery plan |
| **Seasonality** | Predictable lull (e.g., baker post-holiday) | Pre-season capacity planning outreach |

Segment churn analysis by [persona](../../product/personas.md) after sufficient volume.

---

## Buyer Retention

### Retention metrics

| Metric | Definition | CS monitoring |
|--------|------------|---------------|
| **Repeat purchase rate (30-day)** | ≥2 orders within 30 days of first / first-time customers | Early retention signal |
| **Repeat purchase rate (90-day)** | Same at 90-day window | Mature retention signal |
| **Purchase frequency** | Orders per active customer per month | Engagement depth |
| **Customer retention (monthly)** | % ordering in M who order in M+1 | Cohort health |
| **CSAT** | Post-order satisfaction (1–5) | Experience quality |
| **Support contact rate** | Tickets / completed orders | Friction indicator |
| **Refund request rate** | Customer refunds / completed orders | Trust erosion signal |

→ Full definitions: [Customer Metrics](../../product/success-metrics-overview.md#retention--engagement)

### Buyer churn root causes

| Root cause | Signals | Intervention |
|------------|---------|--------------|
| **First order failure** | Refund, dispute, low CSAT | Support resolution + CS follow-up |
| **Trust broken** | Allergen concern, late/missing order | Trust escalation if needed; creator coaching |
| **Discovery gap** | Single-creator purchase, no return | Cross-creator recommendations |
| **Forgotten relationship** | Dormant 90+ days | Creator-update re-engagement (not discounts) |
| **Fulfillment mismatch** | Abandonment at scheduling step | Buyer education on fulfillment options |

---

## Health Scoring

Health scores combine **leading indicators** (engagement, completeness) with **lagging outcomes** (orders, completion, satisfaction). Scores drive automated alerts and CSM prioritization.

### Creator health score (0–100)

| Component | Weight | Green (healthy) | Yellow (watch) | Red (at-risk) |
|-----------|--------|-----------------|----------------|---------------|
| **Order activity** | 25% | ≥1 order in last 30 days | Login but no order 30–45 days | No order 45+ days after activation |
| **Completion rate** | 20% | ≥98% | 95–97% | <95% |
| **On-time ready rate** | 15% | ≥95% | 90–94% | <90% |
| **Profile & catalog completeness** | 15% | Score ≥80% | 60–79% | <60% |
| **Review score** | 10% | ≥4.5 avg | 4.0–4.4 | <4.0 |
| **Compliance currency** | 10% | All docs valid | Expiring within 30 days | Expired or missing |
| **Support/dispute rate** | 5% | 0 disputes / low tickets | 1 dispute or 2+ tickets | 2+ disputes or trust flag |

**Score thresholds:**

| Score | Status | Action |
|-------|--------|--------|
| 80–100 | Healthy | Automated tips only; expansion eligible |
| 60–79 | Watch | Automated nurture + CS monitor |
| 40–59 | At-risk | CSM outreach within 5 business days |
| 0–39 | Critical | CSM outreach within 2 business days; manager review |

**Hard overrides (immediate at-risk regardless of score):**

- Verification or compliance suspension pending
- Trust incident in last 14 days
- Order completion rate <90% over trailing 30 days
- Creator-initiated cancellation rate >5% over trailing 30 days

### Buyer health score (0–100)

| Component | Weight | Green | Yellow | Red |
|-----------|--------|-------|--------|-----|
| **Purchase recency** | 35% | Order in last 30 days | 31–60 days | 61+ days |
| **Purchase frequency** | 25% | ≥2 orders in 90 days | 1 order in 90 days | 0 orders after first |
| **CSAT (last order)** | 20% | 4–5 | 3 | 1–2 |
| **Dispute/refund history** | 15% | None | 1 resolved | Open dispute or 2+ |
| **Engagement** | 5% | Favorites, reorders | Browse only | No login 90+ days |

Buyer scores primarily drive **automated re-engagement** and **support prioritization** for high-value repeat buyers.

---

## Intervention Strategy

### Intervention tiers

| Tier | Trigger | Response time | Channel | Owner |
|------|---------|---------------|---------|-------|
| **T0 — Automated** | Score 80+; milestone events | Immediate | Email, in-app | System |
| **T1 — Guided** | Score 60–79; activation stall | 3 business days | Email sequence | CS (monitored) |
| **T2 — Personal** | Score 40–59; day-14 no listing | 5 business days | Email + in-app message | CSM |
| **T3 — High-touch** | Score 0–39; high GMV creator | 2 business days | Call/video + email | Senior CSM |
| **T4 — Executive** | Top 5% GMV at critical risk | 1 business day | Executive sponsor call | CS leadership |

### Intervention playbook structure

Every T2+ intervention follows this sequence:

1. **Diagnose** — Review health score components, recent orders, support tickets, persona
2. **Personalize** — Reference specific catalog, completion rate, or compliance item — never generic "checking in"
3. **Offer one clear action** — "Publish your first listing" not a list of ten tasks
4. **Set follow-up** — Calendar reminder at 7 days; escalate if no response
5. **Document** — Internal note with outcome tag: resolved, in-progress, churned, escalated

### Persona-specific intervention priorities

| Persona | If at-risk, prioritize |
|---------|------------------------|
| Independent Chef | Profile story, share link, first-order fulfillment coaching |
| Meal Prep Business | Batch capacity, cut-off configuration, weekly rhythm |
| Baker | Lead times, holiday capacity planning, deposit setup |
| Caterer | Quote response time, event calendar, deposit collection |
| Food Truck | Location schedule accuracy, pre-order promotion |
| Cottage Food | Compliance checklist, category clarity, sales cap awareness |
| Pop-Up Kitchen | Event listing, capacity/waitlist, pre-pay setup |
| Commercial Kitchen | Tenant activation, kitchen doc renewal |

---

## Expansion Strategy

Expansion grows **Verified GMV per relationship** — not account count at any cost.

### Creator expansion motions

| Motion | Eligibility | CS action | Metric moved |
|--------|-------------|-----------|--------------|
| **Catalog depth** | Healthy score; <5 active SKUs | Merchandising tips; seasonal collections | Catalog breadth, AOV |
| **Capacity optimization** | Orders hitting capacity limits | Capacity window coaching | GMV per creator (without overcommit) |
| **Fulfillment expansion** | Pickup-only with delivery demand | Delivery zone setup guidance | Orders per creator |
| **Operational maturity** | High completion, growing volume | Advanced dashboard features; batch views | Retention, completion rate |
| **Cross-promotion** | Strong reviews, local density | Feature in collections (Product/Marketing coordination) | Discovery, new buyer acquisition |
| **Subscription patterns** | Meal prep / repeat buyer base | Bundle and renewal guidance | Repeat customer rate |

**Expansion guardrail:** Never encourage capacity increases that risk completion rate or on-time ready rate drops.

### Buyer expansion motions

| Motion | Eligibility | CS action | Metric moved |
|--------|-------------|-----------|--------------|
| **Reorder enablement** | First order complete, CSAT ≥4 | Favorites setup; reorder notification education | Repeat purchase rate |
| **Cross-creator discovery** | Repeat buyer, single creator | Dietary/cuisine recommendations | Cross-creator purchase rate |
| **Advocacy** | NPS ≥9, 3+ orders | Referral program (when available); review encouragement | Creator-attributed acquisition |

### Expansion anti-patterns

- Upselling features before activation complete
- Pushing buyers to unrelated creators via aggressive marketing
- Encouraging creators to list prohibited categories for GMV
- Premium placement that obscures verification status

---

## Win-Back Programs

### Creator win-back

| Timing | Trigger | Approach |
|--------|---------|----------|
| Day 60 | Zero orders after prior active month | Email: "What's blocking your next order?" + single CTA |
| Day 90 | Still inactive | Personal outreach; offer 15-min ops review |
| Day 120 | No response | Archive from active pipeline; quarterly check-in only |

Win-back messaging leads with **software value** (time saved) and **trust** (reviews compounding) — not fee discounts.

### Buyer win-back

| Timing | Trigger | Approach |
|--------|---------|----------|
| Day 90 | Dormant after prior purchase | Email: updates from favorite creators (if any) |
| Day 120 | Still dormant | New verified creators matching dietary preferences |

Never lead with percentage-off discounts — attracts wrong buyer segment per [Success Metrics Overview — Anti-Metrics](../../product/success-metrics-overview.md#anti-metrics-do-not-optimize).

---

## Escalation to Product & Trust

| Signal | Escalate to | Data to include |
|--------|-------------|-----------------|
| ≥3 creators same persona, same friction | Product | Persona, feature area, ticket excerpts |
| Completion rate drop market-wide | Product + Ops | Geo, timeframe, fulfillment type |
| Health score model misprediction | Analytics | False positive/negative examples |
| Creator dispute with trust implications | Trust & Safety | Order ID, allergen/compliance context |
| Buyer safety concern | Trust & Safety | Immediate — bypass standard CS SLA |

→ [Trust & Safety Escalation Playbook](../playbooks/trust-safety-escalation.md)

---

## Reporting

| Report | Cadence | Audience | Contents |
|--------|---------|----------|----------|
| At-risk pipeline | Weekly | CS team | Count by tier, persona, age, owner |
| Intervention outcomes | Weekly | CS leadership | Resolution rate, reactivation rate |
| Health score distribution | Weekly | CS + Product | % green/yellow/red; trend |
| Expansion pipeline | Monthly | CS + Product | Motions attempted, GMV impact |
| Churn post-mortem | Monthly | CS + Product + Trust | Root cause tags, action items |

→ CS metric definitions: [Success Metrics](success-metrics.md)

---

## Related Documents

- [Customer Success README](README.md)
- [Customer Lifecycle](customer-lifecycle.md)
- [Education Playbooks](education-playbooks.md)
- [Success Metrics](success-metrics.md)
- [Value Propositions](../../product/value-props.md)
- [Success Metrics Overview](../../product/success-metrics-overview.md)
- [Personas](../../product/personas.md)
