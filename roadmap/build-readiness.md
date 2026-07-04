# Build Readiness

> What exists, what's missing, and what must be decided before engineering implementation begins.

**Status:** Active  
**Last updated:** 2026-07-03

---

## Can we start building?

**Yes — for core product engineering.** Phases 1–3 of documentation are complete: company strategy, every page spec, API catalogs, data models, service architecture, and AI system specs. An engineering team can begin implementation against `pages/`, `engineering/`, and `design-system/`.

**Not yet — for public launch at scale.** Documentation Phases 1–5 are structurally complete. Remaining launch blockers are **founder decisions**, **legal counsel review** of framework drafts, **cross-link remediation**, and **visual brand assets** — not missing documentation folders.

---

## Documentation complete (ready to implement)

| Area | Location | Status |
|------|----------|--------|
| Company identity & philosophy | `company/` | ✓ |
| Brand & voice | `brand/` | ✓ |
| Product strategy & mechanics | `product/` | ✓ |
| Page specs (37 screens) | `pages/` | ✓ |
| Design system | `design-system/` | ✓ |
| Engineering architecture & APIs | `engineering/` | ✓ |
| AI platform specs | `ai/` | ✓ |
| Creator onboarding & standards | `docs/onboarding/`, `docs/standards/` | ✓ |
| Help center content (source) | `docs/help-center/` | ✓ |
| Operational playbooks | `docs/playbooks/` | ✓ |
| Employee training | `docs/training/` | ✓ |
| Internal briefs | `docs/internal/` | ✓ |
| Operations SOPs | `operations/` | ✓ Phase 4 |
| Customer support playbooks | `support/` | ✓ Phase 4 |
| Legal & compliance (framework) | `legal/` | ✓ Phase 5 — counsel review required |
| Security policies | `engineering/` | ✓ Phase 5 |
| Analytics definitions | `analytics/` | ✓ Phase 5 |
| Growth & GTM | `growth/` | ✓ Phase 5 |
| Competitive research | `research/` | ✓ Phase 5 |

---

## Launch blockers (post-documentation)

| Blocker | Why it matters | Priority |
|---------|----------------|----------|
| **Legal counsel review** | All `legal/` docs are framework drafts — not enforceable until counsel approves | **Launch blocker** |
| **Founder ADR acceptance** | 8 Proposed ADRs in `decisions/` — options analyzed; production config blocked until Accepted | **Launch blocker** |
| **Cross-link remediation** | ✓ Complete — internal link scan clean | — |
| **Visual brand assets** | `assets/README.md` placeholder; logo/wordmark pending | Medium |
| **Architecture diagrams** | `diagrams/` empty — optional for onboarding | Low |

---

## Founder decisions required (block product config)

These appear as `TODO(decision):` across the repo. Implementation can proceed with assumptions, but **launch cannot** without resolution:

| Decision | ADR | Affects |
|----------|-----|---------|
| **Geographic launch market** | [ADR-001](../decisions/adr-001-geographic-launch-market.md) | Compliance templates, verification partners, discovery defaults, GTM |
| **Pricing model** | [ADR-002](../decisions/adr-002-pricing-model.md) | Creator tiers, feature gating, revenue forecasting |
| **Commission structure** | [ADR-003](../decisions/adr-003-commission-structure.md) | Checkout fees, payout UX, unit economics |
| **Trust Score weights & visibility** | [ADR-007](../decisions/adr-007-trust-score-weights-visibility.md) | Discovery ranking, creator dashboard, customer-facing badges |
| **Auth provider** | [ADR-004](../decisions/adr-004-auth-provider.md) | Login, sessions, SSO |
| **Identity verification vendor** | [ADR-005](../decisions/adr-005-identity-verification-vendor.md) | Onboarding flow, Trust Service integration |
| **Stripe Connect model** | [ADR-006](../decisions/adr-006-stripe-connect-model.md) | Payout timing, fee pass-through |
| **Analytics / BI stack** | [ADR-008](../decisions/adr-008-analytics-bi-stack.md) | Event pipeline, dashboards, warehouse |
| **Consumer app naming** | — *(not yet ADR)* | Brand lockups, app store presence |

Track decisions in [`decisions/`](../decisions/) as ADRs when resolved. **8 Proposed ADRs** published — see [Decision Index](../decisions/README.md).

---

## Recommended build sequence

### Phase A — Engineering foundation (can start now)

1. Repo setup, CI/CD, environments per [Infrastructure Overview](../engineering/infrastructure-overview.md)
2. Identity + auth scaffolding
3. Core data model from [Core Entities](../engineering/data/core-entities.md)
4. Design system implementation from `design-system/components/`

### Phase B — Trust path (MVP critical path)

1. Creator signup → identity → kitchen → compliance flows
2. Admin verification queue
3. Trust Service + audit logging
4. Verified-to-sell gate on catalog

### Phase C — Commerce loop

1. Storefront + catalog (customer-facing)
2. Cart + checkout + Stripe
3. Order lifecycle + notifications
4. Creator order queue + fulfillment

### Phase D — Discovery & growth

1. Search, browse, home featured
2. Reviews post-completion
3. Help center integration from `docs/help-center/`
4. Analytics instrumentation

### Phase E — Launch readiness (requires counsel + decisions)

1. Legal docs counsel-approved and published
2. SOPs trained and staffed
3. Support queue operational
4. Security review complete
5. Cross-link remediation pass
6. Soft launch in founding market

---

## What is NOT required to start coding

- Recipe marketplace / royalty program (future — see [Product Roadmap](product-roadmap.md))
- International expansion
- Full analytics warehouse
- Every playbook executed (playbooks guide ops; code can precede some)
- Phase 5 growth/research docs (now complete — execution still requires launch market decision)

---

## Related Documents

- [Product Roadmap](product-roadmap.md)
- [Phased Documentation Rollout](phased-rollout.md)
- [Product Overview](../product/overview.md)
- [Executive Summary](../docs/internal/executive-summary.md)
