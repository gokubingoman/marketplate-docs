# Launching a New Market

> End-to-end operational playbook for geographic expansion — jurisdiction rules, supply acquisition, discovery, and go-live.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Market Expansion  
**Playbook type:** Cross-functional orchestration

---

## Purpose

This playbook orchestrates **geographic market launch** — expanding Marketplate from an existing or pre-launch baseline into a new state, metro, or locality. A new market is not a marketing campaign alone; it requires legal jurisdiction templates, compliance rule configuration, supply acquisition, discovery indexing, trust operator staffing, and liquidity monitoring.

**Open decision:** Initial launch market is `TODO(decision):` per [Marketplace Mechanics](../../product/marketplace-mechanics.md#open-decisions). This playbook applies to every subsequent market.

**Governing thesis:** Liquidity requires verified supply and active demand in a geography — [Marketplace Mechanics — Liquidity](../../product/marketplace-mechanics.md#liquidity).

---

## Trigger

| Trigger | Example |
|---------|---------|
| **Strategic expansion decision** | Founder/Product approves Market X in Q3 roadmap |
| **Creator density threshold** | Waitlist in region exceeds N signups |
| **Partnership opportunity** | Commercial kitchen network in new city |
| **Competitive / regulatory window** | Cottage food law change opens new category |

**Gate 0:** Founder or executive sponsor approves market entry — documented in decision log or ADR.

---

## Stakeholders

| Role | Team | Responsibility |
|------|------|----------------|
| **Market Launch Lead** | Market Expansion / Product | End-to-end orchestration, go/no-go |
| **Legal Counsel** | Legal | Jurisdiction rules, terms updates, regulatory research |
| **Trust & Safety Lead** | Trust & Safety | Compliance templates, operator staffing, verification SLAs |
| **Creator Success** | Creator Ops | Supply acquisition, launch cohort support |
| **Marketing / Growth** | Marketing | Demand generation, local campaigns, PR |
| **Engineering** | Engineering | Discovery geo-index, jurisdiction config, feature flags |
| **AI Platform** | Engineering | Jurisdiction document templates in Verification Assist |
| **Data / Analytics** | Analytics | Market health dashboard, liquidity metrics |
| **Finance** | Finance | Payment/payout jurisdiction, tax configuration |
| **Support** | Support | Localized Help content, staffing |

---

## Prerequisites

Before market launch commit:

| Prerequisite | Owner | Verification |
|--------------|-------|--------------|
| Legal market entry assessment complete | Legal | Written memo: can operate, key restrictions |
| Jurisdiction compliance template drafted | Legal + Trust Ops | Document types, category restrictions, sales caps |
| Compliance Engine rules configured in staging | Engineering + Trust Ops | Test creator path for jurisdiction |
| Payment/payout supported for region | Finance + Engineering | Payment Service config |
| Minimum verified supply target defined | Creator Success | e.g., 25 verified creators across 3+ categories |
| Trust operator capacity for projected volume | Trust Lead | Staffing plan with SLA coverage |
| Discovery geo-index includes region | Engineering | Search/browse return results for market centroid |
| Localized Help articles (minimum set) | Support + Product | Cottage food, verification requirements |
| Marketing budget and launch date approved | Marketing + Finance | Campaign plan |
| Platform Settings jurisdiction entry | Trust Ops | `/admin/settings` → jurisdiction library |

---

## Phase-by-Phase Execution

### Phase 0 — Market Assessment (4–8 weeks)

| Step | Actor | Action |
|------|-------|--------|
| 0.1 | Market Launch Lead | Define market boundary (MSA, county, state) and target personas |
| 0.2 | Legal | Research cottage food laws, licensing requirements, prohibited categories, insurance minimums |
| 0.3 | Creator Success | Supply landscape analysis: commercial kitchens, creator communities, competitor presence |
| 0.4 | Marketing | Demand signal: waitlist, search interest, referral density |
| 0.5 | Data | Size TAM/SAM for verified creator supply and trust-seeking customers |
| 0.6 | Market Launch Lead | Go/no-go recommendation to executive sponsor |

**Go criteria (recommended minimums):**

- Legal clearance with no blocking regulatory issues
- Path to 25+ verified creators within 90 days of soft launch
- Commercial kitchen or commissary partner identified (for chef/meal prep supply)
- Trust ops can maintain verification SLAs at projected volume

---

### Phase 1 — Jurisdiction Configuration (2–4 weeks)

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 1.1 | Legal | Finalize compliance document checklist per entity type and kitchen type | Legal memo → Trust Ops |
| 1.2 | Trust Ops | Create jurisdiction template in Platform Settings | Required docs, category restrictions, sales caps, grace periods |
| 1.3 | Engineering | Deploy Compliance Engine rules for jurisdiction | Staging validation |
| 1.4 | AI Platform | Update Verification Assist expected document types for jurisdiction | Extraction templates |
| 1.5 | Product | Update signup jurisdiction picker; creator-facing compliance copy | `/creator/signup`, `/creator/compliance` |
| 1.6 | Trust Ops | Train operators on jurisdiction-specific checklists | Training session + quiz |

**Reference:** [Marketplace Mechanics — Compliance verification](../../product/marketplace-mechanics.md#compliance-verification) · [Trust Service — Compliance Engine](../../engineering/services/trust-service.md)

---

### Phase 2 — Supply Acquisition (4–12 weeks, parallel with Phase 1)

| Step | Actor | Action |
|------|-------|--------|
| 2.1 | Creator Success | Build launch cohort list (target: 25–50 creators) across personas: baker, cottage food, chef, food truck |
| 2.2 | Marketing | Local creator recruitment campaign; partner with commercial kitchens |
| 2.3 | Creator Success | White-glove onboarding for launch cohort — see [Launching a Creator](launching-a-creator.md) |
| 2.4 | Trust & Safety | Prioritize launch cohort verification in queue (tagged, not SLA-breaking for others) |
| 2.5 | Creator Success | Track cohort: signup → verified → first listing → first order |
| 2.6 | Market Launch Lead | Weekly supply standup until minimum threshold met |

**Launch cohort tagging:** Admin flag `launch_market:[market_id]` on creator profiles for reporting.

---

### Phase 3 — Discovery & Product Enablement (2–3 weeks pre-launch)

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 3.1 | Engineering | Enable geo-index for market; configure default search radius | Discovery Service |
| 3.2 | Engineering | Feature flag: `market.[id].enabled` — customer-facing surfaces | Staged rollout |
| 3.3 | Product | Home/browse collections for new market (editorial seed) | `/`, `/browse` |
| 3.4 | AI Platform | Verify Discovery Ranking trust gates active for region | [Discovery Ranking](../../ai/discovery-ranking.md) |
| 3.5 | Marketing | Landing page: `marketplate.com/[market-slug]` with verified creator previews |
| 3.6 | Support | Publish localized Help: verification requirements, cottage food rules | `/help` |

**Discovery invariants:** Unverified creators never appear in results — [Ranking principles](../../product/marketplace-mechanics.md#ranking-principles).

---

### Phase 4 — Soft Launch (2–4 weeks)

| Step | Actor | Action |
|------|-------|--------|
| 4.1 | Market Launch Lead | Enable feature flag for limited audience: waitlist, invite codes |
| 4.2 | Marketing | Soft launch to waitlist; creator share links drive initial demand |
| 4.3 | Data | Monitor liquidity metrics daily (see Metrics section) |
| 4.4 | Creator Success | Daily check on launch cohort order volume; assist stalled creators |
| 4.5 | Trust & Safety | Monitor verification queue depth; adjust staffing |
| 4.6 | Market Launch Lead | Soft launch go/no-go for public launch |

**Soft launch exit criteria:**

- ≥ 25 verified creators with published listings
- ≥ 10 completed orders in market
- Zero P0 trust incidents
- Search returns ≥ 5 results for core queries in market geo
- Verification SLA ≥ 95%

---

### Phase 5 — Public Launch

| Step | Actor | Action |
|------|-------|--------|
| 5.1 | Market Launch Lead | Flip feature flag to public; remove invite requirement |
| 5.2 | Marketing | PR, local influencers, paid acquisition (within budget) |
| 5.3 | Support | Surge staffing for launch week |
| 5.4 | Engineering | Monitor Discovery, Order, Payment latency and error rates |
| 5.5 | All | Launch war room (daily standup × 5 days) |

**Launch week war room agenda:** Orders, verification queue, support ticket volume, liquidity metrics, incidents.

---

### Phase 6 — Post-Launch Stabilization (30–90 days)

| Step | Actor | Action |
|------|-------|--------|
| 6.1 | Data | Weekly market health report to stakeholders |
| 6.2 | Creator Success | Transition launch cohort from white-glove to standard support |
| 6.3 | Marketing | Optimize campaigns based on CAC and conversion data |
| 6.4 | Trust Ops | Review compliance expirations approaching in new market |
| 6.5 | Market Launch Lead | 30-day and 90-day retros; document learnings for next market |
| 6.6 | Product | Backlog prioritization for market-specific UX gaps discovered |

---

## Decision Points

| Decision | Owner | Options | Default |
|----------|-------|---------|---------|
| Enter market | Executive sponsor | Go · No-go · Defer | No-go if legal blocking issue |
| Soft vs. public launch timing | Market Launch Lead | Extend soft · Proceed · Pause | Extend if supply < 25 verified |
| Lower verification bar to accelerate supply | Trust Lead | **Never** · Standard process | Never — [Values — Trust Is the Product](../company/values.md#1-trust-is-the-product) |
| Geographic boundary | Product + Legal | MSA · County · State-wide | Document in ADR |
| Partner exclusivity with commercial kitchen | Business Dev + Legal | Exclusive · Non-exclusive | Legal review required |
| Pause market (trust incident cluster) | Trust Lead + Market Launch Lead | Full pause · Creator-only pause | See [Trust & Safety Escalation](trust-safety-escalation.md) |

---

## Communication Templates

### Template: Launch Cohort Invitation

**From:** Creator Success  
**Channel:** Email

```
Subject: You're invited — Marketplate is coming to [MARKET]

Hi [Creator name],

We're launching Marketplate in [MARKET] and you'd be a great fit for our founding creator cohort.

As a launch creator, you'll get:
• Priority verification review
• Direct access to our Creator Success team
• Featured placement in our [MARKET] launch collection

Ready to join? [Start your application →]

Questions? Reply to this email.

— [Creator Success name]
```

### Template: Market Soft Launch — Waitlist

**From:** Marketing  
**Channel:** Email

```
Subject: Marketplate is live in [MARKET] — you're in

Hi [Name],

You asked to be notified when Marketplate came to [MARKET]. Today's the day.

Discover verified local food creators — bakers, chefs, cottage food makers, and more.

[Browse [MARKET] creators →]

Every creator is verified. Every listing shows allergens and production location.

— The Marketplate team
```

### Template: Internal — Public Launch Go

**Channel:** Slack `#market-launches`

```
🚀 PUBLIC LAUNCH — [MARKET]

Launch Lead: @[name]
Feature flag: market.[id].enabled = PUBLIC
Verified creators: [N]
Listings live: [N]
Soft launch orders completed: [N]

War room: Daily 9am [timezone] this week
On-call: @[eng] @[trust]

Dashboard: [link]
```

---

## Metrics

| Metric | Definition | Target (90 days post-launch) |
|--------|------------|------------------------------|
| Verified creator count | Creators with all trust layers approved in market | ≥ 50 |
| Active creators (30d order) | Creators with ≥ 1 order in 30d | ≥ 30% of verified |
| Search liquidity | Core queries with ≥ 3 results | ≥ 90% of top 20 queries |
| Time to verified (market) | Median signup → verified in market | ≤ 10 business days |
| Completed orders | Total in market | Growth week-over-week |
| Repeat purchase rate | Second order within 60d | Baseline TBD |
| Trust incident rate | P0/P1 per 1000 orders | ≤ platform average |
| CAC : LTV ratio | Marketing efficiency | Within model |

→ [Creator Metrics](../../product/success-metrics-overview.md#creator-metrics) · [Platform Health Metrics](../../product/success-metrics-overview.md#platform-health-metrics)

**Liquidity health signals:** [Marketplace Mechanics — Liquidity](../../product/marketplace-mechanics.md#liquidity)

---

## Post-Incident / Retro

**Required retros:**

- 30-day post-public launch
- 90-day market stabilization review
- Any market pause or P0 incident

**Retro questions:**

1. Did we hit supply thresholds on time?
2. Were jurisdiction rules correct — any false rejects or compliance gaps?
3. Discovery liquidity — zero-result searches?
4. Verification SLA sustainable at volume?
5. What would we do differently for the next market?

**Outputs:** ADR for market decisions; updates to jurisdiction templates; playbook amendments; next market timeline.

---

## Related Documents

### Product & mechanics
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Product Overview](../../product/overview.md)
- [Success Metrics Overview](../../product/success-metrics-overview.md)

### Flows
- [Creator Onboarding Flow](../../pages/flows/creator-onboarding-flow.md)
- [Customer Purchase Flow](../../pages/flows/customer-purchase-flow.md)

### Engineering & AI
- [Trust Service — Compliance Engine](../../engineering/services/trust-service.md)
- [Discovery Service](../../engineering/services/discovery-service.md)
- [Discovery Ranking](../../ai/discovery-ranking.md)
- [Platform Settings](../../pages/admin/platform-settings.md)

### Creator docs
- [Chef Welcome Package](../onboarding/chef-welcome-package.md)

### Related playbooks
- [Launching a Creator](launching-a-creator.md)
- [Launching a New Feature](launching-new-feature.md)
- [Trust & Safety Escalation](trust-safety-escalation.md)
- [Food Safety Incident](food-safety-incident.md)
