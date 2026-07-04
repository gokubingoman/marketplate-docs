# Architecture Decision Records (ADRs)

Documented founder and architecture decisions for Marketplate. When a `TODO(decision):` resolves, publish or update an ADR here and cross-link from affected docs.

**Template:** [`templates/adr-template.md`](../templates/adr-template.md)  
**Governing doc:** [Founding Constitution](../company/constitution.md)

---

## Status key

| Status | Meaning |
|--------|---------|
| **Proposed** | Options analyzed; awaiting founder acceptance |
| **Accepted** | Decision locked; implement against this record |
| **Deprecated** | Superseded by a later ADR |
| **Superseded** | Replaced — see successor ADR |

---

## Decision index

| ADR | Title | Status | Blocks |
|-----|-------|--------|--------|
| [ADR-001](adr-001-geographic-launch-market.md) | Geographic launch market | **Proposed** | Legal, GTM, compliance templates, discovery defaults |
| [ADR-002](adr-002-pricing-model.md) | Creator pricing model | **Proposed** | Feature gating, revenue forecast, marketing |
| [ADR-003](adr-003-commission-structure.md) | Marketplace commission structure | **Proposed** | Checkout fees, payouts, legal fee disclosure |
| [ADR-004](adr-004-auth-provider.md) | Authentication provider | **Proposed** | Identity service, login UX, admin MFA |
| [ADR-005](adr-005-identity-verification-vendor.md) | Identity verification vendor | **Proposed** | Creator onboarding, Trust Service |
| [ADR-006](adr-006-stripe-connect-model.md) | Stripe Connect account model | **Proposed** | Payment service, payout timing, onboarding |
| [ADR-007](adr-007-trust-score-weights-visibility.md) | Trust Score weights and visibility | **Proposed** | Discovery ranking, creator dashboard, badges |
| [ADR-008](adr-008-analytics-bi-stack.md) | Analytics and BI stack | **Proposed** | Event pipeline, dashboards, data warehouse |

---

## Engineering stubs

Until ADRs are **Accepted**, engineering may implement against documented **assumptions** in each ADR's "Interim implementation" section. Do not ship production config (Stripe, auth, legal text) against assumptions without founder sign-off.

---

## Related Documents

- [Build Readiness](../roadmap/build-readiness.md)
- [Documentation Gaps](../roadmap/documentation-gaps.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
