# Product Onboarding

> Onboarding guide for Product Managers and Product Designers with PM responsibilities. **What to do** and **why**.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Reports to:** Head of Product

Index: [Employee Training](README.md)

---

## Role Purpose

Product defines **what** Marketplate builds and **why** — translating the trust thesis into specs that engineering, design, operations, and support can implement without ambiguity.

**Why this role exists:** Independent food creators are underserved by restaurant tools and generic e-commerce. Product judgment prevents feature bloat that erodes the clarity trust requires. Every feature must trace to [Product Overview](../../product/overview.md) pillars and serve verified creators — not delivery-aggregator parity.

Product owns documentation completeness: **documentation is production code.** An undocumented feature is incomplete.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | Shared foundation + [Product Philosophy](../../company/company-philosophy.md#product-philosophy) | Internalize decision framework table |
| **1–2** | [Product Overview](../../product/overview.md) + [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Map pillars to existing features |
| **2–3** | [Personas](../../product/personas.md) — all creator types + End Customer | Name primary persona for any spec |
| **3–4** | [Pages README](../../pages/README.md) + 3 page specs in your domain | Understand page doc template |
| **4** | [Success Metrics](../../product/success-metrics-overview.md) | Know north star and trust metrics |
| **5** | Shadow verification or support workflow | See product decisions in operations |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Founding Constitution — Document Standards](../../company/constitution.md#document-standards) | Feature, page, SOP templates |
| [Company Philosophy — Product](../../company/company-philosophy.md#product-philosophy) | Ship/deprioritize framework |
| [Product Overview](../../product/overview.md) | Scope boundaries — what we are not |
| [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Trust model invariants |
| [Personas](../../product/personas.md) | Every spec names primary persona |
| [Value Props](../../product/value-props.md) | Creator and customer outcomes |
| [Phased Rollout](../../roadmap/phased-rollout.md) | Documentation phase plan |

### Week 2–4 (role depth)

| Document | Why |
|----------|-----|
| [Information Architecture](../../pages/information-architecture.md) | Navigation and surface map |
| [Navigation Model](../../pages/navigation-model.md) | Cross-surface consistency |
| [Engineering Architecture Overview](../../engineering/architecture-overview.md) | Feasibility and service boundaries |
| [Service Catalog](../../engineering/service-catalog.md) | Which service owns what |
| [AI Platform README](../../ai/README.md) | AI-first workflow constraints |
| [Design Principles](../../design-system/principles.md) | Calm, trust-visible UX intent |
| [Feature doc template](../../templates/feature-doc-template.md) | How to write specs |

### Admin and flows (trust-critical product)

| Document | Why |
|----------|-----|
| [Trust Verification Flow](../../pages/flows/trust-verification-flow.md) | Core marketplace gate |
| [Admin Dashboard](../../pages/admin/admin-dashboard.md) | Internal product quality bar |
| [Verification Queue](../../pages/admin/verification-queue.md) | Human-in-the-loop UX |
| [Moderation Queue](../../pages/admin/moderation-queue.md) | Enforcement UX |

---

## Systems Access

| System | Access level | Purpose |
|--------|--------------|---------|
| **Documentation repo** | Write | Specs, page docs, ADRs |
| **Admin console** | Read (operator shadow) | See ops workflows your specs enable |
| **Analytics** | View | Metrics validation |
| **Design files** | View/comment | Partner with design |
| **Issue tracker / roadmap** | Write | Prioritization and delivery |
| **Staging environment** | User | Acceptance testing |

---

## Decision Framework

Apply [Product Philosophy decision table](../../company/company-philosophy.md#product-philosophy):

| Question | Pass → Ship/prioritize | Fail → Deprioritize |
|----------|------------------------|---------------------|
| Increases verifiable trust? | ✓ | Unless trust-neutral + high creator value |
| Serves independent food creators specifically? | ✓ | May belong elsewhere |
| Cottage food operator can use without support? | ✓ | Simplify or add guided flows |
| Complexity disproportionate to value? | Cut scope | — |
| Documented before implementation? | Proceed | Write spec first |

### When philosophies conflict

1. **Trust philosophy wins** — then clarity, then long-term scalability
2. Document tradeoffs in an [ADR](../../decisions/)
3. Trust-impacting changes require T&S review

### Spec completion checklist

Before marking a feature "ready for engineering":

- [ ] Feature doc with all [constitution-required sections](../../company/constitution.md#feature-documents)
- [ ] Page specs updated for affected screens in [pages/](../../pages/)
- [ ] API requirements documented (Phase 3+)
- [ ] Operations: owner, SLA, escalation in feature doc or linked SOP
- [ ] AI involvement documented per [AI doc template](../../templates/ai-doc-template.md) if applicable
- [ ] Primary persona declared; anti-persona noted

**Why:** Undocumented behavior becomes tribal knowledge. Tribal knowledge does not scale internationally.

---

## Escalation

| Scenario | Escalate to | Action |
|----------|-------------|--------|
| Trust vs growth conflict | T&S + Head of Product | Trust wins; document if exception needed |
| Scope requires founder decision | Executive | Prefix `TODO(decision):` in doc |
| Engineering feasibility blocks trust requirement | Eng lead + T&S | Redesign — do not weaken trust |
| Legal/compliance ambiguity | Legal + T&S | Block ship until resolved |
| Cross-team priority conflict | Head of Product | Frame with metrics and persona impact |

Playbooks: [Launching a New Feature](../playbooks/launching-new-feature.md)

---

## Success Criteria

### Week 1
- [ ] Written one-page summary: "What Marketplate is not" with examples
- [ ] Mapped 5 existing page specs to product pillars
- [ ] Identified primary persona for assigned product area

### Day 30
- [ ] Ship or advance one feature doc through eng review with full template compliance
- [ ] Participate in T&S review for one trust-touching change
- [ ] Zero specs merged without Related Documents links

### Day 90
- [ ] Own a metric on [Success Metrics](../../product/success-metrics-overview.md) dashboard
- [ ] Author one ADR for a significant product decision
- [ ] Run creator feedback session before major workflow change

---

## Related Documents

- [Employee Training](README.md)
- [Design Onboarding](design-onboarding.md) — Partner role
- [Engineering Onboarding](engineering-onboarding.md) — Partner role
- [docs/standards/Marketplate Standards](../standards/marketplate-standards.md)
- [company/](../../company/) · [product/](../../product/) · [pages/admin/](../../pages/admin/)
