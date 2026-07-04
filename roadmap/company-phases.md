# Marketplate Company Phases

> The long-term product and company roadmap. **The marketplace is Phase 1 — not the whole company.**

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Founders / Product

---

## The framing shift

When Marketplate started, the instinct was:

> *An Etsy for home-cooked food.*

The company we are building is larger:

> **The operating system and trusted commerce platform for independent food businesses.**

The **marketplace is the first product** — it validates real transactions, proves trust, and earns the right to expand. The long-term business is infrastructure that powers independent chefs from **discovery and trust → operations → AI → finance → growth → enterprise**.

This framing influences every product decision. Features that only optimize marketplace GMV without strengthening creator infrastructure belong in later phases — or not at all.

**Related:** [Vision](../company/vision.md) · [Product Overview](../product/overview.md) · [Mission](../company/mission.md)

---

## Phase map

| Phase | Name | Goal | Timeframe (indicative) |
|-------|------|------|------------------------|
| **1** | [Marketplace (Launch)](#phase-1--marketplace-launch) | Validate real transactions | Now — Months 0–18 |
| **2** | [Native Mobile](#phase-2--native-mobile) | Habit + mobility | Months 12–24 |
| **3** | [Delivery Network](#phase-3--delivery-network) | Platform logistics | Years 2–4 |
| **4** | [Chef OS](#phase-4--chef-os) | Shopify for food | Years 2–5 |
| **5** | [AI Kitchen Assistant](#phase-5--ai-kitchen-assistant) | AI employee for every chef | Years 3–6 |
| **6** | [Discovery Platform](#phase-6--discovery-platform) | Spotify × Airbnb for food | Years 3–6 |
| **7** | [Community](#phase-7--community) | Social layer | Years 4–7 |
| **8** | [Subscriptions](#phase-8--subscriptions) | Recurring revenue | Years 3–6 |
| **9** | [Catering](#phase-9--catering) | Events + B2B meals | Years 3–6 |
| **10** | [Financial Products](#phase-10--financial-products) | Banking + capital | Years 5–8 |
| **11** | [Marketplace APIs](#phase-11--marketplace-apis) | Infrastructure for partners | Years 5–10 |
| **12** | [Kitchen Network](#phase-12--kitchen-network) | Shared kitchen economy | Years 6–10 |
| **13** | [Supply Marketplace](#phase-13--supply-marketplace) | B2B supply for chefs | Years 6–10 |
| **14** | [Franchise / Multi-location](#phase-14--franchise--multi-location) | Scaling creators | Years 7–10 |
| **15** | [Enterprise](#phase-15--enterprise) | Institutions + venues | Years 8–10+ |

Phases overlap in practice. Sequencing reflects **dependency order** and **trust maturity** — not strict gates.

Documentation rollout (separate): [Phased Documentation Rollout](phased-rollout.md) · Engineering build order: [Build Readiness](build-readiness.md)

---

## Phase 1 — Marketplace (Launch)

**Goal:** Validate real transactions.

This is the product we document in `pages/`, `engineering/`, and launch first. Success = verified creators completing real orders with repeat customers and operational reliability.

### Buyer

- Browse nearby chefs
- Search, categories, filters
- Pickup + local delivery (creator-managed at launch)
- Checkout, reviews, favorites, follow chefs
- Notifications

### Chef

- Beautiful storefront with custom URL (`eddie.marketplate.app`) — see [Storefronts](#storefronts)
- Menu builder, photos, pricing, availability
- Order management, analytics
- Stripe payouts
- Trust verification (identity, kitchen, food handler)
- Reviews

### Platform

- Identity, kitchen, and food handler verification
- Trust Score v1 — see [Trust Score](#trust-score)
- AI image moderation + AI support (human-gated)
- Admin dashboard, support dashboard
- Refunds, disputes
- Help center — see [Help Center](#help-center)
- [Marketplate Collections](#marketplate-collections) v1 (editorial + staff picks)

**Ship criteria:** Verified GMV, creator retention, trust incident rate near zero, help deflection working.

→ Page specs: [`pages/`](../pages/) · Mechanics: [Marketplace Mechanics](../product/marketplace-mechanics.md)

---

## Phase 2 — Native Mobile

**Goal:** Meet customers and creators where they live — home screen, push, camera, wallet.

| Capability | Customer | Creator |
|------------|----------|---------|
| iOS + Android native apps | ✓ | ✓ |
| Push notifications | Order status, ready for pickup | New orders, messages |
| Live Activities / real-time | Order tracking | Active order queue |
| Saved chefs, location discovery | ✓ | — |
| Camera uploads | — | Verification, menu photos |
| Order tracking | ✓ | Status updates |
| QR pickup | Scan at handoff | Generate pickup QR |
| Apple Wallet / Google Wallet | Order pass, loyalty (future) | — |

v1 launches on responsive web; native follows once core loop is proven.

→ Detail: [Product Roadmap — Mobile Apps](product-roadmap.md#mobile-apps-ios--android)

---

## Phase 3 — Delivery Network

**Goal:** Marketplate becomes a logistics layer — without becoming a restaurant aggregator.

This is when platform-coordinated delivery feels real: drivers, dispatch, GPS, proof of delivery.

| Capability | Notes |
|------------|-------|
| Driver app | Courier onboarding, verification |
| Dispatch engine | Route optimization, batching, zones |
| Live GPS + proof of delivery | Audit trail for trust |
| Scheduled delivery | Meal prep, catering handoff |
| Creator opt-in | Verified kitchen → courier handoff only |

**Not Uber Eats:** supply remains verified creators; creator brand forward; trust visible at checkout.

→ Detail: [Product Roadmap — Platform Delivery](product-roadmap.md#platform-coordinated-delivery)

---

## Phase 4 — Chef OS

**Goal:** Marketplate becomes **Shopify for food** — the system creators run their entire business on.

| Domain | Capabilities |
|--------|--------------|
| **Inventory** | Ingredient tracking, stock alerts |
| **Operations** | Kitchen scheduling, staff management, prep planning, calendar |
| **Recipes** | Recipe management, cost calculator, shopping lists — links to [Recipe Marketplace](product-roadmap.md#recipe-marketplace--royalty-program) |
| **Economics** | Profit calculator, reports, taxes |
| **CRM** | Customer CRM, email, SMS |
| **Growth** | Loyalty, discounts, gift cards, QR ordering |
| **Catering** | Quotes, invoices — expands in Phase 9 |
| **Commerce** | Everything in Phase 1, deepened |

Creators who outgrow spreadsheets never leave the platform.

---

## Phase 5 — AI Kitchen Assistant

**Goal:** Every chef gets an AI employee — **recommends, never replaces judgment.**

Example prompts:

- *"How much profit did I make last month?"*
- *"What should I cook tomorrow?"*
- *"Which menu item has the highest margin?"*
- *"Generate next week's menu."*
- *"Reply to this customer."* (human sends)
- *"Create Instagram content."* (human publishes)
- *"Price this dish."*
- *"Forecast inventory."*

Grounded in creator's own data. Human approval on customer-facing outputs. See [AI Philosophy](../company/constitution.md#ai-philosophy) and [AI Platform](../ai/).

Extends: [Support Assist](../ai/support-assist.md), new **Kitchen Assistant** system (future `ai/kitchen-assistant.md`).

---

## Phase 6 — Discovery Platform

**Goal:** Discovery feels **editorial**, not transactional — Spotify meets Airbnb.

| Surface | Examples |
|---------|----------|
| Trending | Dishes, chefs, cuisines |
| Collections | [Marketplate Collections](#marketplate-collections) at scale |
| Curated | Editor's Picks, holiday, game day, date night |
| Dietary | Vegan, gluten-free, high protein, lunch under $15 |
| Local | Neighborhood guides, "Best Jamaican in Toronto" |
| Meal plans | Weekly bundles across creators |

Trust-weighted ranking remains — no engagement bait. See [Discovery Ranking](../ai/discovery-ranking.md).

---

## Phase 7 — Community

**Goal:** Social layer that **serves commerce and trust** — not engagement for its own sake.

- Follow chefs, followers, favorites, lists, wishlists
- Stories, kitchen updates, photo posts
- Recipes (community + licensed — Phase 4/Recipe Marketplace)
- Live cooking, events
- Community comments, challenges, chef milestones

**Guardrail:** Community features must strengthen creator–customer relationships, not replace verified commerce. See [Product Overview — What we are not](../product/overview.md#what-marketplate-is-not).

---

## Phase 8 — Subscriptions

**Goal:** Recurring revenue for creators and predictable meals for customers.

- Weekly / monthly meal plans
- Family plans, chef memberships
- VIP menus, private drops, exclusive dishes
- Priority ordering windows

High fit for meal prep personas — [Personas](../product/personas.md#meal-prep-business).

---

## Phase 9 — Catering

**Goal:** Events and business meals — quote-based commerce at scale.

- Corporate lunch, office meals, weddings, private chefs
- Bulk ordering, quotes, deposits, contracts, invoices
- B2B buyer personas

Partially anticipated in Phase 4 Chef OS; this phase productizes end-to-end.

---

## Phase 10 — Financial Products

**Goal:** Complete the economic stack for independent food businesses.

| Product | Purpose |
|---------|---------|
| Instant payouts | Cash flow for creators |
| Business banking | Accounts tied to Marketplate OS |
| Working capital / kitchen loans | Growth financing |
| Equipment financing | Ovens, vehicles, packaging lines |
| Tax estimates, expense tracking | Compliance + planning |
| Revenue forecasting | AI-assisted (Phase 5) |

**Huge opportunity** — requires licensing, partnerships, legal depth in `legal/`. Trust Score and transaction history become underwriting signals.

---

## Phase 11 — Marketplace APIs

**Goal:** Marketplate becomes **infrastructure others build on**.

| API | Purpose |
|-----|---------|
| Ordering API | Embed checkout |
| Chef / Menu API | Sync catalog |
| Payments API | Payouts + splits |
| Storefront API | White-label surfaces (enterprise) |
| Verification API | Trust-as-a-service for partners |
| Analytics API | Creator + partner insights |
| Partner API | Webhooks, OAuth, sandbox |

Aligns with [Vision — Infrastructure Layer](../company/vision.md#4-infrastructure-layer-for-the-local-food-economy).

---

## Phase 12 — Kitchen Network

**Goal:** Coordinate the physical layer — shared commercial kitchens.

- Kitchen rentals, booking, equipment rentals
- Partner kitchens, Marketplace-certified kitchens
- Tenant compliance coordination

Connects creators without their own facilities to verified production environments.

---

## Phase 13 — Supply Marketplace

**Goal:** Chefs buy supplies through Marketplate — packaging to insurance.

- Packaging, ingredients, containers, equipment, aprons, printers, POS
- Wholesale pricing, verified suppliers
- Integrated with inventory (Phase 4) and prep planning

B2B supply — distinct from customer-facing marketplace but same creator relationship.

---

## Phase 14 — Franchise / Multi-location

**Goal:** Tools for creators who scale beyond a single kitchen.

- Multiple kitchens, regional menus, central inventory
- Staff permissions, location analytics, brand management
- Franchise-style governance without franchise extractive economics

---

## Phase 15 — Enterprise

**Goal:** Institutions and venues — same trust stack at scale.

- Restaurants (independent, not chains-first), hotels, sports venues
- Ghost kitchens, airports, hospitals, schools, corporate campuses
- Enterprise SLAs, custom verification, API-first deployment

**Positioning:** Enterprise uses Marketplate **because** of verification depth — not despite it. Not a pivot to anonymous food service.

---

# Signature Platform Features

Cross-phase capabilities that define the Marketplate brand.

---

## Trust Score

One composite score — the **Superhost equivalent** for food creators.

| Signal | Weight (TBD) |
|--------|--------------|
| Identity verification | Required gate |
| Kitchen verification | Required gate |
| Reviews (verified purchase) | High |
| Repeat customer rate | High |
| Refund rate | Inverse |
| Response time | Medium |
| Order completion rate | High |
| Food safety incidents | Inverse (hard penalty) |
| AI confidence (verification, moderation) | Assist only — not public alone |

`TODO(decision):` Component weights and public vs internal visibility — see [Glossary](../company/glossary.md).

→ Standards: [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)

---

## AI Kitchen Verification

Upload kitchen photos → AI assists human review:

- Cleanliness, equipment, packaging workspace
- Potential hazards, image authenticity (not stock photos)
- Flags for Trust & Safety queue — **never auto-approve**

→ [Verification Assist](../ai/verification-assist.md) · [Trust Verification Flow](../pages/flows/trust-verification-flow.md)

---

## AI Food Verification

Before dishes go live:

- Food quality and presentation signals
- Duplicate / stock image detection
- Safety indicators ( labeling visible, etc.)
- Image moderation

Human approval before publish. Ties to [Moderation Assist](../ai/moderation-assist.md).

---

## Marketplate Verified

Premium badge — **hard to earn, high trust, better discovery ranking**.

Distinct from baseline "Verified Creator" (Phase 1 minimum to sell). Requires sustained Trust Score, compliance history, and operational excellence.

→ Discovery: [Discovery Ranking](../ai/discovery-ranking.md) hard gates + boost

---

## Chef Levels

Progression system for creators:

| Level | Meaning |
|-------|---------|
| **New Chef** | Onboarding; not yet verified |
| **Verified Chef** | Passed identity + kitchen + compliance — can sell |
| **Trusted Chef** | Sustained Trust Score + volume |
| **Top Chef** | Top percentile in market |
| **Marketplate Signature** | Editorial + metrics — platform co-marketing |
| **Invite Only** | Exclusive tier; limited supply |

Levels unlock features (analytics depth, Collections placement, instant payout eligibility) — not pay-to-win ranking.

---

## Storefronts

Every chef owns a permanent home:

```
eddie.marketplate.app
```

Not just another listing — a **owned brand surface** on Marketplate infrastructure. Custom URL, story, menu, verification badges, shareable link.

→ Page spec: [Creator Storefront](../pages/customer/creator-storefront.md) · [Storefront Settings](../pages/creator/storefront-settings.md)

---

## Help Center

Production-quality help comparable to Stripe, Shopify, or Eventbrite:

- Complete docs for buyers, chefs, support, trust & safety, operations
- Source: [`docs/help-center/`](../docs/help-center/) → product surface [`pages/customer/help.md`](../pages/customer/help.md)

---

## Marketplate Collections

**Signature discovery feature** — curated, shareable, searchable editorial collections.

Examples:

- 🇯🇲 Best Jamaican Food in Toronto
- 🌱 Vegan Weeknight Picks
- 🍝 Italian Comfort Food
- 👨‍🍳 New Chefs This Week
- ⭐ Marketplate Staff Picks
- 🎉 Game Day Favorites
- 💪 High Protein Meals
- 🍱 Lunch Under $15

**Creators:** Marketplate editorial, chefs (future), community (Phase 7) — with trust gates on who can curate.

Collections make discovery feel **editorial instead of transactional**. Phase 1 ships staff/editorial collections; Phase 6 scales programmatic + community curation.

→ Page spec: [Browse](../pages/customer/browse.md) · [Discovery Service](../engineering/services/discovery-service.md)

---

## Recipe Marketplace & Royalty Program

Creators license recipes; other chefs import with attribution; **original author earns royalty per order**.

→ Full spec: [Product Roadmap — Recipe Marketplace](product-roadmap.md#recipe-marketplace--royalty-program) · Phase 4+ Chef OS integration

---

# Roadmap governance

| Action | Process |
|--------|---------|
| Add phase or feature | Update this doc + feature doc when committed |
| Promote to active build | ADR in [`decisions/`](../decisions/) + page/engineering specs |
| Change company framing | Update [Vision](../company/vision.md), [Product Overview](../product/overview.md), [Executive Summary](../docs/internal/executive-summary.md) |

**Filter (every phase):** *Does this make independent food creators more trusted and more capable of running their business?*

---

## Related Documents

- [Product Roadmap](product-roadmap.md) — supplementary detail on mobile, delivery, recipes
- [Build Readiness](build-readiness.md)
- [Phased Documentation Rollout](phased-rollout.md)
- [Vision](../company/vision.md)
- [Product Overview](../product/overview.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
- [Executive Summary](../docs/internal/executive-summary.md)
