# Personas

> Detailed user archetypes for creators, customers, and internal operators. Every feature and page spec must name its primary persona.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product

---

## Purpose

Personas translate Marketplate's strategy into human context. They define goals, frustrations, trust requirements, and success criteria for each user type we serve.

This document does not duplicate brand voice or company values — see [Values](../company/values.md) and [Brand Voice](../brand/voice-and-tone.md). It focuses on **behavior, jobs-to-be-done, and product implications**.

For product scope and pillars, see [Product Overview](overview.md).

---

## Persona Index

| Persona | Type | Primary pillar |
|---------|------|----------------|
| [Independent Chef](#independent-chef) | Creator | Operations + Trust |
| [Meal Prep Business](#meal-prep-business) | Creator | Operations + Commerce |
| [Baker](#baker) | Creator | Trust + Discovery |
| [Caterer](#caterer) | Creator | Commerce + Operations |
| [Food Truck Operator](#food-truck-operator) | Creator | Discovery + Operations |
| [Cottage Food Operator](#cottage-food-operator) | Creator | Trust + Compliance |
| [Pop-Up Kitchen](#pop-up-kitchen) | Creator | Discovery + Commerce |
| [Commercial Kitchen Operator](#commercial-kitchen-operator) | Creator | Operations + Trust |
| [End Customer (Trust-Seeking Buyer)](#end-customer-trust-seeking-buyer) | Customer | Trust + Discovery |
| [Platform Operations (Internal)](#platform-operations-internal) | Internal | Trust + Platform health |

---

## Shared Creator Attributes

All creator personas share a baseline profile unless a sub-section explicitly overrides it.

| Attribute | Description |
|-----------|-------------|
| **Relationship to Marketplate** | Supply-side user; owns catalog, pricing, fulfillment, and customer communication |
| **Core job** | Sell food directly to customers while building a trusted brand |
| **Shared goals** | More orders, fewer operational headaches, clear compliance path, fair economics, repeat customers |
| **Shared frustrations** | Fragmented tools (Instagram DMs + spreadsheets + Venmo), unclear food regulations, no verification story, platform fees without value |
| **Trust requirements** | Must complete identity and kitchen verification to earn "Verified Creator" status |
| **Primary surfaces** | Creator dashboard, catalog manager, order queue, analytics, compliance center, customer messaging |
| **Success signal** | Sustained order volume with high completion rate and positive reviews |

Creator-specific sections below describe **differentiating context** — not a different product.

---

## Independent Chef

**Archetype:** Solo or small-team chef selling prepared meals, meal kits, or specialty items under a personal brand.

### Profile

| Field | Detail |
|-------|--------|
| **Business size** | 1–3 people |
| **Typical volume** | 20–150 orders/week |
| **Production** | Home kitchen (where legal), rented commercial kitchen, or shared commissary |
| **Channels today** | Instagram, word of mouth, farmers markets, occasional pop-ups |

### Goals

- Turn culinary skill into a sustainable income without opening a restaurant
- Present a professional brand that justifies premium pricing
- Spend time cooking, not chasing payments and order details

### Frustrations

- Customers ask "Are you licensed?" repeatedly — no easy way to prove legitimacy
- Order details scattered across DMs; mistakes happen on modifications and allergies
- No single place to show menu, story, and availability

### Product implications

- **Trust:** Personal brand tied to verified identity; chef story prominent on profile
- **Operations:** Simple production queue; allergy and dietary flags on every order
- **Discovery:** Photography-forward profile; "Chef's table" or limited-batch merchandising
- **Commerce:** Pre-order windows and capacity limits to prevent overcommitment

### Key metrics

Order completion rate, repeat customer rate, average order value, review score — see [Creator Metrics](success-metrics-overview.md#creator-metrics).

---

## Meal Prep Business

**Archetype:** Structured weekly or subscription-oriented business selling planned meals in batches.

### Profile

| Field | Detail |
|-------|--------|
| **Business size** | 2–10 people |
| **Typical volume** | 100–1,000+ meals/week |
| **Production** | Commercial kitchen or commissary |
| **Channels today** | Website, local ads, gym partnerships, Instagram |

### Goals

- Predictable weekly volume and production planning
- Reduce churn through reliable quality and clear nutrition information
- Scale without custom software development

### Frustrations

- Cut-off times and batch planning are manual and error-prone
- Subscription logic hacked together in spreadsheets
- Hard to communicate macro/nutrition/allergen info consistently

### Product implications

- **Operations:** Batch production view; cut-off datetime enforcement; capacity by week
- **Commerce:** Recurring or multi-meal bundles; subscription-ready order patterns (even if v1 is manual renewal)
- **Trust:** Nutrition and ingredient transparency standardized in catalog
- **Discovery:** Filter by dietary goal (high protein, vegan, etc.)

### Key metrics

Weekly active order rate, batch utilization, subscription renewal proxy (repeat weekly purchase), refund rate.

---

## Baker

**Archetype:** Artisan or cottage baker selling bread, pastries, cakes, and custom orders.

### Profile

| Field | Detail |
|-------|--------|
| **Business size** | 1–5 people |
| **Typical volume** | 30–300 orders/week; spiky around holidays |
| **Production** | Cottage kitchen or commercial bakery space |
| **Channels today** | Pre-orders via DM, farmers markets, local coffee shop wholesale (informal) |

### Goals

- Manage lead times for custom cakes and holiday rushes
- Showcase craftsmanship; justify premium over grocery bakery
- Reduce no-shows and last-minute cancellations on custom work

### Frustrations

- Custom order details lost in message threads
- Deposit and cancellation policies enforced inconsistently
- Seasonal demand swamps manual processes

### Product implications

- **Commerce:** Deposits, custom order forms, lead-time rules per SKU
- **Operations:** Production calendar with daily bake capacity
- **Trust:** Allergen labeling (nuts, gluten, dairy) mandatory and visible pre-checkout
- **Discovery:** Seasonal collections; "Available this weekend" urgency without dark patterns

### Key metrics

Custom order fulfillment rate, on-time ready rate, cancellation/no-show rate, review mentions of quality/consistency.

---

## Caterer

**Archetype:** Event-focused food business serving groups — corporate lunches, weddings, private parties.

### Profile

| Field | Detail |
|-------|--------|
| **Business size** | 3–25 people |
| **Typical volume** | 5–30 events/month; high AOV |
| **Production** | Commercial kitchen; on-site execution for some events |
| **Channels today** | Referrals, event planners, Google, legacy catering platforms |

### Goals

- Qualified leads with clear event parameters (headcount, date, budget, venue)
- Quote-to-book workflow without endless back-and-forth
- Deposit collection and change-order discipline

### Frustrations

- Unqualified inquiries waste time
- Scope creep on menu and headcount after quote
- Payment timing misaligned with ingredient purchasing

### Product implications

- **Commerce:** Inquiry → quote → deposit → final payment flow; minimum lead time by event size
- **Operations:** Event calendar separate from daily retail queue; staffing notes
- **Trust:** Event photos, verified kitchen, insurance/compliance docs available on request
- **Discovery:** "Catering" as distinct fulfillment type with filters for headcount and date

### Key metrics

Quote-to-book conversion, average event AOV, deposit collection rate, post-event review rate.

---

## Food Truck Operator

**Archetype:** Mobile vendor with location-dependent availability and fast-turnaround service.

### Profile

| Field | Detail |
|-------|--------|
| **Business size** | 1–6 people |
| **Typical volume** | Highly variable by location/day |
| **Production** | On-truck; commissary for prep |
| **Channels today** | Twitter/X location posts, Instagram, location apps |

### Goals

- Drive pre-orders and skip-the-line pickup at known locations
- Communicate real-time location and sell-out status
- Build loyal following across rotating spots

### Frustrations

- Customers arrive after sell-out
- Location updates are manual and stale
- Line management chaos during peak hours

### Product implications

- **Discovery:** Location schedule, "Open now" status, map integration
- **Operations:** Real-time inventory/sell-out; pickup window slots
- **Commerce:** Mobile-optimized checkout; quick reorder for regulars
- **Trust:** Commissary verification + mobile unit identification

### Key metrics

Pre-order rate vs. walk-up, sell-out accuracy, location schedule adherence, repeat customer rate by route.

---

## Cottage Food Operator

**Archetype:** Home-based producer operating under cottage food laws with category and sales limits.

### Profile

| Field | Detail |
|-------|--------|
| **Business size** | 1–2 people (often side business) |
| **Typical volume** | 10–80 orders/week within legal caps |
| **Production** | Home kitchen registered under cottage food program |
| **Channels today** | Facebook, farmers markets, friends and family |

### Goals

- Operate legally with confidence; understand what can and cannot be sold
- Access customers beyond immediate network
- Professional presence without restaurant-level overhead

### Frustrations

- Cottage food rules vary by jurisdiction — fear of accidental violation
- Customers don't understand why certain items aren't available
- Competing with unlicensed sellers undercuts trust

### Product implications

- **Trust:** Jurisdiction-aware compliance checklist; cottage food badge; category restrictions enforced in catalog
- **Operations:** Sales cap tracking where applicable; clear labeling requirements
- **Commerce:** Pickup-first; delivery only where legally permitted
- **Discovery:** "Cottage food" filter for customers who want to support home producers

### Key metrics

Compliance completion rate, catalog restriction adherence (zero violations), conversion on verified cottage badge.

---

## Pop-Up Kitchen

**Archetype:** Temporary or recurring culinary concept without permanent storefront — collabs, supper clubs, market stalls.

### Profile

| Field | Detail |
|-------|--------|
| **Business size** | 1–8 people per event |
| **Typical volume** | Episodic — 20–200 covers per event |
| **Production** | Rented kitchen + temporary service location |
| **Channels today** | Eventbrite, Instagram, mailing lists |

### Goals

- Fill seats or pre-order slots before event date
- Coordinate ticketing-like capacity with food production
- Build audience for next pop-up announcement

### Frustrations

- Each event feels like starting from zero
- Refund policy ambiguity when events sell out or cancel
- No persistent profile — customers forget between events

### Product implications

- **Discovery:** Event-based listings with date, location, remaining capacity
- **Commerce:** Pre-pay required; waitlist; automatic close at capacity
- **Operations:** Event mode in dashboard distinct from ongoing catalog
- **Trust:** Per-event kitchen/venue verification linkage; clear cancellation policy

### Key metrics

Sell-through rate before event, no-show rate, follower-to-attendee conversion, repeat attendance rate.

---

## Commercial Kitchen Operator

**Archetype:** Shared kitchen facility hosting multiple food businesses — may also operate own brand.

### Profile

| Field | Detail |
|-------|--------|
| **Business size** | 5–50+ tenants |
| **Typical volume** | N/A at facility level; enables tenant volume |
| **Production** | Licensed commercial kitchen with multiple bays |
| **Channels today** | Direct tenant relationships, local food ecosystem partnerships |

### Goals

- Verify facility once; reduce per-tenant compliance friction
- Optional visibility for tenants using the kitchen
- Streamline health inspection and documentation

### Frustrations

- Each tenant uses different tools; kitchen admin is paperwork-heavy
- Tenants misrepresent production location
- No marketplace connects verified kitchen to customer trust

### Product implications

- **Trust:** Kitchen-level verification with tenant linkage; inspection doc repository
- **Operations:** Multi-tenant permissions; kitchen admin role (see below)
- **Discovery:** Optional "Produced at [Kitchen Name]" badge on tenant listings
- **Commerce:** Tenants operate independently; kitchen does not centralize payments by default

### Key metrics

Tenant verification attach rate, kitchen doc renewal compliance, tenant GMV enabled.

**Note:** Commercial kitchen operators may use a distinct **Kitchen Admin** role — a sub-persona of creator ops with facility-wide visibility. Detailed permissions belong in engineering access docs.

---

## End Customer (Trust-Seeking Buyer)

**Archetype:** Local buyer who wants high-quality food from a real person or small business — not an anonymous ghost kitchen.

### Profile

| Field | Detail |
|-------|--------|
| **Demographics** | Broad; skews urban/suburban, 25–55, values quality and local economy |
| **Purchase frequency** | Weekly to monthly depending on category |
| **Spend sensitivity** | Willing to pay premium for trust, quality, and story — not price-shopping delivery apps |
| **Channels today** | Instagram discovery, farmers markets, friend referrals, Google search |

### Goals

- Find food that fits dietary needs and quality standards
- Know who made it, where it was made, and that it's safe
- Reliable pickup or delivery with clear timing
- Support local creators intentionally

### Frustrations

- Cannot tell if social media seller is licensed or safe
- Allergen information incomplete or buried
- Inconsistent communication on order status
- Bad experiences with unverified sellers erode category trust

### Jobs-to-be-done

| Job | Marketplate response |
|-----|---------------------|
| "Find trusted local food matching my diet" | Verified discovery with filters |
| "Understand what I'm buying before I pay" | Transparent product pages with ingredients, allergens, fulfillment |
| "Know my order is handled" | Order tracking and creator communication |
| "Buy again from someone I trust" | Order history, favorites, repeat purchase |

### Product implications

- **Trust:** Verification badges, kitchen transparency, review integrity — non-negotiable at every funnel step
- **Discovery:** Calm, photography-rich browsing; no clutter
- **Commerce:** Clear total cost, fulfillment choice, cancellation policy before payment
- **Operations:** Proactive status updates; easy support path

### Key metrics

Repeat purchase rate, time-to-trust (first order completion), NPS/CSAT, support contact rate — see [Customer Metrics](success-metrics-overview.md#customer-metrics).

---

## Platform Operations (Internal)

**Archetype:** Trust & Safety, Creator Success, or Marketplace Operations team member responsible for platform integrity and creator enablement.

### Profile

| Field | Detail |
|-------|--------|
| **Team size** | Scales with marketplace GMV and geography |
| **Primary tools** | Admin console, verification queues, dispute resolution, compliance dashboards |
| **Accountability** | Human approval on high-stakes trust decisions per [AI Philosophy](../company/constitution.md#ai-philosophy) |

### Goals

- Maintain verification integrity and food safety standards
- Resolve disputes fairly with complete audit trails
- Enable creators to succeed without manual hand-holding at scale
- Detect fraud, policy violations, and quality degradation early

### Frustrations

- Incomplete creator submissions clog queues
- Tools that don't surface risk signals proactively
- Ambiguous policy without documented SOPs

### Jobs-to-be-done

| Job | Product requirement |
|-----|---------------------|
| Review verification submissions | Queue with checklist, document preview, approve/reject/request-info |
| Handle disputes | Case management linked to order, messages, policies |
| Monitor marketplace health | Dashboards for trust metrics, anomaly flags |
| Support creators | Internal notes visible across creator lifecycle |

### Product implications

- **Admin OS:** First-class internal product — not an afterthought SQL console
- **AI assist:** AI recommends; human approves on verification and moderation
- **Audit:** Every action logged with actor, timestamp, and rationale
- **SLAs:** Measurable targets per workflow — see [`operations/`](../operations/)

### Key metrics

Verification turnaround time, dispute resolution time, false positive/negative rates on moderation, creator activation rate — see [Trust Metrics](success-metrics-overview.md#trust-metrics) and [Platform Health Metrics](success-metrics-overview.md#platform-health-metrics).

---

## Persona × Pillar Matrix

Quick reference for prioritization discussions.

| Persona | Trust | Discovery | Commerce | Operations |
|---------|:-----:|:---------:|:--------:|:----------:|
| Independent Chef | ● | ● | ● | ●● |
| Meal Prep Business | ● | ● | ●● | ●● |
| Baker | ●● | ● | ● | ● |
| Caterer | ● | ● | ●● | ●● |
| Food Truck | ● | ●● | ● | ●● |
| Cottage Food | ●● | ● | ● | ● |
| Pop-Up Kitchen | ● | ●● | ●● | ● |
| Commercial Kitchen | ●● | ○ | ○ | ●● |
| End Customer | ●● | ●● | ● | ● |
| Platform Ops | ●● | ○ | ● | ●● |

Legend: ●● = primary · ● = significant · ○ = secondary

---

## Using Personas in Documentation

Every [page specification](../pages/) and [feature document](../templates/feature-doc-template.md) must declare:

1. **Primary persona** — who this is built for
2. **Secondary persona** — if applicable
3. **Anti-persona** — who might appear but is not the design target (e.g., enterprise restaurant chain manager)

When personas conflict, **trust-seeking customer safety** and **verified creator compliance** take precedence over growth shortcuts.

---

## Related Documents

- [Product Overview](overview.md)
- [Value Propositions](value-props.md)
- [Marketplace Mechanics](marketplace-mechanics.md)
- [Success Metrics Overview](success-metrics-overview.md)
- [Founding Constitution](../company/constitution.md)
- [Mission](../company/mission.md)
- [Company Philosophy](../company/company-philosophy.md)
- [Brand Strategy](../brand/brand-strategy.md)
- [Phased Rollout](../roadmap/phased-rollout.md)
