# Marketplate Partner Handbook

> How Marketplate operates — for internal partners, senior hires, advisors with operational scope, and contractors with decision authority.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Audience:** Partners, senior hires, operational advisors

---

## Purpose

This handbook explains how Marketplate is organized, how decisions are made, and how product, engineering, operations, trust, AI, and documentation work together in practice. It assumes familiarity with Marketplate's mission and vision — start with [Company Overview](company-overview.md) or [Executive Summary](executive-summary.md) if you are new.

The authoritative governing document is the [Founding Constitution](../../company/constitution.md). When this handbook and another document conflict, the Constitution wins.

---

## Company Structure and Priorities

### What We Are Building

Marketplate is the **trusted marketplace and operating system for independent food creators**. We serve two external user types and one internal type:

| User type | Definition |
|-----------|------------|
| **Creator** | Independent food entrepreneur selling through Marketplate |
| **Customer** | Buyer seeking verified, local food from a real person or small business |
| **Platform operator** | Internal team member maintaining trust, compliance, and marketplace health |

Three application surfaces map to these users — see [Information Architecture](../../pages/information-architecture.md):

| Surface | Entry | Audience |
|---------|-------|----------|
| Customer Marketplace | `/` | End customers |
| Creator OS | `/dashboard` | Verified and onboarding creators |
| Admin / Trust & Safety | `/admin` | Platform operators |

### Priority Stack

When priorities conflict, apply this order:

1. **Trust** — Verification, food safety, transparency, review integrity
2. **Creator value** — Independent food entrepreneurs building durable businesses
3. **Clarity** — Plain language, explicit states, honest communication
4. **Quality** — Fewer things, built exceptionally well
5. **Long-term scalability** — Maintainable architecture, international readiness
6. **Velocity** — Speed matters, but never ahead of items 1–5

This stack derives from [Values](../../company/values.md) and [Company Philosophy](../../company/company-philosophy.md). When trust and growth conflict, we choose trust.

### Mission Filter

Before committing resources to any initiative, ask:

1. Does this help an independent creator run a better business?
2. Does this increase verifiable trust?
3. Is the quality bar world-class?
4. Does this scale without sacrificing clarity?

If the primary beneficiary is a delivery aggregator or corporate restaurant chain, it does not belong on our roadmap.

---

## Product Philosophy

### Four Pillars

Every feature maps to at least one pillar. Features requiring explicit justification if they strengthen none:

| Pillar | Principle |
|--------|-----------|
| **Trust** | Never sacrifice trust for growth |
| **Discovery** | Optimize for fit and confidence, not infinite scroll |
| **Commerce** | Creators own customer relationship; platform facilitates |
| **Operations** | Reduce uncertainty on every interaction |

Pillars form a reinforcing loop: Trust → Discovery → Commerce → Operations → Trust. Breaking any link weakens the whole product. See [Product Overview — Pillar Interdependencies](../../product/overview.md#pillar-interdependencies).

### Product Decision Framework

| Question | Pass | Fail |
|----------|------|------|
| Does this increase verifiable trust? | Ship or prioritize | Deprioritize unless trust-neutral and high creator value |
| Does this serve independent food creators specifically? | Continue | Reconsider — may belong elsewhere |
| Can a cottage food operator use this without support? | Continue | Simplify or add guided flows |
| Does this add complexity disproportionate to value? | Cut scope | — |
| Is this documented before implementation begins? | Proceed to build | Write spec first |

### Explicit Anti-Patterns

- Feature parity chasing with delivery aggregators
- Configuration-heavy designs that avoid product judgment
- Shipping trust-impacting features without verification workflow review
- "Launch now, document later"
- Open marketplace without verification
- Pay to hide negative reviews
- Promoted listings without verification badge
- Overselling capacity at checkout

Marketplace rules and invariants: [Marketplace Mechanics](../../product/marketplace-mechanics.md).

### Scope Boundaries

**In scope (v1 strategic intent):** Verified creator onboarding, storefront and order management, customer discovery and purchase, pickup and delivery coordination, reviews, creator payouts, admin and trust & safety tooling.

**Out of scope (v1):** Dine-in reservations, restaurant POS wedge, national perishable shipping as default, creator wholesale marketplace, white-label licensing, cryptocurrency checkout.

Full boundaries: [Product Overview — Product Scope Boundaries](../../product/overview.md#product-scope-boundaries).

---

## Documentation Approach

### Core Principle

**Documentation is production code.** Incomplete documentation means the feature is incomplete.

This repository is Marketplate's **institutional memory** — designed for engineers, designers, operators, executives, investors, and AI agents. It must eventually contain everything required to design, build, operate, and scale the company internationally.

### Documentation Standards

| Principle | Practice |
|-----------|----------|
| Spec before code | Feature docs and page specs precede implementation |
| Link, don't duplicate | Cross-reference related systems; one canonical source per topic |
| Dual audience | Write for humans and AI agents |
| Evergreen | Include status, version, last updated, owner |
| Traceability | Significant decisions recorded as ADRs in [`decisions/`](../../decisions/) |
| Related Documents | Every page ends with connected systems |

### Document Types and Templates

| Type | Template | Required sections |
|------|----------|-------------------|
| Feature | [`feature-doc-template.md`](../../templates/feature-doc-template.md) | Purpose, requirements, UX, engineering, security, ops, support |
| Page | [`page-doc-template.md`](../../templates/page-doc-template.md) | Layout, interactions, responsive behavior, states, API requirements |
| SOP | [`sop-template.md`](../../templates/sop-template.md) | Owner, trigger, SLA, AI/human responsibilities, escalation, audit |
| Engineering | [`engineering-doc-template.md`](../../templates/engineering-doc-template.md) | Architecture, failure modes, monitoring, scaling, DR |
| AI system | [`ai-doc-template.md`](../../templates/ai-doc-template.md) | Evaluation, fallbacks, confidence thresholds, human approval |
| ADR | [`adr-template.md`](../../templates/adr-template.md) | Decision, alternatives, tradeoffs, impact |

### Before Marking Work Complete

- [ ] Feature doc exists using the appropriate template
- [ ] Page specs updated for affected screens
- [ ] API documented before implementation (engineering domain)
- [ ] Related Documents section links to connected systems
- [ ] Significant decisions recorded in `decisions/`
- [ ] Glossary updated if new terms introduced — [Glossary](../../company/glossary.md)

### Repository Structure

```
/company          Mission, vision, values, philosophy
/brand            Brand strategy, positioning, voice
/design-system    Principles, foundations, components
/product          Product strategy, personas, mechanics
/pages            Page specifications (every screen)
/engineering      Architecture, APIs, infrastructure
/operations       SOPs, workflows (Phase 4)
/ai               AI systems and prompts
/legal            Compliance, policies (Phase 5)
/support          Customer support playbooks (Phase 4)
/docs/internal    Partner-facing synthesis documents
/roadmap          Product and documentation roadmaps
/decisions        Architecture Decision Records
/templates        Reusable document templates
```

Rollout status: [Phased Rollout](../../roadmap/phased-rollout.md).

---

## Decision Making

### Philosophy Conflict Resolution

When domain philosophies conflict:

1. **Trust philosophy wins**
2. Then clarity
3. Then long-term scalability

Apply the values decision sequence from [Values — Using Values in Decisions](../../company/values.md#using-values-in-decisions):

1. Trust check — Does either option weaken verification, safety, or transparency?
2. Creator check — Which option helps independent food entrepreneurs build durable businesses?
3. Clarity check — Which option reduces uncertainty?
4. Long-term check — Which option still looks correct at 10× scale?

If values still conflict after this sequence, escalate with explicit framing. Do not silently compromise trust.

### Architecture Decisions

Significant engineering decisions require an ADR with: decision, background, reasoning, alternatives, tradeoffs, impact, status, date, related documents.

Prefer boring, readable technology. Document APIs before implementation. Every module independently testable. Every feature observable. See [Engineering Philosophy](../../company/company-philosophy.md#engineering-philosophy).

Modular monolith first — extract services when triggers are met (independent scaling, different SLO, dedicated team, regulatory isolation). Extraction triggers documented in [Architecture Overview](../../engineering/architecture-overview.md#strategic-approach-modular-monolith-first).

### Open Decisions

Business decisions blocked on founder or executive input use the `TODO(decision):` prefix — never vague TODOs. Current open decisions include:

| Decision | Impact |
|----------|--------|
| Pricing model (subscription vs. transaction vs. hybrid) | Onboarding, value prop, feature gating |
| Commission structure | Unit economics, checkout, payouts |
| Geographic launch market | Compliance templates, verification partners, GTM |
| Initial international expansion sequence | Localization and regulatory frameworks |
| Auth provider selection | Identity module implementation |
| Identity verification vendor | Trust module integration |
| Cloud provider and primary region | Infrastructure deployment |

Resolved decisions become ADRs. Do not implement against unresolved `TODO(decision):` items without explicit approval.

### Trust Decision Tree

For trust-impacting changes, apply this sequence before shipping:

```
1. Does this weaken food safety compliance?        → Stop. Do not ship.
2. Does this allow unverified creators to transact? → Stop unless ADR-approved exception.
3. Does this reduce transparency to customers?      → Redesign or do not ship.
4. Does this weaken review integrity?               → Redesign.
5. Otherwise                                        → Proceed with standard review.
```

Trust-impacting changes require Trust & Safety review (Phase 4 ops) and documentation in [Marketplace Mechanics](../../product/marketplace-mechanics.md).

---

## Engineering

### Architecture Summary

Marketplate is a modular monolith with domain modules: Identity, Trust, Catalog, Order, Payment, Discovery, Notification, Admin (Analytics future).

**Trust layer** is cross-cutting — enforced at Catalog + Order gates, not cached without TTL and event invalidation. Fail closed: unknown verification state denies paid transaction.

**Technology:** PostgreSQL, Redis, S3-compatible storage, Stripe + Stripe Connect, containerized runtime, PostgreSQL full-text search initially.

Key architectural principles:

| Principle | Implementation |
|-----------|----------------|
| One service, one responsibility | Each module owns one domain |
| Documented APIs before implementation | OpenAPI specs in `engineering/api/` |
| Fail closed on trust | Deny paid transaction on unknown verification |
| Idempotent side effects | Payment, notification, webhook handlers |
| Events for side effects | Order confirmed → async notification, index update |

Full reference: [Architecture Overview](../../engineering/architecture-overview.md), [Service Catalog](../../engineering/service-catalog.md), [Integration Patterns](../../engineering/integration-patterns.md), [Data Flow](../../engineering/data-flow.md), [Infrastructure Overview](../../engineering/infrastructure-overview.md).

### Service Ownership

| Module | Owns | Trust role |
|--------|------|------------|
| [Identity](../../engineering/services/identity-service.md) | Users, sessions, roles | Authentication for all surfaces |
| [Trust](../../engineering/services/trust-service.md) | Verification, moderation, audit | Core trust state and enforcement |
| [Catalog](../../engineering/services/catalog-service.md) | Storefronts, items, capacity | Verification gates on paid listings |
| [Order](../../engineering/services/order-service.md) | Cart, checkout, lifecycle | Verification check at checkout |
| [Payment](../../engineering/services/payment-service.md) | Charges, refunds, payouts | Immutable financial audit trail |
| [Discovery](../../engineering/services/discovery-service.md) | Search, ranking, collections | Trust-weighted ranking; unverified never ranked with verified |
| [Notification](../../engineering/services/notification-service.md) | Email, future push/in-app | Order and verification updates |

API documentation: [`engineering/api/`](../../engineering/api/).

### Failure Posture

| Failure | Response |
|---------|----------|
| Trust module unavailable | Checkout blocked for all creators — fail closed |
| Payment module unavailable | Graceful checkout error; no duplicate charges |
| Stale verification cache | TTL ≤ 60s with event invalidation; no long-lived trust cache |

Trust-impacting failures require incident documentation per operations philosophy.

### Testing Expectations

Heavy unit and integration testing; targeted E2E on trust and payment paths. Trust-critical tests: verification gate tests, fail-closed scenarios, audit log completeness. AI features tested with golden datasets per system doc in [`ai/`](../../ai/).

---

## Operations

### Operations Philosophy

Every customer interaction should **reduce uncertainty**. Every incident becomes documentation. Every SOP should eventually become partially automated.

Every operational workflow must define:

| Element | Required |
|---------|----------|
| Owner | Named role or team |
| Trigger | What starts the workflow |
| SLA | Measurable time-to-resolution target |
| AI responsibilities | What AI may recommend or automate |
| Human responsibilities | What requires human judgment |
| Escalation rules | When and how to escalate |
| Audit logging | What is recorded and retained |
| Post-mortem | Required for trust-impacting incidents |

Use [SOP template](../../templates/sop-template.md) for all operational procedures. Operations documentation is Phase 4 — [`operations/`](../../operations/) — informed by Phase 3 engineering observability and audit trails.

### Key Operational Workflows (Planned)

| Workflow | Owner domain | Reference |
|----------|--------------|-----------|
| Creator verification | Trust & Safety | [Trust Verification Flow](../../pages/flows/trust-verification-flow.md) |
| Compliance renewal | Trust & Safety | [Marketplace Mechanics — Compliance](../../product/marketplace-mechanics.md#compliance-verification) |
| Order fulfillment | Creator + platform support | [Order Fulfillment Flow](../../pages/flows/order-fulfillment-flow.md) |
| Dispute resolution | Trust & Safety | [Marketplace Mechanics — Disputes](../../product/marketplace-mechanics.md#disputes) |
| Payout issues | Finance + Payment module | [Payment Service](../../engineering/services/payment-service.md) |
| Incident response | Engineering + Operations | [Architecture Overview — Failure Modes](../../engineering/architecture-overview.md#failure-modes) |

### SLAs

Measurable SLAs required for: verification turnaround, payouts, support response, incident resolution. Specific targets will be defined in Platform Settings and operations SOPs (Phase 4). Until published, treat verification delays and payout failures as business emergencies for creators — communicate proactively, never leave creators without status updates.

---

## Customer Support

Support documentation lives in [`support/`](../../support/) (Phase 4). Operating principles apply now:

- **Reduce uncertainty** — Every support interaction should leave the user knowing what happened, what happens next, and when
- **Plain language** — Copy that a first-time cottage food operator can act on without escalation
- **Escalation paths** — Trust, safety, and payment issues route to appropriate owners; support does not improvise policy
- **AI assist, human accountability** — [Support Assist](../../ai/support-assist.md) provides FAQ retrieval and ticket classification; humans handle policy answers and trust-critical responses

Support Assist integration: semantic FAQ search on [Help](../../pages/customer/help.md); ticket classification with macro suggestions; no autonomous customer replies.

---

## Moderation and Trust & Safety

### Trust Enforcement Ladder

Progressive enforcement protects marketplace integrity:

```
Education → Warning → Listing restriction → Order suspension → Account suspension → Permanent removal
```

| Trigger | Typical response |
|---------|------------------|
| Incomplete verification | Cannot go live |
| Expired compliance doc | Auto-suspend listings after grace |
| Allergen mislabeling confirmed | Immediate suspension pending investigation |
| Pattern of unresolved disputes | Account review |
| Fraudulent identity | Permanent removal |

### Moderation

[Moderation Assist](../../ai/moderation-assist.md) scores policy violations on listings, reviews, and messages. Workflow: content/report ingest → AI scoring → [Moderation Queue](../../pages/admin/moderation-queue.md) → human enforcement decision.

**Non-negotiable rules:**

- Verified purchase only for reviews
- No pay-to-remove reviews — ever
- AI recommends; humans approve suspensions and permanent removal
- Default: no auto-suspend on any AI threshold

### Verification

[Verification Assist](../../ai/verification-assist.md) extracts documents and flags fraud/mismatch. Workflow: creator submit → Trust Service ingest → AI async → [Verification Queue](../../pages/admin/verification-queue.md) → human approve/reject.

Three verification layers operate as a system:

1. **Identity** — Government ID, business registration, tax identity
2. **Kitchen** — Production environment documentation and photos
3. **Compliance** — Jurisdiction-appropriate licenses, permits, insurance

Default: **no auto-approve verification**. Full model: [Marketplace Mechanics — Trust Model](../../product/marketplace-mechanics.md#trust-model).

---

## AI Governance

### Platform Principle

**AI recommends. Humans approve.**

AI removes repetitive work for Trust & Safety, support ops, and discovery — without replacing human accountability on verification, moderation, enforcement, or customer-facing policy answers.

### Trust Impact Matrix

| Trust Impact | AI Role | Human Role |
|--------------|---------|------------|
| **High** (verification, moderation, compliance) | Recommend with confidence score | Approve or reject every decision |
| **Medium** (support triage, content suggestions) | Draft or classify; auto-act above threshold with audit | Review samples; handle exceptions |
| **Low** (internal search, doc generation, analytics) | Auto-act with logging | Periodic evaluation |

### Deployment Requirements

Every AI system documents: purpose, inputs, outputs, prompt strategy, evaluation, fallbacks, confidence thresholds, security, human approval, monitoring, continuous improvement.

Evaluation pipeline: label maintenance → offline benchmarks → regression gate → shadow traffic (48h minimum for trust systems) → human sign-off → promote model version → online monitoring + weekly sample audit.

**Fallback always** — every pipeline degrades to manual/keyword/rule paths; never block core flows.

Configuration without code deploy: verification thresholds, moderation severity, discovery weights, queue SLAs — via [Platform Settings](../../pages/admin/platform-settings.md).

Full platform: [AI Platform](../../ai/README.md).

---

## Brand

Brand expresses mission and vision externally. Internal partners should understand brand constraints when making product, support, and communication decisions.

| Document | Governs |
|----------|---------|
| [Brand Strategy](../../brand/brand-strategy.md) | External expression of mission and positioning |
| [Brand Positioning](../../brand/positioning.md) | Competitive differentiation in market |
| [Voice and Tone](../../brand/voice-and-tone.md) | How values sound in external communication |

**Brand-product alignment rules:**

- Lead with trust, not speed — verification and creator identity before discounts or delivery times
- Do not benchmark UX against delivery apps — pickup windows, subscriptions, and catering quotes are core workflows
- Creator segments are not interchangeable in messaging — see [Personas](../../product/personas.md)
- Calm, premium visual identity — large photography, minimal interface; see [Design Principles](../../design-system/principles.md)

We are not Uber Eats. We are not a race-to-the-bottom marketplace. External language must reflect creator infrastructure and verified trust.

---

## Roadmap and Work Organization

### Documentation Phases

Work proceeds in five phases using parallel specialist agents within each domain:

| Phase | Status | Focus |
|-------|--------|-------|
| 1 — Foundation | **Complete** | Company, brand, product |
| 2 — Design & UX | **Complete** | IA, every page spec |
| 3 — Engineering | **Complete** | Architecture, APIs, services, AI |
| 4 — Operations | Not started | SOPs, support, trust & safety, admin |
| 5 — Launch | Not started | Legal, security, analytics, growth, research, QA |

Phase 4 requires engineering docs defining observable systems and audit trails. Phase 5 requires operations and legal foundations. See [Phased Rollout](../../roadmap/phased-rollout.md).

### Product Roadmap Horizons

| Horizon | Focus |
|---------|-------|
| **Foundation** (Years 0–2) | Prove trust model; nail onboarding, verification, ordering |
| **Expansion** (Years 2–5) | Broaden creator types, fulfillment, geography; deepen OS |
| **Infrastructure** (Years 5–10) | Ecosystem integrations, international scale, extensibility |

Vision milestones: [Vision — Strategic Pillars](../../company/vision.md#strategic-pillars-510-year-horizon).

### Sub-Agent Execution Model

Documentation is built in phases using parallel specialist agents. Each agent owns a domain, cross-references existing docs, avoids duplication, and produces implementation-ready Markdown. Agent prompts: [`prompts/phase-agent-prompts.md`](../../prompts/phase-agent-prompts.md).

When contributing documentation:

1. Read governing docs (Constitution, relevant philosophy section)
2. Cross-reference existing canonical sources — link, don't duplicate
3. Use appropriate template
4. Include Related Documents section
5. Update glossary for new terms
6. Flag blocked decisions with `TODO(decision):` only when founder input is required

### Quality Bar

Nothing should resemble placeholder documentation or generic AI output. Every document must read as if written by an experienced principal engineer, product leader, and technical writer working together.

Challenge assumptions. Identify edge cases. Design for the next decade. Remove unnecessary complexity.

---

## Working With Future Decisions

Marketplate maintains explicit open decisions rather than silent assumptions. Partners and senior hires should:

1. **Identify** — Scan product, market, and engineering docs for `TODO(decision):` items before planning work that depends on them
2. **Frame** — Escalate with explicit options, tradeoffs, and recommended default
3. **Record** — Resolved decisions become ADRs in [`decisions/`](../../decisions/); update all dependent docs
4. **Never silently compromise trust** — If a decision cannot be made immediately, choose the trust-preserving default

Current high-impact open decisions:

- Pricing model and commission structure
- Geographic launch market and expansion sequence
- Auth provider, identity verification vendor, cloud provider
- Serviceable addressable market quantification for founding geography

Partners with operational authority should treat unresolved decisions as blockers for implementation — not as invitations to guess.

---

## Onboarding Checklist for Partners

Recommended reading sequence:

1. [Founding Constitution](../../company/constitution.md)
2. [Company Overview](company-overview.md)
3. [Mission](../../company/mission.md) and [Vision](../../company/vision.md)
4. [Values](../../company/values.md) and [Company Philosophy](../../company/company-philosophy.md)
5. [Product Overview](../../product/overview.md) and [Marketplace Mechanics](../../product/marketplace-mechanics.md)
6. [Architecture Overview](../../engineering/architecture-overview.md)
7. [AI Platform](../../ai/README.md)
8. [Phased Rollout](../../roadmap/phased-rollout.md)

Role-specific deep dives:

| Role | Additional reading |
|------|-------------------|
| Product | [Personas](../../product/personas.md), [Value Propositions](../../product/value-props.md), [`pages/`](../../pages/) |
| Engineering | [Service Catalog](../../engineering/service-catalog.md), [`engineering/api/`](../../engineering/api/), [`decisions/`](../../decisions/) |
| Design | [`design-system/`](../../design-system/), [Design Principles](../../design-system/principles.md) |
| Operations / Trust | [Trust Verification Flow](../../pages/flows/trust-verification-flow.md), [`ai/verification-assist.md`](../../ai/verification-assist.md) |
| Growth / Brand | [`brand/`](../../brand/), [Market Context](../../company/market-context.md) |

---

## Related Documents

### Internal

- [Company Overview](company-overview.md)
- [Executive Summary](executive-summary.md)

### Governance

- [Founding Constitution](../../company/constitution.md)
- [Mission](../../company/mission.md)
- [Vision](../../company/vision.md)
- [Values](../../company/values.md)
- [Company Philosophy](../../company/company-philosophy.md)
- [Market Context](../../company/market-context.md)
- [Glossary](../../company/glossary.md)

### Product & Marketplace

- [Product Overview](../../product/overview.md)
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Personas](../../product/personas.md)
- [Success Metrics Overview](../../product/success-metrics-overview.md)

### Engineering & AI

- [Architecture Overview](../../engineering/architecture-overview.md)
- [Service Catalog](../../engineering/service-catalog.md)
- [AI Platform](../../ai/README.md)
- [Verification Assist](../../ai/verification-assist.md)
- [Moderation Assist](../../ai/moderation-assist.md)
- [Support Assist](../../ai/support-assist.md)
- [Discovery Ranking](../../ai/discovery-ranking.md)

### Roadmap & Templates

- [Phased Rollout](../../roadmap/phased-rollout.md)
- [Templates](../../templates/)
- [Decisions (ADRs)](../../decisions/)

### Brand & Design

- [Brand Strategy](../../brand/brand-strategy.md)
- [Brand Positioning](../../brand/positioning.md)
- [Voice and Tone](../../brand/voice-and-tone.md)
- [Design Principles](../../design-system/principles.md)
