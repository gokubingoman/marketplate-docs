# Marketplate Standards

> The master standards manual for Marketplate — brand, food, marketplace, operations, design, engineering, and documentation. **Link, don't duplicate:** this document indexes authoritative sources and defines standards that exist nowhere else.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Company Operations  
**Governing authority:** [Founding Constitution](../../company/constitution.md)

---

## Purpose

This manual is the **single entry point** for anyone — employee, creator, partner, investor, or AI agent — who needs to understand how Marketplate defines quality across the platform.

It answers three questions:

1. **What is required?** — Non-negotiable standards that protect trust, safety, and quality.
2. **Where is it documented?** — Cross-references to domain-specific docs that hold the detail.
3. **What lives here only?** — Standards defined in this repository section that are not duplicated elsewhere (photography, packaging, operational SLAs, refund mediation principles).

Specialized standards extend this manual:

| Document | Scope |
|----------|-------|
| [Chef Quality Standards](chef-quality-standards.md) | Creator-side food production, packaging, fulfillment, and reputation |
| [Trust & Safety Standards](trust-and-safety-standards.md) | Verification, moderation, fraud, incidents, and platform integrity |

**Trust thesis:** Trust is our product. Software enables trust. — [Constitution](../../company/constitution.md#trust-philosophy)

---

## How to Use This Manual

| Audience | Start here | Then read |
|----------|------------|-----------|
| **New employee** | This document → [Company Philosophy](../../company/company-philosophy.md) | Role-specific docs linked in each section |
| **Creator** | [Chef Quality Standards](chef-quality-standards.md) | [Creator Compliance](../../pages/creator/compliance.md) |
| **Engineer** | Engineering section below | [Architecture Overview](../../engineering/architecture-overview.md) |
| **Designer** | Design section below | [Design System](../../design-system/README.md) |
| **Trust & Safety** | [Trust & Safety Standards](trust-and-safety-standards.md) | [Marketplace Mechanics — Trust Model](../../product/marketplace-mechanics.md#trust-model) |
| **Support / Ops** | Customer communication + Support sections | [Help page spec](../../pages/customer/help.md) |

When a standard conflicts with a feature spec, **the more restrictive trust or safety requirement wins** unless an ADR explicitly documents an exception in [`decisions/`](../../decisions/).

---

## Brand Standards

Marketplate brand expression must be **trustworthy, warm, precise, calm, premium, and human** across every touchpoint.

### Authoritative references

| Topic | Document |
|-------|----------|
| Brand purpose, personality, differentiation | [Brand Strategy](../../brand/brand-strategy.md) |
| Positioning and competitive frame | [Positioning](../../brand/positioning.md) |
| Voice attributes and tone by context | [Voice and Tone](../../brand/voice-and-tone.md) |
| Product, feature, and UI naming | [Naming Conventions](../../brand/naming-conventions.md) |

### Platform-wide brand rules

| Rule | Requirement |
|------|-------------|
| **Verification language** | Use credential-based labels only: "Verified Identity," "Verified Kitchen," "Food safety documentation on file." Never imply guarantees Marketplate cannot substantiate. |
| **Creator prominence** | Lead with the creator's name and story — not "Marketplate user" or anonymous seller framing. |
| **No dark patterns** | No hidden fees, artificial urgency, or pay-to-hide-negative-review mechanics. |
| **Consistent terminology** | Use [Glossary](../../company/glossary.md) terms in product, docs, and support. Creator (not vendor), customer (not user), storefront (not shop). |
| **Human voice** | AI assists behind the scenes; customer-facing copy is human-reviewed. |

### Brand compliance checklist

Before publishing customer-facing material:

- [ ] Follows [Voice Checklist](../../brand/voice-and-tone.md#voice-checklist)
- [ ] Uses [Naming Conventions](../../brand/naming-conventions.md) for features and verification labels
- [ ] Trust claims are verifiable and match current product capability
- [ ] Photography is authentic — see Photography Standards below

---

## Food Standards

Food standards protect customers and creators. They apply to **every item sold on Marketplate**, regardless of fulfillment model or creator persona.

### Authoritative references

| Topic | Document |
|-------|----------|
| Creator production requirements | [Chef Quality Standards](chef-quality-standards.md) |
| Allergen disclosure and checkout acknowledgment | [Marketplace Mechanics — Transparency](../../product/marketplace-mechanics.md#transparency) |
| Jurisdiction and category restrictions | [Marketplace Mechanics — Compliance verification](../../product/marketplace-mechanics.md#compliance-verification) |
| Creator compliance UI | [Creator Compliance](../../pages/creator/compliance.md) |

### Platform food invariants

| Invariant | Standard |
|-----------|----------|
| **Verified to sell** | Unverified creators cannot accept paid orders |
| **Accurate labeling** | Ingredients, allergens, and dietary tags must reflect actual preparation |
| **Category eligibility** | Prohibited items per jurisdiction cannot be listed — platform enforces, not honor system |
| **Production location linkage** | Every SKU associated with a verified kitchen |
| **No silent substitution** | Material ingredient changes require listing update before sale |

Food safety incidents follow [Trust & Safety Standards — Incident Response](trust-and-safety-standards.md#incident-response). Confirmed allergen mislabeling triggers immediate suspension pending investigation — [Enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder).

---

## Marketplace Standards

Marketplace standards define how supply and demand interact on Marketplate.

### Authoritative references

| Topic | Document |
|-------|----------|
| Trust model, transactions, fulfillment | [Marketplace Mechanics](../../product/marketplace-mechanics.md) |
| Discovery and ranking principles | [Marketplace Mechanics — Discovery](../../product/marketplace-mechanics.md#discovery) |
| Creator and customer funnels | [Success Metrics Overview](../../product/success-metrics-overview.md) |
| Trust enforcement | [Trust & Safety Standards](trust-and-safety-standards.md) |

### Marketplace invariants

| Invariant | Rule |
|-----------|------|
| **Verified to sell** | Paid checkout blocked until identity, kitchen, and compliance verified |
| **Transparent to buy** | Trust-relevant information visible before payment |
| **Creator-owned relationship** | Creator is merchant of record; platform facilitates |
| **Audit everything** | Trust, payment, and moderation actions leave immutable audit trails |
| **Human approval on high stakes** | AI recommends; humans approve verification, suspensions, policy exceptions |
| **No overselling** | Capacity enforced at checkout — overselling is a platform defect |

### Ranking and merchandising

Discovery optimizes for **fit and confidence**, not engagement maximization. Prohibited ranking factors include payment for obscured promotion and boosting creators with expired compliance. Full rules: [Ranking principles](../../product/marketplace-mechanics.md#ranking-principles).

### Anti-patterns (explicitly rejected)

Open marketplace without verification, pay-to-hide reviews, promoted listings without verification badge, bidding wars for ranking, platform as anonymous middleman, overselling capacity — [Anti-Patterns](../../product/marketplace-mechanics.md#anti-patterns-explicitly-rejected).

---

## Photography Standards

Photography is a **trust surface**. Customers judge food quality and creator authenticity from images before they read a description.

These standards apply to creator-uploaded menu photography, storefront banners, and profile images. Marketing photography follows [Brand Strategy](../../brand/brand-strategy.md) with the same authenticity principles.

### Required qualities

| Criterion | Standard |
|-----------|----------|
| **Authenticity** | Photograph the actual food you sell. Same recipe, portion, and presentation customers receive. |
| **Accuracy** | Image represents the listed item — not a different dish, stock photo, or competitor's work. |
| **Recency** | Replace images when recipe, portion, or presentation changes materially. |
| **Legibility** | In focus, adequately lit, not over-filtered. Customer can identify the food. |
| **Clean context** | Background and surfaces appropriate for food — no visible clutter, dirty equipment, or unrelated branded packaging (unless ingredient brand is disclosed). |

### Prohibited content

| Prohibited | Reason |
|------------|--------|
| Stock photography or AI-generated food images | Misrepresents actual product |
| Images stolen from other creators or restaurants | Fraud; copyright violation |
| Misleading garnishes or props not included in order | False advertising |
| Before/after health or weight-loss imagery | Off-brand; regulatory risk |
| Images containing unverified health claims | Trust and legal risk |
| NSFW, violent, or unrelated imagery | Policy violation |

### Technical requirements

| Property | Minimum |
|----------|---------|
| **Resolution** | 1200px on shortest side for hero/menu images |
| **Aspect ratio** | 4:3 or 1:1 recommended; consistent within a menu where possible |
| **Format** | JPEG, PNG, or WebP |
| **File size** | ≤ 10 MB per image at upload |
| **Alt text** | Creator-provided description encouraged; platform generates fallback — [Accessibility Standards](../../design-system/accessibility-standards.md#image--media) |

### Discovery eligibility

Photography quality affects discovery over time. Creators with consistently low-quality, misleading, or flagged images may lose featured placement eligibility. Moderation pipeline: [Moderation Assist](../../ai/moderation-assist.md).

### Kitchen and verification photos

Kitchen verification photos follow [Trust & Safety Standards — Kitchen Verification](trust-and-safety-standards.md#kitchen-verification). These are operational artifacts — not marketing assets — and must accurately depict the production environment.

---

## Packaging Standards

Packaging protects food safety, communicates professionalism, and carries legally required information.

Detailed creator obligations: [Chef Quality Standards — Packaging](chef-quality-standards.md#packaging).

### Platform packaging principles

| Principle | Requirement |
|-----------|-------------|
| **Food-safe materials** | Containers, wraps, and labels appropriate for food type and hold time |
| **Temperature integrity** | Hot food stays hot; cold food stays cold through stated pickup/delivery window |
| **Tamper evidence** | Sealed containers or tamper-evident closures for delivery and pickup handoff |
| **Label completeness** | Every package includes item identification and allergen summary where required by jurisdiction |
| **Creator branding** | Optional creator branding encouraged; Marketplate branding not required on physical packaging |
| **Sustainability** | Prefer recyclable or compostable materials where food-safe; no platform mandate at v1 |

### Fulfillment-model specifics

| Model | Additional requirement |
|-------|------------------------|
| **Pickup — scheduled** | Order ID or customer name visible on exterior; pickup instructions in app |
| **Pickup — same day** | Time-sensitive labeling for perishable items |
| **Delivery — creator managed** | Secure transport; spill/leak prevention; temperature bags for hot/cold items |
| **Catering / event** | Service documentation, setup notes, and labeled trays for buffet/service styles |
| **Shipping — non-perishable** | Only where legally permitted; crush-proof packaging; ingredient/allergen label on exterior |

---

## Customer Communication Standards

Every customer interaction must **reduce uncertainty** — per [Operations Philosophy](../../company/constitution.md#operations-philosophy).

### Authoritative references

| Topic | Document |
|-------|----------|
| Voice and tone by context | [Voice and Tone](../../brand/voice-and-tone.md) |
| Help center content and support form | [Help page spec](../../pages/customer/help.md) |
| Creator messaging | [Creator Messages](../../pages/creator/messages.md) |
| Error message patterns | [Voice and Tone — Error Messages](../../brand/voice-and-tone.md#error-messages) |

### Communication rules

| Channel | Standard |
|---------|----------|
| **Transactional email / push** | Confirm facts: what, when, where, how much. No marketing filler in order confirmations. |
| **Order status updates** | Material delays communicated proactively by creator; chronic lateness affects [Trust Score](trust-and-safety-standards.md#trust-score). |
| **Support responses** | Empathetic, accountable, resolution-focused. Specific timelines — not "soon." Target: first response within 24 hours; urgent food-safety issues within 4 hours. |
| **Policy explanations** | Neutral, clear, linked to authoritative policy. No blame shifting between platform and creator. |
| **Allergen communication** | Creators respond to allergen questions within stated SLA; severe allergy inquiries routed to priority queue. |

### Prohibited communication

- Misleading verification or safety claims
- Off-platform payment solicitation (fraud risk)
- Harassment, discrimination, or retaliation against reviewers
- Sharing customer PII beyond order fulfillment need
- Automated customer replies without human review for policy or safety topics

---

## Refunds and Disputes Standards

Refunds protect customers while preserving creator accountability. Policies must be **displayed pre-checkout** and versioned in [`legal/`](../../legal/).

### Authoritative references

| Topic | Document |
|-------|----------|
| Cancellation and refund principles | [Marketplace Mechanics — Cancellations and refunds](../../product/marketplace-mechanics.md#cancellations-and-refunds) |
| Dispute stages | [Marketplace Mechanics — Disputes](../../product/marketplace-mechanics.md#disputes) |
| Customer help content | [Help — Cancellations FAQ](../../pages/customer/help.md#key-faq-content-v1) |
| Dispute tooling | [Dispute Detail](../../pages/admin/dispute-detail.md) |

### Default refund principles

| Scenario | Standard |
|----------|----------|
| **Creator-initiated cancel** | Full refund; impacts creator reliability metrics |
| **Customer cancel within policy window** | Per creator/platform policy disclosed at checkout |
| **Custom order / catering deposit** | Deposit forfeiture rules disclosed pre-payment |
| **Platform force-cancel** | Safety or compliance issue; full refund; creator investigation |
| **Quality dispute — creator at fault** | Full or partial refund per mediation outcome |
| **Quality dispute — inconclusive** | Case-by-case mediation; documented rationale |

### Refund processing

| Element | Standard |
|---------|----------|
| **Timeline** | Refunds process in 5–10 business days to original payment method — communicated in [Help](../../pages/customer/help.md) |
| **Partial refunds** | Allowed when proportional to issue; logged in dispute record |
| **Platform mediation** | Trust & Safety mediates when creator and customer disagree — [Trust & Safety Standards — Disputes](trust-and-safety-standards.md#dispute-resolution) |
| **No pay-to-remove reviews** | Refunds never conditioned on review removal |

---

## Support Standards

Support is a trust function, not a cost center.

### Service levels

| Priority | Examples | First response SLA | Resolution target |
|----------|----------|-------------------|-------------------|
| **P0 — Safety** | Allergic reaction report, foodborne illness, tampering | 1 hour | Same business day escalation |
| **P1 — Order critical** | Wrong order, missed pickup window, payment failure post-charge | 4 hours | 24 hours |
| **P2 — Standard** | Policy questions, refund status, account issues | 24 hours | 3 business days |
| **P3 — General** | Feature questions, feedback | 48 hours | Best effort |

Food-safety categories route to priority queue automatically — [Help — Contact support](../../pages/customer/help.md#contact-support).

### Support quality standards

| Standard | Requirement |
|----------|-------------|
| **Context preservation** | Order-attached tickets include verified order ID and status |
| **Macro alignment** | Support macros use exact UI terminology from [Naming Conventions](../../brand/naming-conventions.md) |
| **Escalation path** | Unresolved issues escalate to Trust & Safety with audit trail |
| **AI assist role** | [Support Assist](../../ai/support-assist.md) classifies and suggests macros — humans send customer-facing replies |
| **Deflection measurement** | FAQ effectiveness tracked via [Help analytics](../../pages/customer/help.md#analytics) |

Every support incident that reveals a systemic gap becomes documentation — [Operations Philosophy](../../company/constitution.md#operations-philosophy).

---

## AI Standards

AI removes repetitive work; **humans remain accountable** for verification, enforcement, and customer-facing policy answers.

### Authoritative references

| Topic | Document |
|-------|----------|
| AI philosophy and doc requirements | [Constitution — AI Philosophy](../../company/constitution.md#ai-philosophy) |
| AI platform overview | [AI Platform README](../../ai/README.md) |
| Verification assist | [Verification Assist](../../ai/verification-assist.md) |
| Moderation assist | [Moderation Assist](../../ai/moderation-assist.md) |
| Support assist | [Support Assist](../../ai/support-assist.md) |
| Discovery ranking | [Discovery Ranking](../../ai/discovery-ranking.md) |
| AI doc template | [AI Doc Template](../../templates/ai-doc-template.md) |

### Non-negotiable AI rules

| Rule | Implementation |
|------|----------------|
| **AI recommends; humans approve** | No auto-approve verification; no auto-suspend; no autonomous customer policy replies |
| **Document before deploy** | Every AI system documented in `ai/` with eval, thresholds, fallbacks |
| **Fallback always** | AI failure never blocks creator submit or customer purchase |
| **No training on customer data** | Without explicit consent and legal review |
| **Version everything** | `model_version` on every AI output |
| **Explainability** | Moderation and ranking cite evidence; operators can dismiss AI flags with audit note |

Trust-critical thresholds configurable in [Platform Settings](../../pages/admin/platform-settings.md) — defaults prohibit autonomous enforcement.

---

## Accessibility Standards

Accessibility is a **trust requirement** — especially for allergen disclosure and checkout flows.

### Authoritative references

| Topic | Document |
|-------|----------|
| WCAG 2.2 AA targets and patterns | [Accessibility Standards](../../design-system/accessibility-standards.md) |
| Design principle | [Design System — Accessibility first](../../design-system/principles.md#6-accessibility-first) |
| Page-level requirements | [Page Doc Template — Accessibility](../../templates/page-doc-template.md) |

### Platform accessibility invariants

| Requirement | Standard |
|-------------|----------|
| **Compliance target** | WCAG 2.2 Level AA on all customer- and creator-facing UI |
| **Allergen disclosure** | Visible, not hover-only; programmatically associated; checkout acknowledgment not pre-checked |
| **Keyboard access** | All functionality available via keyboard |
| **Touch targets** | Minimum 44×44 CSS pixels |
| **Motion** | Respect `prefers-reduced-motion` |
| **Testing** | axe-core in CI; manual VoiceOver/NVDA smoke test each release |

---

## Design Standards

Interfaces must feel **calm, premium, and trust-building**.

### Authoritative references

| Topic | Document |
|-------|----------|
| Design principles | [Design System Principles](../../design-system/principles.md) |
| Color, typography, spacing | [Design System Foundations](../../design-system/README.md#foundations) |
| Components | [Components Overview](../../design-system/components-overview.md) |
| Trust signal treatment | [Trust in Design](../../design-system/principles.md#trust-in-design) |

### Design invariants

| Rule | Standard |
|------|----------|
| **One primary action per screen** | Single obvious next step |
| **Whitespace** | Generous spacing; content and photography lead |
| **Design tokens** | No hardcoded colors or spacing — use semantic tokens |
| **Responsive parity** | Critical information never hidden on mobile |
| **Trust signals** | Verification badges consistent everywhere; full price breakdown before payment |
| **No dark patterns** | See Brand Standards |

Decision framework: [Design System — Decision Framework](../../design-system/principles.md#decision-framework).

---

## Engineering Standards

Engineering implements trust as **fail-closed gates**, observable systems, and documented APIs.

### Authoritative references

| Topic | Document |
|-------|----------|
| System architecture | [Architecture Overview](../../engineering/architecture-overview.md) |
| Service boundaries | [Service Catalog](../../engineering/service-catalog.md) |
| API specifications | [API Overview](../../engineering/api/api-overview.md) |
| Integration patterns | [Integration Patterns](../../engineering/integration-patterns.md) |
| Infrastructure | [Infrastructure Overview](../../engineering/infrastructure-overview.md) |
| Engineering doc template | [Engineering Doc Template](../../templates/engineering-doc-template.md) |

### Engineering invariants

| Principle | Standard |
|-----------|----------|
| **Documentation precedes implementation** | OpenAPI specs before code |
| **One module, one responsibility** | Strict domain boundaries — [Architecture Overview](../../engineering/architecture-overview.md) |
| **Fail closed on trust** | Unknown verification state → deny paid transaction |
| **Audit everything** | Immutable audit log for trust, payment, admin actions |
| **Observable by default** | Structured JSON logs; golden signals per module |
| **Idempotent side effects** | Payment, notification, webhook handlers use idempotency keys |
| **Trust-critical testing** | Verification gates, fail-closed scenarios, audit completeness in CI |

Technology choices favor **boring, operable technology** — [Engineering Philosophy](../../company/company-philosophy.md#engineering-philosophy).

---

## Documentation Standards

Documentation is **production code**. Incomplete documentation means the feature is incomplete.

### Authoritative references

| Topic | Document |
|-------|----------|
| Documentation philosophy | [Constitution — Documentation Philosophy](../../company/constitution.md#documentation-philosophy) |
| Document types and templates | [Constitution — Document Standards](../../company/constitution.md#document-standards) |
| Quality bar | [Constitution — Quality Bar](../../company/constitution.md#quality-bar) |
| Templates | [`templates/`](../../templates/) |
| Glossary | [Glossary](../../company/glossary.md) |

### Documentation invariants

| Principle | Requirement |
|-----------|-------------|
| **Spec before code** | Feature, page, API, and AI docs precede implementation |
| **Traceability** | Engineering decisions link back to product and trust docs |
| **Dual audience** | Understandable by humans and AI agents |
| **Link, don't duplicate** | Cross-reference authoritative sources |
| **Evergreen writing** | Written for years of consumption |
| **Related systems** | Every page references connected systems |
| **Decision tracking** | `TODO(decision):` only for explicit business decisions requiring founder input |

Repository structure: [Constitution — Required Repository Structure](../../company/constitution.md#required-repository-structure).

---

## Operational Standards

Operations turn policy into reliable execution.

### Core principles

From [Operations Philosophy](../../company/constitution.md#operations-philosophy):

- Every customer interaction reduces uncertainty
- Every incident becomes documentation
- Every SOP should eventually become partially automated
- AI assists; humans remain accountable
- Measurable SLAs on every workflow
- Complete audit trails

### Standard operational SLAs

| Workflow | Owner | SLA | Reference |
|----------|-------|-----|-----------|
| Identity verification review | Trust & Safety | 2 business days | [Verification Queue](../../pages/admin/verification-queue.md) |
| Kitchen verification review | Trust & Safety | 3 business days | [Trust Verification Flow](../../pages/flows/trust-verification-flow.md) |
| Compliance document review | Trust & Safety | 2 business days | [Creator Compliance](../../pages/creator/compliance.md) |
| Moderation — high severity | Trust & Safety | 4 hours | [Moderation Assist](../../ai/moderation-assist.md#confidence-thresholds) |
| Moderation — standard | Trust & Safety | 24 hours | [Moderation Queue](../../pages/admin/moderation-queue.md) |
| Dispute mediation | Trust & Safety | 3 business days | [Trust & Safety Standards](trust-and-safety-standards.md#dispute-resolution) |
| Customer support — P0 | Support | 1 hour first response | Support Standards above |
| Customer support — standard | Support | 24 hours first response | [Help](../../pages/customer/help.md) |
| Payout processing | Finance / Payment | Per creator dashboard schedule | [Payment Service](../../engineering/services/payment-service.md) |
| Compliance expiry grace | Platform | Configurable; default 14 days | [Trust Service](../../engineering/services/trust-service.md) |

Detailed SOPs: [`operations/`](../../operations/) *(Phase 4)*.

### Incident and post-mortem standards

| Requirement | Standard |
|-------------|-------------|
| **Trust incidents** | P0 escalation; same-day executive notification for food-safety events |
| **Post-mortem** | Required for all P0/P1 trust incidents within 5 business days |
| **Documentation update** | Post-mortem must link to updated docs or ADR if process changed |
| **Audit retention** | Trust and payment audit events: immutable retention per [Integration Patterns](../../engineering/integration-patterns.md) |

### Enforcement ladder

Progressive enforcement: Education → Warning → Listing restriction → Order suspension → Account suspension → Permanent removal — [Marketplace Mechanics](../../product/marketplace-mechanics.md#trust-enforcement-ladder). Detailed application: [Trust & Safety Standards — Enforcement](trust-and-safety-standards.md#enforcement-ladder).

---

## Standards Governance

### Ownership and review

| Document | Owner | Review cadence |
|----------|-------|----------------|
| This manual | Company Operations | Quarterly |
| Chef Quality Standards | Creator Success + Trust & Safety | Quarterly |
| Trust & Safety Standards | Trust & Safety | Monthly |
| Domain docs (brand, design, engineering) | Domain owners | Per domain schedule |

### Change process

1. Propose change with rationale and trust impact assessment
2. Cross-functional review if customer- or creator-facing
3. Update authoritative doc; update this index if scope changes
4. ADR for significant policy or architecture shifts
5. Communicate to affected teams; update Help/Compliance surfaces if customer-visible

### Metrics

Standards effectiveness measured via [Success Metrics — Trust](../../product/success-metrics-overview.md#trust-metrics). If Verified GMV grows while trust metrics degrade, treat as a crisis — not success.

---

## Related Documents

### Standards suite

- [Chef Quality Standards](chef-quality-standards.md)
- [Trust & Safety Standards](trust-and-safety-standards.md)
- [Standards README](README.md)

### Governance

- [Founding Constitution](../../company/constitution.md)
- [Company Philosophy](../../company/company-philosophy.md)
- [Values](../../company/values.md)
- [Glossary](../../company/glossary.md)

### Product and marketplace

- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Product Overview](../../product/overview.md)
- [Success Metrics Overview](../../product/success-metrics-overview.md)

### Design, brand, engineering, AI

- [Brand](../../brand/README.md)
- [Design System](../../design-system/README.md)
- [Engineering](../../engineering/README.md)
- [AI Platform](../../ai/README.md)
