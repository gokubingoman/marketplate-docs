# ADR-009: Consumer App Naming

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Brand · Product · Growth

---

## Decision

**Pending founder approval.**

Select the **customer-facing product name** for web and future native apps — unified brand vs. distinct consumer sub-brand.

---

## Background

**Marketplate** is the company and platform name ([Naming Conventions](../brand/naming-conventions.md)). Creators use **Creator OS** / dashboard context. Customers need a clear, trustworthy name for:

- App store listings (Phase 2 native mobile)
- Marketing and PR ([Brand Marketing](../growth/brand-marketing.md))
- Login/signup screens ([Login](../pages/auth/login.md), [Signup](../pages/auth/signup.md))
- Push notifications and email sender names
- Wordmark and logo lockups ([`assets/`](../assets/README.md))

The name must reinforce **trust**, not aggregator convenience (Uber Eats / DoorDash positioning).

---

## Options

| Option | Customer-facing name | Creator-facing | Pros | Cons |
|--------|---------------------|----------------|------|------|
| **A — Unified "Marketplate"** | **Marketplate** | Marketplate for Creators (internal) | One brand; simple; matches company | Generic; doesn't signal "food" |
| **B — Marketplate + tagline** | **Marketplate** with descriptor "Verified local food" | Same platform | Brand clarity without second name | Tagline length in app icon context |
| **C — Distinct consumer sub-brand** | e.g., **Plate**, **LocalPlate**, **TrustPlate** | Marketplate (company) | Consumer app memorability | Brand split cost; confusion risk |
| **D — Geo-qualified launch name** | **Marketplate [City]** at launch | Marketplate | Local PR hook | Doesn't scale; rebrand cost |

---

## Reasoning (recommended direction)

**Recommend Option A — "Marketplate" for all customer-facing surfaces**, with **Option B tagline in marketing only** (not app icon):

1. **Trust thesis** — one brand from discovery through verification badges; no "wrapper app" perception.
2. Creators already promote `eddie.marketplate.app` storefronts — customer app should feel like the same ecosystem.
3. Sub-brands (Option C) mimic aggregator playbooks; research positions against DoorDash/Uber Eats ([Competitive Landscape](../research/competitive-landscape.md)).
4. App store title can use subtitle: *Marketplate — Verified Local Food* without a separate product name.

**Creator context:** "Sell on Marketplate" / "Your Marketplate storefront" — no change.

**Avoid:** "MP," "Market Plate," "MarketplateApp" in customer copy.

---

## Alternatives considered

- **Distinct consumer sub-brand (Option C)** — revisit only if trademark conflict on "Marketplate" in launch jurisdiction (legal check required).
- **Geo-qualified (Option D)** — acceptable for **launch PR only**, not product name.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Single brand equity | Less catchy standalone consumer hook vs. invented sub-brand |
| Creator-customer name alignment | App store SEO relies on category + subtitle |
| Simpler legal/trademark footprint | May need strong visual identity to compensate |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| `brand/naming-conventions.md` | Remove TODO; lock customer app name |
| Auth pages | Title, meta, OG tags |
| Email templates | Sender display name |
| App store (Phase 2) | App title + subtitle |
| `assets/` | Wordmark for customer app |
| Growth campaigns | Unified messaging |

---

## Interim implementation

- Use **Marketplate** in all page specs and help center until ADR accepted
- Design system: placeholder wordmark text "Marketplate"
- App store assets deferred to Phase 2

---

## Related Documents

- [Naming Conventions](../brand/naming-conventions.md)
- [Brand Strategy](../brand/brand-strategy.md)
- [Positioning](../brand/positioning.md)
- [Company Phases — Phase 2 Native Mobile](../roadmap/company-phases.md#phase-2--native-mobile)
