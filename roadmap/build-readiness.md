# Build Readiness

> What exists, what's missing, and what must be decided before engineering implementation begins.

**Status:** Active  
**Last updated:** 2026-07-03

---

## Can we start building?

**Yes — for core product engineering.** Phases 1–3 of documentation are complete: company strategy, every page spec, API catalogs, data models, service architecture, and AI system specs. An engineering team can begin implementation against `pages/`, `engineering/`, and `design-system/`.

**Not yet — for operating a live marketplace at scale.** Phases 4–5 and several founder decisions remain before public launch with real money, real food, and real regulatory exposure.

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

---

## Documentation gaps (block or risk launch)

| Gap | Folder | Why it matters | Priority |
|-----|--------|----------------|----------|
| **Legal & compliance** | `legal/` | Terms, privacy, food sale regulations, creator agreements, refund policy as enforceable legal text | **Launch blocker** |
| **Operations SOPs** | `operations/` | Verification review steps, dispute handling, food safety incident procedures at task level | **Launch blocker** |
| **Customer support playbooks** | `support/` | Macros, escalation trees, SLA execution | High |
| **Analytics definitions** | `analytics/` | Event taxonomy implementation, dashboards, data governance | High |
| **Security policies** | `engineering/` (Phase 5) | Formal infosec policy, incident response, access reviews | High |
| **Growth & GTM** | `growth/` | Launch market acquisition plan | Medium (parallel to build) |
| **Competitive research** | `research/` | Ongoing intelligence | Medium |
| **ADRs for open tech decisions** | `decisions/` | Auth provider, verification vendor, cloud region | Medium |
| **Documentation QA pass** | `roadmap/documentation-gaps.md` | Cross-link validation, consistency audit | Before launch |
| **Visual brand assets** | `assets/` | Logo, wordmark, photography direction (empty today) | Medium |
| **Diagrams** | `diagrams/` | Architecture visuals for onboarding (optional) | Low |

---

## Founder decisions required (block product config)

These appear as `TODO(decision):` across the repo. Implementation can proceed with assumptions, but **launch cannot** without resolution:

| Decision | Affects |
|----------|---------|
| **Geographic launch market** | Compliance templates, verification partners, discovery defaults, GTM |
| **Pricing model** | Creator tiers, feature gating, revenue forecasting |
| **Commission structure** | Checkout fees, payout UX, unit economics |
| **Trust Score weights & visibility** | Discovery ranking, creator dashboard, customer-facing badges |
| **Auth provider** | Login, sessions, SSO |
| **Identity verification vendor** | Onboarding flow, Trust Service integration |
| **Stripe Connect model** | Payout timing, fee pass-through |
| **Consumer app naming** | Brand lockups, app store presence |

Track decisions in [`decisions/`](../decisions/) as ADRs when resolved.

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

### Phase E — Launch readiness (requires Phase 4–5 docs)

1. Legal docs live
2. SOPs trained and staffed
3. Support queue operational
4. Security review complete
5. Soft launch in founding market

---

## What is NOT required to start coding

- Recipe marketplace / royalty program (future — see [Product Roadmap](product-roadmap.md))
- International expansion
- Full analytics warehouse
- Every playbook executed (playbooks guide ops; code can precede some)
- Phase 5 growth/research docs

---

## Related Documents

- [Product Roadmap](product-roadmap.md)
- [Phased Documentation Rollout](phased-rollout.md)
- [Product Overview](../product/overview.md)
- [Executive Summary](../docs/internal/executive-summary.md)
