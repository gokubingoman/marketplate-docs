# Legal & Compliance

> Framework-level legal documentation for Marketplate — terms, privacy, creator agreements, food commerce compliance, and refund policy. **Requires review and approval by qualified legal counsel before publication or use in production.**

**Status:** Draft — Framework  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Legal *(Phase 5)*

---

## ⚠️ Attorney Review Required

These documents are **internal framework drafts** prepared for documentation completeness and cross-functional alignment. They are **not** published legal terms and **must not** be presented to customers, creators, or regulators without review, customization, and approval by qualified legal counsel licensed in each applicable jurisdiction.

Before publication:

1. **Engage legal counsel** for the launch market and any expansion jurisdictions.
2. **Resolve all `TODO(decision):` items** — especially geographic launch market, commission structure, and jurisdiction-specific clauses.
3. **Align with payment processor agreements**, insurance requirements, and tax obligations.
4. **Version and publish** with effective dates; wire checkout acknowledgment to published versions.
5. **Establish legal contact** for subpoenas, regulatory inquiries, and consumer rights requests.

---

## Purpose

This folder contains Marketplate's legal and compliance framework — the authoritative source for terms, privacy, seller agreements, food commerce rules, and refund policy that product, engineering, operations, and support must implement consistently.

Governing thesis: **Trust is our product. Software enables trust.** — [Founding Constitution](../company/constitution.md#trust-philosophy)

Strategic marketplace model: [Marketplace Mechanics](../product/marketplace-mechanics.md)

---

## Document Index

| Document | Audience | Summary |
|----------|----------|---------|
| [Terms of Service](terms-of-service.md) | Customers, creators, visitors | Platform rules, marketplace role, user obligations, disputes, limitations |
| [Privacy Policy](privacy-policy.md) | All users | Data collection, purposes, retention, rights, PII, AI processing |
| [Creator Agreement](creator-agreement.md) | Creators (sellers) | Seller obligations, verification, food safety, fees, payouts, termination |
| [Food Commerce Compliance](food-commerce-compliance.md) | Creators, compliance, legal | Cottage food, commercial kitchen, jurisdictional framework |
| [Refund & Cancellation Policy](refund-and-cancellation-policy.md) | Customers, creators | Cancellation windows, refund rules, dispute framing, platform force-cancel |

---

## Policy Hierarchy

When documents conflict, resolve in this order (most specific wins within tier):

1. **Checkout-acknowledged policy version** — the version customer accepted at payment for that transaction
2. **Creator Agreement** — seller-specific obligations beyond platform minimums
3. **Refund & Cancellation Policy** — financial outcomes and dispute framing
4. **Terms of Service** — general platform rules
5. **Help Center summaries** — plain-language guides; legal text governs when they differ

Help Center: [Platform Policies](../docs/help-center/platform-policies.md) · [Refunds](../docs/help-center/refunds.md) · [Privacy](../docs/help-center/privacy.md)

---

## Cross-Domain Map

| Legal topic | Product | Operations | Help Center |
|-------------|---------|------------|-------------|
| Marketplace role / MoR | [Marketplace Mechanics — Transactions](../product/marketplace-mechanics.md#transactions) | — | [Platform Policies](../docs/help-center/platform-policies.md) |
| Verification | [Trust Model](../product/marketplace-mechanics.md#trust-model) | [Verification Review SOP](../operations/verification-review-sop.md) | [Verification](../docs/help-center/verification.md) |
| Food safety | [Compliance verification](../product/marketplace-mechanics.md#compliance-verification) | [Food Safety Incident SOP](../operations/food-safety-incident-sop.md) | [Food Safety](../docs/help-center/food-safety.md) |
| Disputes & refunds | [Disputes](../product/marketplace-mechanics.md#disputes) | [Dispute Resolution SOP](../operations/dispute-resolution-sop.md) · [Refund Processing SOP](../operations/refund-processing-sop.md) | [Refunds](../docs/help-center/refunds.md) |
| Trust enforcement | [Enforcement ladder](../product/marketplace-mechanics.md#trust-enforcement-ladder) | [Moderation SOP](../operations/moderation-sop.md) · [Creator Suspension SOP](../operations/creator-suspension-sop.md) | [Trust](../docs/help-center/trust.md) |
| AI processing | [AI Philosophy](../company/constitution.md#ai-philosophy) | — | [Privacy](../docs/help-center/privacy.md) |
| Standards | — | [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md) | [Community Guidelines](../docs/help-center/community-guidelines.md) |

---

## Versioning & Publication

| Requirement | Implementation |
|-------------|----------------|
| **Version IDs** | Semantic versioning (e.g., `1.0.0`) with effective date |
| **Checkout capture** | Store policy version IDs acknowledged at payment — [Marketplace Mechanics — Transparency](../product/marketplace-mechanics.md#transparency) |
| **Material changes** | Email notification before effective date; re-acknowledgment where required |
| **Archive** | Retain superseded versions for dispute resolution — policy version lock per [Dispute Resolution SOP](../operations/dispute-resolution-sop.md) |
| **Localization** | `TODO(decision):` Translation and jurisdiction-specific annexes per launch market |

---

## Open Decisions

| Decision | Impact | Documents affected |
|----------|--------|-------------------|
| `TODO(decision):` Geographic launch market | Governing law, cottage food rules, tax, consumer rights | All |
| `TODO(decision):` Commission structure | Fee disclosure, Creator Agreement, ToS | ToS, Creator Agreement |
| `TODO(decision):` Insurance minimum coverage | Compliance requirements | Creator Agreement, Food Commerce |
| `TODO(decision):` Entity legal name and registered address | Publication headers, regulatory contact | All |
| `TODO(decision):` Arbitration vs. court jurisdiction | Dispute resolution clauses | ToS, Creator Agreement |

---

## Related Documents

- [Founding Constitution](../company/constitution.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
- [Marketplate Standards — Refunds](../docs/standards/marketplate-standards.md#refunds-and-disputes-standards)
- [Operations](../operations/)
- [Help Center](../docs/help-center/)
- [Phased Rollout — Phase 5](../roadmap/phased-rollout.md)
