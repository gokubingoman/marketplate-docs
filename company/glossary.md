# Marketplate Glossary

> Canonical definitions for terms used across company, product, engineering, operations, and support documentation.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

When a term appears in documentation, use the definition here. If a new term is introduced, add it to this glossary in the same PR or documentation batch. For philosophical context, see [Company Philosophy](company-philosophy.md). For trust model details, see [Marketplace Mechanics](../product/marketplace-mechanics.md).

---

## A

### Allergen Disclosure

Required listing of major allergens and cross-contamination risks for a product or menu item. Allergen disclosure is a trust-critical data field — incomplete or inaccurate disclosure is a safety and liability issue, not a UX nicety.

### Audit Trail

A chronological, tamper-resistant record of actions taken on trust-critical, financial, or compliance workflows. Every verification decision, payout, moderation action, and admin override must leave an audit trail.

---

## B

### Batch Order

An order model where customers purchase a fixed quantity of items produced in a scheduled production run (e.g., "12 meals for pickup Sunday"). Common for meal prep operators. Contrast with **On-Demand Order**.

### Business OS (Operating System)

Marketplate's role as integrated infrastructure for independent food creators — not merely a storefront. Includes discovery, commerce, fulfillment, compliance, communication, payouts, and reputation management.

---

## C

### Catering Order

A quote-based or deposit-based order for event food with custom menus, headcount, delivery timing, and often multi-stage payment. Workflow differs from standard marketplace checkout.

### Commercial Kitchen

A licensed shared production facility where multiple food creators prepare goods. Commercial kitchens may operate as Marketplate ecosystem partners. Creators who produce in commercial kitchens require **Kitchen Verification** tied to that facility.

### Commissary

A licensed kitchen facility that prepares food for off-site sale or service — often used by food trucks and mobile vendors. Functionally similar to a commercial kitchen; verification must reflect the commissary as the production environment.

### Compliance Status

The current state of a creator's adherence to applicable food law, licensing, and platform policy requirements. Compliance status can affect listing visibility, order acceptance, and verification badge display.

### Cottage Food

Food produced in a home kitchen under jurisdiction-specific cottage food laws, with defined product restrictions and labeling requirements. Cottage food operators are a core creator segment.

### Creator

An independent food entrepreneur who sells food they produce — including chefs, meal prep operators, bakers, caterers, food truck operators, cottage food producers, and pop-up vendors. "Creator" is Marketplate's preferred term over "seller," "vendor," or "merchant" because it emphasizes identity, craft, and trust.

### Creator Dashboard

The authenticated workspace where creators manage listings, orders, fulfillment, compliance documents, payouts, and customer communication.

### Creator Storefront

A creator's public-facing presence on Marketplate — profile, verification badges, menu or catalog, reviews, and ordering entry points. The storefront represents the creator's brand; Marketplate provides the trust layer.

### Customer

An individual who discovers, orders from, and reviews verified food creators on Marketplate. Customers may purchase for personal consumption, events, or gifting.

---

## D

### Delivery Aggregator

A platform (e.g., Uber Eats, DoorDash) that connects customers to existing restaurant supply through on-demand delivery, typically taking commission and owning much of the customer relationship. Marketplate is **not** a delivery aggregator — see [Market Context](market-context.md).

---

## F

### Food Safety Verification

The process of confirming that a creator's production practices, licenses, and documentation meet applicable food safety standards. A non-negotiable trust pillar. Includes review of permits, inspections, and ongoing compliance.

### Fulfillment Model

How a creator delivers goods to the customer: pickup, local delivery, shipping, on-site catering, or hybrid. Creators configure their fulfillment model; Marketplate coordinates but does not force a single model.

### Fulfillment Window

A scheduled time range during which a customer picks up an order or receives delivery. Critical for batch production and meal prep workflows.

---

## I

### Identity Verification

Confirmation that a creator is a real person (or legitimate business entity) operating the account. Includes document review and may include biometric or third-party verification services. Distinct from **Kitchen Verification**.

---

## K

### Kitchen Verification

Confirmation that a creator's stated production environment — home kitchen under cottage food law, commercial kitchen, commissary, food truck, or pop-up venue — is real, licensed where required, and matches what the creator represents to customers.

### Kitchen Profile

The documented record of a creator's production environment(s): address, license numbers, inspection dates, facility type, and verification status. Creators with multiple or changing environments (pop-ups, food trucks) may have multiple kitchen profiles.

---

## L

### Listing

A creator's offered product or menu item on Marketplate, including description, pricing, photos, allergen information, fulfillment options, and availability. Listings inherit the creator's verification and compliance status.

### Local Food Economy

The ecosystem of independent food creators, commercial kitchens, customers, regulators, and local fulfillment partners in a geographic area. Marketplate's long-term vision includes serving as infrastructure for this economy — see [Vision](vision.md).

---

## M

### Marketplace

The discovery and transaction layer connecting verified creators with customers. The marketplace is trust-weighted — verification and reputation influence visibility alongside relevance and quality.

### Marketplace OS

See **Business OS**. Shorthand for Marketplate as the combined marketplace and operating system.

### Meal Prep Operator

A creator who prepares batch meals on a recurring schedule for subscription or repeat-order customers. A primary persona with distinct fulfillment, labeling, and scheduling needs.

### Moderation

Review of user-generated content (listings, reviews, messages, photos) for policy compliance, safety, and trust integrity. AI may recommend; humans approve on trust-critical moderation.

---

## O

### On-Demand Order

An order placed and fulfilled in near-real-time, typical of restaurant delivery but less common for independent creators. Marketplate supports on-demand where creators offer it but does not optimize the platform exclusively for this model.

### Order Lifecycle

The states an order passes through from placement to completion: placed → confirmed → in production → ready → fulfilled → completed (or cancelled/refunded). Each transition is logged and visible to creator and customer.

---

## P

### Payout

Transfer of earned funds from Marketplate to a creator after order completion, minus applicable fees. Payout workflows require audit trails and defined SLAs.

### Pickup Order

An order where the customer collects food at a specified location and **Fulfillment Window**. Common for cottage food, bakers, and meal prep.

### Pop-Up

A temporary food service event or short-term production location. Kitchen verification must reflect the pop-up venue for the duration of operation.

### Pre-Order

An order placed in advance of production, often required for batch production, custom baked goods, or limited-quantity items. Pre-orders include a defined fulfillment date.

### Production Run

A scheduled batch of food prepared together — e.g., Sunday meal prep for 40 customers. Production runs anchor batch ordering and inventory planning for meal prep operators.

---

## R

### Review

Customer feedback on a completed order, including rating and written commentary. Reviews contribute to **Trust Score** and creator reputation. Review integrity is protected against fraud and retaliation.

### Review Integrity

Policies and systems ensuring reviews are authentic, tied to verified purchases, and resistant to manipulation. Includes moderation and anomaly detection.

---

## S

### Subscription Order

A recurring order model where customers receive products on a defined cadence (weekly, biweekly, monthly). Requires subscription management, billing, and skip/pause flows.

### Super Admin

Internal Marketplate role with elevated platform access for verification, moderation, support escalation, and system configuration. Super Admin actions require audit logging.

---

## T

### Trust Badge

A visible indicator on a creator's storefront confirming a specific verification or compliance milestone — e.g., identity verified, kitchen verified, food safety current. Badges must reflect real-time status, not one-time onboarding.

### Trust-Critical Path

Any workflow where failure or error could impact food safety, financial integrity, identity accuracy, or customer trust — e.g., verification, payouts, allergen data, moderation. Trust-critical paths require human approval, audit trails, and higher testing standards.

### Trust Score

A composite signal reflecting a creator's verification status, compliance history, review quality, fulfillment reliability, and incident record. Trust Score influences marketplace visibility and customer confidence. Exact weighting is defined in [Marketplace Mechanics](../product/marketplace-mechanics.md).

TODO(decision): Define Trust Score component weights and public vs. internal visibility — which factors are shown to customers and which are internal-only signals.

### Trust Thesis

The foundational principle that **trust is the product; software enables trust**. All platform decisions trace back to this thesis — see [Mission](mission.md).

---

## V

### Verification

The umbrella process for confirming creator identity, kitchen environments, and food safety compliance. Verification is ongoing — not a one-time onboarding checkbox. Subtypes: **Identity Verification**, **Kitchen Verification**, **Food Safety Verification**.

### Verification Status

The current state of a creator's verification: pending, in review, verified, expired, suspended, or rejected. Verification status determines badge display and may gate order acceptance.

---

## Platform and Documentation Terms

### ADR (Architecture Decision Record)

A documented record of a significant technical or architectural decision. Stored in [`decisions/`](../decisions/) using the [ADR template](../templates/adr-template.md).

### Agent (AI Agent)

An AI system or autonomous documentation/build agent operating against Marketplate's institutional memory with defined domain ownership — e.g., Company & Vision Agent, Trust & Safety Agent.

### Institutional Memory

This repository — the canonical knowledge base for designing, building, and operating Marketplate. See [Founding Constitution](constitution.md).

### Phase (Documentation Phase)

A stage in the [Phased Rollout](../roadmap/phased-rollout.md) plan for building documentation and capabilities: Foundation → Design & UX → Engineering → Operations → Launch.

### SLA (Service Level Agreement)

A measurable commitment for workflow completion time — e.g., verification review within 48 hours, support first response within 4 hours. Every operational workflow defines an SLA.

### SOP (Standard Operating Procedure)

A documented operational workflow with owner, trigger, steps, escalation rules, and audit requirements. Template: [SOP template](../templates/sop-template.md).

---

## Related Documents

- [Founding Constitution](constitution.md) — Governing principles
- [Mission](mission.md) — Trust thesis and purpose
- [Vision](vision.md) — Long-term direction
- [Values](values.md) — Behavioral norms
- [Market Context](market-context.md) — Category and competitive terms in context
- [Company Philosophy](company-philosophy.md) — Decision frameworks
- [Product Overview](../product/overview.md) — Product terminology in use
- [Product Personas](../product/personas.md) — Creator and customer segment definitions
- [Marketplace Mechanics](../product/marketplace-mechanics.md) — Trust model and marketplace terms
- [Brand Naming](../brand/naming-conventions.md) — Brand-specific naming conventions
- [Phased Rollout](../roadmap/phased-rollout.md) — Documentation phase definitions
