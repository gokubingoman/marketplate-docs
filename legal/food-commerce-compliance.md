# Food Commerce Compliance

> **DRAFT — FRAMEWORK ONLY.** Requires review and approval by qualified legal counsel before publication. Food commerce law varies significantly by jurisdiction — this document provides a platform framework, not legal advice.

**Status:** Draft — Framework  
**Version:** 1.0.0  
**Effective date:** `TODO(decision):` Set upon legal approval  
**Last updated:** 2026-07-03  
**Owner:** Legal · Trust & Safety

**Plain-language summary:** [Help — Food Safety](../docs/help-center/food-safety.md) · [Help — Verification](../docs/help-center/verification.md)

---

## 1. Purpose

This document defines Marketplate's **framework for food commerce compliance** — how creators must operate legally, how the Platform verifies and enforces eligibility, and how jurisdictional rules apply.

Marketplate is a marketplace facilitator. **Creators are solely responsible** for compliance with all applicable food laws. Marketplate verifies documentation and enforces platform standards but does not replace government licensing, inspection, or enforcement.

Governing thesis: [Founding Constitution — Trust Philosophy](../company/constitution.md#trust-philosophy)

Strategic model: [Marketplace Mechanics — Compliance verification](../product/marketplace-mechanics.md#compliance-verification)

---

## 2. Regulatory Framework

### 2.1 Layered responsibility

| Layer | Responsible party | Marketplate role |
|-------|-------------------|------------------|
| **Licensing & permits** | Creator + government authority | Verify documents; block ineligible categories |
| **Food safety practice** | Creator | Standards enforcement via quality metrics and incidents |
| **Labeling & allergens** | Creator | Mandatory fields; suspension on confirmed mislabeling |
| **Inspection & enforcement** | Government health authorities | Cooperate with valid requests; incident reporting |
| **Consumer protection** | Creator (seller) + Platform policies | Dispute mediation; refund policy |

### 2.2 Platform verification vs. government authority

| Marketplate verifies | Marketplate does not |
|----------------------|----------------------|
| Document authenticity and consistency | Conduct health inspections |
| Entity identity matches submitted docs | Certify allergen-free kitchens |
| Kitchen type matches product categories | Approve recipes or formulations |
| Compliance docs are current (within grace rules) | Replace creator's legal obligations |
| Product categories eligible per jurisdiction template | Guarantee regulatory compliance |

**Kitchen verification is not a health inspection substitute.** This limitation must appear in customer-facing and creator-facing materials.

[Trust & Safety Standards — Kitchen Verification](../docs/standards/trust-and-safety-standards.md#kitchen-verification)

### 2.3 Geographic scope

`TODO(decision):` **Launch market** determines:

- Initial jurisdiction rule set and compliance template library
- Cottage food law applicability
- Required document types and category restrictions
- Sales caps and direct-to-consumer limits
- Whether Marketplate collects/remits sales tax
- Health authority notification requirements for incidents

Until launch market is decided, all jurisdiction-specific sections below are **framework placeholders** requiring counsel-approved annexes.

---

## 3. Kitchen Types & Requirements

Marketplate supports multiple production environments. Each type has distinct verification and compliance requirements.

### 3.1 Kitchen type matrix

| Kitchen type | Description | Verification focus | Typical compliance docs |
|--------------|-------------|--------------------|-------------------------|
| **Home (cottage food)** | Residential kitchen producing under cottage food law | Address confirmation, jurisdiction eligibility, facility photos | Cottage food registration/permit, food handler cert |
| **Commercial shared kitchen** | Licensed facility with multiple tenants | Facility registration, tenant bay/schedule linkage | Business license, facility agreement, food handler cert |
| **Dedicated commercial facility** | Creator-operated licensed kitchen | Business address, facility photos, inspection records | Business license, health permit, food handler cert |
| **Commissary** | Central prep facility for mobile operators | Commissary registration, linked units | Commissary permit, unit roster |
| **Mobile (food truck / trailer)** | Mobile unit with commissary requirement | Unit ID, commissary linkage, route/schedule | Mobile vending permit, commissary agreement |

Product linkage: Every SKU must associate with a **verified production location**. [Marketplace Mechanics — Kitchen verification](../product/marketplace-mechanics.md#kitchen-verification)

### 3.2 Multi-tenant commercial kitchens

- Facility verified once at facility level
- Tenants linked to permitted bays, schedules, or agreements
- Tenancy changes require updated linkage before sale from new bay
- Creator must not produce outside assigned space

Operations: [Verification Review SOP](../operations/verification-review-sop.md)

### 3.3 Mobile operators

Food trucks and mobile units must:

- Link to a verified commissary for prep, storage, and servicing
- Provide unit identification (license plate, health decal, etc.)
- Comply with mobile vending permits for operating jurisdictions
- Update location/schedule for pop-up and "open now" fulfillment models

---

## 4. Cottage Food Operations

Cottage food laws allow limited home-based production without full commercial kitchen licensing in many jurisdictions — with significant restrictions.

### 4.1 General cottage food principles (framework)

| Principle | Platform requirement |
|-----------|---------------------|
| **Registration** | Valid cottage food registration/permit for jurisdiction |
| **Eligible products** | Only categories permitted under applicable cottage food law |
| **Sales caps** | Creator must not exceed jurisdictional annual sales limits — `TODO(decision):` Platform tracking mechanism |
| **Prohibited items** | Typically includes certain refrigerated, low-acid canned, meat, and seafood items — varies by state |
| **Labeling** | Cottage food label requirements per jurisdiction (producer name, address, disclaimer) |
| **Direct sales** | Many jurisdictions restrict cottage food to direct-to-consumer — delivery/shipping rules vary |
| **Interstate sales** | Generally prohibited or heavily restricted — Platform may block cross-state cottage sales |

### 4.2 Category enforcement

The Platform compliance engine **blocks ineligible categories** at listing time based on jurisdiction template — not honor system.

Examples of commonly restricted cottage categories (jurisdiction-dependent):

- Raw or heat-treated animal products
- Certain dairy products
- Low-acid canned foods
- Cut leafy greens
- Garlic-in-oil preparations
- `TODO(decision):` Launch market cottage food category allowlist/blocklist`

[Marketplace Mechanics — Category restrictions](../product/marketplace-mechanics.md#compliance-verification)

### 4.3 Cottage food disclosures

Creators operating under cottage food laws must:

- Display appropriate consumer disclaimers where required
- Not represent products as produced in a commercial inspected facility unless true
- Accurately declare production location type to customers

Customer education: [Help — Food Safety](../docs/help-center/food-safety.md)

---

## 5. Commercial Kitchen Operations

Creators using commercial kitchen facilities must:

| Requirement | Detail |
|-------------|--------|
| **Business license** | Valid for operating jurisdiction |
| **Health permit** | Facility or operator permit as required |
| **Food handler certification** | Valid cert matching verified identity or registered staff |
| **Facility agreement** | Documented access to shared kitchen (if applicable) |
| **Insurance** | General/product liability when required by platform policy or law |
| **Inspection records** | Provided where available from local authority |

Commercial operators may access broader product categories subject to permits held.

---

## 6. Compliance Document Management

### 6.1 Required document types

| Document | Applicability |
|----------|---------------|
| Food handler certificate | Most creators — named individual must match identity |
| Business license | Commercial operators |
| Cottage food registration/permit | Home-based cottage operators |
| Health department permit | Commercial facilities |
| Mobile vending permit | Food trucks |
| Liability insurance | Where mandated by platform or law |
| Sales tax registration | Where applicable |
| Specialty permits | Catering, alcohol (`TODO(decision):` if ever supported) |

Full matrix: [Trust & Safety Standards — Compliance Verification](../docs/standards/trust-and-safety-standards.md#compliance-verification)

### 6.2 Renewal & expiration

| Phase | Platform behavior |
|-------|-------------------|
| **60 days before expiry** | Creator notification |
| **30 days before expiry** | Dashboard warning; email reminder |
| **Expiry date** | Grace period begins (default: 14 days) |
| **Post-grace** | Listings suspended; `compliance.expired` event |

Expired compliance does not silently continue — [Marketplace Mechanics](../product/marketplace-mechanics.md#compliance-verification)

Creator surface: [Creator Compliance page](../pages/creator/compliance.md)

### 6.3 Food handler & staff coverage

- Food handler certificate must match verified identity or registered staff member
- Creators with employees must ensure certified food handler supervision during production
- `TODO(decision):` Staff roster verification for creators above headcount threshold

---

## 7. Labeling, Allergens & Customer Disclosures

### 7.1 Mandatory listing fields

Every menu item must include:

- Complete ingredient list
- Major allergen disclosures ("Contains" / "May contain")
- Accurate dietary tags (vegan, gluten-free, etc.) — only when substantiated
- Fulfillment-relevant information (lead time, storage, serving size)

### 7.2 Allergen standards

| Rule | Enforcement |
|------|-------------|
| Major allergens disclosed per applicable regulations | Listing required fields |
| Checkout acknowledgment for flagged allergens | Customer must confirm review |
| No "allergen-free" claims without substantiation | Moderation + compliance review |
| Confirmed mislabeling | Immediate suspension pending investigation |

Incident response: [Food Safety Incident SOP](../operations/food-safety-incident-sop.md)

### 7.3 Cross-contact

Creators must not claim zero cross-contact risk in shared kitchens. Customers with severe allergies bear responsibility for reviewing disclosures and communicating with creators.

---

## 8. Fulfillment Model Compliance

Different fulfillment models carry distinct compliance considerations:

| Model | Compliance notes |
|-------|------------------|
| **Pickup — scheduled** | Time/temperature control for ready-to-eat foods |
| **Pickup — same day / food truck** | Mobile vending permits; location disclosure |
| **Delivery — creator managed** | Safe transport; jurisdiction delivery rules for cottage food |
| **Catering / events** | Catering permits where required; deposit terms disclosed |
| **Pop-up / ticketed events** | Temporary event permits where required |
| **Shipping — non-perishable** | Only where legally permitted; packaging and labeling standards |

Perishable nationwide shipping is **not** a default v1 model.

[Marketplace Mechanics — Fulfillment Models](../product/marketplace-mechanics.md#fulfillment-models)

---

## 9. Incident Response & Regulatory Cooperation

### 9.1 Food safety incidents

Reports of allergic reaction, foodborne illness, tampering, or confirmed mislabeling trigger the food safety incident workflow.

| Class | Examples | Response |
|-------|----------|----------|
| **P0 — Critical** | Allergic reaction, illness, tampering | Immediate listing/order suspension; investigation |
| **P1 — High** | Confirmed allergen mislabeling, unlicensed operation | Same-day response |

Operations: [Food Safety Incident SOP](../operations/food-safety-incident-sop.md) · [Trust & Safety Standards — Incident Response](../docs/standards/trust-and-safety-standards.md#incident-response)

### 9.2 Regulatory notification

`TODO(decision):` Define when and how Marketplate notifies health authorities per launch market legal counsel guidance.

Framework considerations:

- Mandatory reporting statutes for foodborne illness
- Cooperation with health department investigations
- Document preservation for regulatory requests
- Customer notification obligations

### 9.3 Evidence preservation

| Artifact | Retention |
|----------|-----------|
| Order snapshot | Life of dispute + 7 years |
| Listing at time of order | Immutable archive |
| Verification documents | Case-linked retention |
| Messages | Case-linked retention |

---

## 10. Jurisdiction Annexes (Placeholder)

Upon launch market decision, counsel must approve jurisdiction-specific annexes appended to this document:

| Annex | Contents |
|-------|----------|
| `TODO(decision):` Launch state/local annex A | Cottage food rules, permit types, category lists, sales caps, labeling |
| `TODO(decision):` Tax annex B | Sales tax collection, food tax exemptions |
| `TODO(decision):` Shipping annex C | Interstate commerce restrictions for food |
| `TODO(decision):` Expansion annex template | Framework for adding new markets |

Platform implementation: jurisdiction templates in [Platform Settings](../pages/admin/platform-settings.md)

---

## 11. Creator & Customer Acknowledgments

### 11.1 Creator acknowledgment

Creators acknowledge at verification and periodically:

- They are solely responsible for food law compliance
- Marketplate verification does not constitute regulatory approval
- They will only sell eligible categories for their compliance status
- They will maintain current documentation

Incorporated in: [Creator Agreement](creator-agreement.md)

### 11.2 Customer acknowledgment

Customers acknowledge at checkout:

- They reviewed creator-provided allergen information
- Marketplate does not prepare food or guarantee allergen-free preparation
- They purchase from the creator as merchant of record

Incorporated in: [Terms of Service](terms-of-service.md)

---

## Related Documents

- [Legal README](README.md)
- [Creator Agreement](creator-agreement.md)
- [Terms of Service](terms-of-service.md)
- [Refund & Cancellation Policy](refund-and-cancellation-policy.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
- [Chef Quality Standards](../docs/standards/chef-quality-standards.md)
- [Verification Review SOP](../operations/verification-review-sop.md)
- [Food Safety Incident SOP](../operations/food-safety-incident-sop.md)
- [Help — Food Safety](../docs/help-center/food-safety.md)
- [Help — Verification](../docs/help-center/verification.md)
