# Acquisition Channels

> Creator and customer acquisition channels, channel mix by launch phase, and CAC framework.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Growth · Marketing · Finance

---

## Purpose

This document defines **where Marketplate acquires creators and customers**, how channels are prioritized across launch phases, and how we measure acquisition efficiency. It implements the sequencing model in [Go-to-Market Strategy](go-to-market-strategy.md) with actionable channel tactics.

Every channel must pass the **trust filter**: if a channel attracts unverified supply, discount hunters, or requires misleading claims, it is deprioritized or excluded.

---

## Channel Philosophy

| Principle | Application |
|-----------|-------------|
| **Organic and creator-led first** | Lowest CAC, highest trust, aligns with creator-owned relationships |
| **Paid is amplification, not foundation** | Paid channels activate after supply density and conversion proof |
| **Persona-specific, not generic** | Meal prep operators discover differently than bakers — see [Personas](../product/personas.md) |
| **Measure quality, not just volume** | Track verification completion and first-order rate, not signups alone |
| **CAC payback over CAC minimization** | A higher-CAC creator who retains and drives GMV beats a cheap churned signup |

→ Anti-metrics: [Success Metrics Overview — Anti-Metrics](../product/success-metrics-overview.md#anti-metrics-do-not-optimize)

---

## Creator Acquisition Channels

### Channel map

| Channel | Phase | Cost model | Trust fit | Primary personas |
|---------|-------|------------|-----------|------------------|
| **Founder / team network** | Pre-launch | Low | High | All |
| **Commercial kitchen partnerships** | Pre-launch → ongoing | Medium | High | Meal prep, Independent Chef, Commercial Kitchen |
| **Culinary schools & incubators** | Pre-launch → ongoing | Medium | High | Independent Chef, Baker, Caterer |
| **Cottage food associations** | Pre-launch → ongoing | Low–Medium | High | Cottage Food |
| **Creator referrals** | Soft launch → ongoing | Medium (incentive TBD) | High | All verified creators |
| **Content / SEO (creator-facing)** | Pre-launch → ongoing | Medium (content cost) | High | All |
| **Local events & pop-ups** | Soft launch | Medium | High | Pop-Up, Food Truck |
| **Paid social (creator-targeted)** | Public launch | High | Medium | Broad — requires trust-forward creative |
| **Paid search (creator-intent)** | Public launch | High | Medium | "Sell food online," "cottage food platform" |
| **Influencer / creator advocates** | Public launch | Medium–High | Medium | Requires vetting and trust alignment |

### Channel detail: High-priority (Phase 0–2)

#### Founder and team network

| Attribute | Detail |
|-----------|--------|
| **Objective** | Seed founding creator cohort (5–25) |
| **Tactics** | Direct outreach to known operators; warm intros; local food community presence |
| **Success metric** | Applications from qualified operators; verification completion rate |
| **Owner** | Founders + Growth |

#### Commercial kitchen partnerships

| Attribute | Detail |
|-----------|--------|
| **Objective** | Pipeline of meal prep, chef, and tenant operators with verified production environments |
| **Tactics** | Partnership MOU; co-hosted info sessions; tenant onboarding kits; verification fast-path *(same standards, better education)* |
| **Success metric** | Verified creators per partner kitchen; time to verified |
| **Owner** | Growth + Creator Success |
| **Cross-link** | [Positioning — Ecosystem Partners](../brand/positioning.md#tertiary-ecosystem-partners) |

#### Cottage food associations

| Attribute | Detail |
|-----------|--------|
| **Objective** | Reach home-based operators with compliance anxiety |
| **Tactics** | Educational workshops ("building a trusted cottage food business"); compliance content; association newsletter features |
| **Messaging** | Lead with trust and compliance — not "easy money" |
| **Success metric** | Cottage food persona verification rate; compliance doc completion |
| **Owner** | Growth + Trust (content review) |

#### Creator-facing content / SEO

| Attribute | Detail |
|-----------|--------|
| **Objective** | Inbound pipeline for creator-intent searches |
| **Topic clusters** | Cottage food compliance, meal prep business setup, food business verification, selling food locally |
| **Guardrail** | No claims about verification speed or approval guarantees |
| **Success metric** | Organic applications; content → application conversion |
| **Owner** | Marketing + Product (SEO) |

→ Content strategy: [Brand Marketing — Content Strategy](brand-marketing.md#content-strategy)

### Channel detail: Scale (Phase 3+)

#### Creator referrals

| Attribute | Detail |
|-----------|--------|
| **Objective** | Expand supply through trusted creator networks |
| **Mechanics** | `TODO(decision):` Referral incentive structure — must not incentivize verification shortcuts |
| **Success metric** | Referred creator verification completion rate; referred creator first-order rate |
| **Guardrail** | Referrer must be verified; referred creator completes full verification |

#### Paid social and search (creator)

| Attribute | Detail |
|-----------|--------|
| **Objective** | Scale creator pipeline after organic proof |
| **Activation gate** | Public launch; CAC model calibrated; trust-forward creative approved |
| **Targeting** | Interest: cottage food, meal prep business, food entrepreneurship; geo: `[Launch Market]` |
| **Creative** | Creator stories, verification proof points — not "start selling in 5 minutes" |
| **Success metric** | Cost per verified creator; time to first order |

---

## Customer Acquisition Channels

### Channel map

| Channel | Phase | Cost model | Trust fit | Notes |
|---------|-------|------------|-----------|-------|
| **Creator share links** | Soft launch → ongoing | Zero | Highest | Primary channel — creator-owned URL |
| **Creator social promotion** | Soft launch → ongoing | Zero (creator cost) | High | Creator posts storefront; platform provides assets |
| **Word of mouth / referrals** | Soft launch → ongoing | Low | High | Post-positive first-order experience |
| **Email (creator audience imports)** | Soft launch | Low | High | Creator-initiated; platform provides templates |
| **Local SEO / content (buyer-facing)** | Soft launch → ongoing | Medium | High | "Verified local food in [Launch Market]" |
| **Marketplate Collections** | Public launch | Low (editorial) | High | Editorial discovery — [Company Phases](../roadmap/company-phases.md#marketplate-collections) |
| **Community partnerships** | Public launch | Medium | High | Local food orgs, health/wellness communities |
| **PR / earned media** | Public launch | Medium | High | Trust stories, not discount announcements |
| **Paid social (customer-targeted)** | Public launch | High | Medium | Geo-fenced; trust creative only |
| **Paid search (buyer-intent)** | Public launch | High | Medium | "Verified meal prep [city]" — not "cheap food delivery" |

### Channel detail: Primary (Phase 2–3)

#### Creator share links

| Attribute | Detail |
|-----------|--------|
| **Objective** | Convert creator existing audiences to first orders |
| **Mechanics** | `creator.marketplate.app` URLs; QR codes; share assets in creator dashboard |
| **Attribution** | `creator_attributed` first-touch in analytics |
| **Success metric** | % first orders via share link; share link → order conversion |
| **CS support** | Share coaching in [Education Playbooks](../docs/customer-success/education-playbooks.md) |
| **Product** | [Storefront Settings](../pages/creator/storefront-settings.md) |

**Why primary:** Aligns with creator-owned customer relationships — [Value Propositions — Creator](../product/value-props.md#creator-value-propositions).

#### Local SEO and buyer content

| Attribute | Detail |
|-----------|--------|
| **Objective** | Capture trust-seeking search intent in `[Launch Market]` |
| **Keyword themes** | Verified local food, meal prep [city], cottage food [city], local baker [city] |
| **Avoid** | "Cheap food delivery," "fast food near me" — wrong intent |
| **Success metric** | Organic sessions → registration → first order |

#### Marketplate Collections

| Attribute | Detail |
|-----------|--------|
| **Objective** | Editorial discovery driving browse → order |
| **Examples** | "Best Jamaican Food in [Launch Market]," "Vegan Weeknight Picks," "New Chefs This Week" |
| **Trust gate** | Only verified creators in collections |
| **Success metric** | Collection view → storefront → order conversion |

→ Discovery: [Browse](../pages/customer/browse.md) · [Discovery Ranking](../ai/discovery-ranking.md)

### Channel detail: Amplification (Phase 3)

#### Paid customer acquisition

| Attribute | Detail |
|-----------|--------|
| **Activation gate** | ≥50 verified creators; completion rate ≥98% for 4 weeks; CAC model approved |
| **Geo** | `[Launch Market]` only — no national spend |
| **Creative** | Verified creator photography, trust badges, creator names — not stock food imagery |
| **Landing** | Browse or Collection — never empty category pages |
| **Exclusions** | No discount-first ads; no fake urgency; no competitor comparison on delivery speed |

---

## Channel Mix by Launch Phase

| Phase | Creator channel mix (target %) | Customer channel mix (target %) |
|-------|-------------------------------|--------------------------------|
| **Pre-launch** | Network 40%, partnerships 35%, content 15%, events 10% | Waitlist only — no customer acquisition |
| **Soft launch** | Partnerships 30%, referrals 20%, content 25%, network 25% | Share links 60%, creator social 25%, word of mouth 15% |
| **Public launch** | Content 25%, partnerships 20%, referrals 20%, paid 20%, events 15% | Share links 35%, SEO 20%, collections 15%, PR 10%, paid 15%, other 5% |
| **Steady state (Month 6+)** | Content 30%, referrals 25%, partnerships 15%, paid 20%, other 10% | Share links 30%, SEO 20%, repeat/organic 25%, collections 10%, paid 15% |

Percentages are directional — recalibrate monthly against CAC and quality metrics.

→ Phase definitions: [Launch Plan](launch-plan.md)

---

## CAC Framework

### Definitions

| Term | Definition |
|------|------------|
| **CAC (Creator)** | Total creator acquisition spend + allocated team cost / new **verified** creators in period |
| **CAC (Customer)** | Total customer acquisition spend / new customers with **completed first order** in period |
| **Blended CAC** | Total acquisition spend / total new verified creators + new paying customers |
| **Creator CAC payback** | Creator CAC / monthly platform revenue per creator (fees × GMV) |
| **Customer CAC payback** | Customer CAC / gross profit per customer in payback window |

**Critical:** CAC denominators use **verified creators** and **completed orders** — not raw signups or registrations. Unverified signups are an anti-metric.

### Cost allocation

| Cost bucket | Creator CAC | Customer CAC |
|-------------|-------------|--------------|
| Paid media spend | ✓ (creator campaigns) | ✓ (customer campaigns) |
| Partnership fees / events | ✓ | ✓ (if buyer-focused) |
| Content production | ✓ (creator content) | ✓ (buyer content) |
| Referral incentives | ✓ | ✓ |
| Growth team salary (allocated) | ✓ (% by effort) | ✓ (% by effort) |
| Creator Success onboarding (allocated) | ✓ (activation portion) | — |
| Brand / PR (shared) | Split by campaign objective | Split by campaign objective |

### CAC targets (internal placeholders)

Targets require fee model ADR and launch market calibration. Use as review framework until baselines exist.

| Metric | Soft launch | Public launch (Month 3) | Steady state |
|--------|-------------|-------------------------|--------------|
| Creator CAC | Track only | ≤ $X per verified creator | ↓ or stable with quality |
| Customer CAC | Track only | ≤ $X per first order | ≤ 3× monthly gross profit |
| Creator CAC payback | — | ≤ 6 months | ≤ 4 months |
| Customer CAC payback | — | ≤ 2 orders | ≤ 1.5 orders |
| Creator-attributed customer % | ≥50% | ≥40% | Monitor — organic is healthy |

`TODO(decision):` Set dollar targets after commission structure and launch market ADR.

### CAC quality gates

A channel with low CAC but poor downstream metrics is **not efficient**:

| Downstream metric | Minimum for channel continuation |
|-------------------|----------------------------------|
| Creator verification completion rate | ≥70% |
| Creator first listing rate (14-day) | ≥80% |
| Creator first order rate (30-day) | ≥50% |
| Customer repeat purchase rate (30-day) | ≥25% |
| Order completion rate (channel cohort) | ≥98% |

**Kill rule:** Pause any paid channel where CAC rises 50% WoW without conversion improvement, or where trust guardrails degrade.

---

## Attribution Model

### First-touch attribution (Phase 1)

| Source | Event / UTM pattern |
|--------|---------------------|
| Creator share link | `?ref=creator_{id}` or dedicated subdomain |
| Collection | `?ref=collection_{slug}` |
| Paid campaign | Standard UTM: source, medium, campaign |
| Organic search | Landing page referrer |
| Direct | No referrer; may include creator word-of-mouth |

### Creator-attributed customer acquisition

**Definition:** Customer whose first completed order originated from a creator share link or creator-specific referral code.

→ CS metric: [Success Metrics — Creator-attributed acquisition](../docs/customer-success/success-metrics.md#buyer-conversion-cs-influenced-via-education)

### Multi-touch (future)

Phase 1 uses first-touch for simplicity. Multi-touch model deferred to [Analytics](../analytics/) maturity.

---

## Persona × Channel Matrix

Prioritize channels by creator persona — see [Personas](../product/personas.md).

| Persona | Top creator channels | Top customer channels (via persona) |
|---------|---------------------|-------------------------------------|
| Independent Chef | Kitchen partnerships, culinary schools, content | Creator share links, local SEO |
| Meal Prep Business | Commercial kitchens, health communities | Creator share links, meal prep SEO |
| Baker | Cottage food associations, local events, Instagram | Creator social, seasonal collections |
| Caterer | Culinary schools, B2B networks | Creator share links, corporate referrals |
| Food Truck | Events, pop-ups, location-based social | Creator social, event-driven discovery |
| Cottage Food Operator | Cottage food associations, compliance content | Local trust SEO, community partnerships |
| Pop-Up Kitchen | Events, local food press | Event-driven, creator social |
| Commercial Kitchen Operator | B2B kitchen networks | Tenant creator share links |

---

## Channels We Do Not Use

| Channel / tactic | Reason |
|------------------|--------|
| **Discount aggregator sites** | Attracts price shoppers; erodes trust positioning |
| **Buy email lists** | Low quality; CAN-SPAM risk; wrong audience |
| **"Anyone can sell food" marketplaces as channel** | Wrong trust model |
| **Fake review / astroturf campaigns** | Violates trust thesis |
| **Incentivized reviews** | Violates review integrity — [Marketplace Mechanics](../product/marketplace-mechanics.md) |
| **Dark pattern retargeting** | Fake urgency, hidden fees — see [Brand Marketing — Guardrails](brand-marketing.md#marketing-guardrails) |
| **Unverified creator promotion** | Platform invariant violation |

---

## Phase 2 — Native Mobile

When [Company Phases — Phase 2](../roadmap/company-phases.md#phase-2--native-mobile) ships, add:

| Channel | Notes |
|---------|-------|
| App Store Optimization (ASO) | Trust-forward screenshots; creator stories |
| Push notification re-engagement | Order status, creator updates — not discount spam |
| App install campaigns | Geo-fenced; post-liquidity only |
| QR pickup → app install | Fulfillment moment conversion |

---

## Reporting Cadence

| Report | Audience | Cadence | Contents |
|--------|----------|---------|----------|
| **Channel performance** | Growth team | Weekly | Spend, CAC, conversion by channel |
| **Creator pipeline** | Growth + CS | Weekly | Applications, verification funnel, activation |
| **Customer acquisition** | Growth + Product | Weekly | First orders by source, repeat rate by cohort |
| **CAC payback review** | Growth + Finance | Monthly | Payback trends, channel ROI, budget reallocation |
| **Persona channel review** | Growth + CS + Product | Quarterly | Channel × persona performance |

→ Aligns with [CS Reporting Cadence](../docs/customer-success/success-metrics.md#reporting-cadence)

---

## Open Decisions

| Decision | Channel impact |
|----------|----------------|
| `TODO(decision):` Geographic launch market | All geo-targeted channels, partnership list, SEO keywords |
| `TODO(decision):` Commission structure | Creator acquisition economics, paid channel viability |
| `TODO(decision):` Creator referral incentive | Referral channel design |
| `TODO(decision):` Customer referral program | Word-of-mouth channel mechanics |

---

## Related Documents

- [Growth README](README.md)
- [Go-to-Market Strategy](go-to-market-strategy.md)
- [Brand Marketing](brand-marketing.md)
- [Launch Plan](launch-plan.md)
- [Value Propositions](../product/value-props.md)
- [Personas](../product/personas.md)
- [Customer Lifecycle](../docs/customer-success/customer-lifecycle.md)
- [Success Metrics Overview](../product/success-metrics-overview.md)
- [Positioning](../brand/positioning.md)
- [Discovery Ranking](../ai/discovery-ranking.md)
