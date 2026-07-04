# Engineering Onboarding

> Onboarding guide for software engineers. **What to do** and **why** Marketplate builds systems this way.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Engineering  
**Reports to:** Engineering Lead

Index: [Employee Training](README.md)

---

## Role Purpose

Engineering implements the trusted marketplace operating system — services, APIs, data models, and observability that let creators run businesses and customers buy with confidence.

**Why this role exists:** Marketplate must scale internationally across diverse creator types and regulatory environments. Clever architectures become bottlenecks when authors leave. We optimize for **readability, maintainability, and modularity** — boring technology over clever technology. See [Engineering Philosophy](../../company/company-philosophy.md#engineering-philosophy).

Every API is documented before implementation. Every trust-critical path has audit trails and explicit failure modes.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | Shared foundation + [Engineering README](../../engineering/README.md) | Orient to repo structure |
| **1–2** | [Architecture Overview](../../engineering/architecture-overview.md) | System diagram mental model |
| **2** | [Service Catalog](../../engineering/service-catalog.md) | Know service boundaries |
| **2–3** | [API Overview](../../engineering/api/api-overview.md) + [Authentication](../../engineering/api/authentication.md) | REST conventions, roles, permissions |
| **3–4** | [Data Model Overview](../../engineering/data/data-model-overview.md) + [Core Entities](../../engineering/data/core-entities.md) | Entity relationships |
| **4** | [Data Flow](../../engineering/data-flow.md) — purchase + verification paths | End-to-end traces |
| **5** | Local dev environment + first small PR (doc fix or test) | Contribution workflow |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Company Philosophy — Engineering](../../company/company-philosophy.md#engineering-philosophy) | Technology and failure-mode preferences |
| [Company Philosophy — Documentation](../../company/company-philosophy.md#documentation-philosophy) | Spec before code |
| [Architecture Overview](../../engineering/architecture-overview.md) | System design principles |
| [Service Catalog](../../engineering/service-catalog.md) | Single responsibility per service |
| [Integration Patterns](../../engineering/integration-patterns.md) | Events, external integrations |
| [Infrastructure Overview](../../engineering/infrastructure-overview.md) | Environments, deployment |
| [Engineering doc template](../../templates/engineering-doc-template.md) | Service doc standard |

### Week 2–4 (by assignment)

| Service area | Start here |
|--------------|------------|
| Auth & users | [Identity Service](../../engineering/services/identity-service.md) |
| Verification & moderation | [Trust Service](../../engineering/services/trust-service.md) |
| Catalog & storefronts | [Catalog Service](../../engineering/services/catalog-service.md) |
| Orders & checkout | [Order Service](../../engineering/services/order-service.md) |
| Payments & payouts | [Payment Service](../../engineering/services/payment-service.md) |
| Notifications | [Notification Service](../../engineering/services/notification-service.md) |
| Search & ranking | [Discovery Service](../../engineering/services/discovery-service.md) |

### API surfaces

| API | Document |
|-----|----------|
| Customer-facing | [Customer API](../../engineering/api/customer-api.md) |
| Creator-facing | [Creator API](../../engineering/api/creator-api.md) |
| Internal admin | [Admin API](../../engineering/api/admin-api.md) |

### Trust and AI integration

| Document | Why |
|----------|-----|
| [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Invariants you must not break in code |
| [AI Platform README](../../ai/README.md) | Human-in-the-loop boundaries |
| [Trust Verification Flow](../../pages/flows/trust-verification-flow.md) | Verification pipeline |
| [Page specs](../../pages/) | API requirements per screen |

---

## Systems Access

| System | Access level | Purpose |
|--------|--------------|---------|
| **Source repos** | Write (via PR) | Application code |
| **Documentation repo** | Write | Specs, ADRs, service docs |
| **CI/CD** | Developer | Build, test, deploy pipelines |
| **Staging** | Developer | Integration testing |
| **Production** | On-call rotation (after training) | Incident response |
| **Observability** | View | Logs, metrics, traces — required on every feature |
| **Secrets manager** | Scoped | No secrets in code or docs |

---

## Decision Framework

| Decision | Prefer | Avoid |
|----------|--------|-------|
| Technology | Proven, team-readable | Bleeding-edge without ops maturity |
| Service boundaries | Single responsibility | God services |
| Trust-critical data | Audit trails, immutable logs | Shared mutable state without audit |
| Failure handling | Documented graceful degradation | Silent failures on trust paths |
| Observability | Structured logging, metrics, tracing | "Add monitoring later" |
| API changes | Versioned, documented first | Undocumented APIs to unblock frontend |

Significant architecture decisions → [ADR](../../templates/adr-template.md) in [decisions/](../../decisions/).

### Pre-merge checklist

- [ ] Spec/API doc updated if behavior changed
- [ ] Trust-critical paths have audit logging
- [ ] Failure modes handled — no silent drops on verification/payment
- [ ] Tests cover trust-critical paths (not just vanity coverage)
- [ ] Related page specs linked in PR description

**Why audit trails:** Financial and verification data without audit history is a compliance and incident-response liability.

---

## Escalation

| Scenario | Escalate to | Action |
|----------|-------------|--------|
| Production incident | On-call → incident commander | Post-mortem doc required for trust-impacting |
| Security vulnerability | Security lead | No public disclosure until patched |
| Trust invariant conflict in implementation | Eng lead + Product + T&S | Do not ship weakening change |
| AI auto-action request from stakeholder | AI Platform + T&S | Default: human approval on high-stakes |
| Cross-service ownership dispute | Eng lead + ADR | Clarify service boundary |

---

## Success Criteria

### Week 1
- [ ] Trace one customer purchase and one verification submission through [Data Flow](../../engineering/data-flow.md)
- [ ] Local environment running with tests passing
- [ ] Merged first PR (code or documentation)

### Day 30
- [ ] Own a service or API area with on-call shadow complete
- [ ] Shipped feature with observability (logs + metric) and doc updates
- [ ] Zero undocumented API endpoints in owned area

### Day 90
- [ ] Author one ADR for architectural decision
- [ ] Participate in production incident post-mortem
- [ ] Review PR for trust-critical audit trail compliance

---

## Related Documents

- [Employee Training](README.md)
- [AI Systems Onboarding](ai-systems-onboarding.md) — If working on AI integration
- [Product Onboarding](product-onboarding.md) — Spec partnership
- [engineering/](../../engineering/)
- [ai/](../../ai/)
- [pages/admin/](../../pages/admin/)
- [docs/standards/](../standards/)
