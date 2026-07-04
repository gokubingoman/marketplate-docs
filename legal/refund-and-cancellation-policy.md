# Refund & Cancellation Policy

> **DRAFT — FRAMEWORK ONLY.** Requires review and approval by qualified legal counsel before publication. Do not present to users until counsel-approved.

**Status:** Draft — Framework  
**Version:** 1.0.0  
**Effective date:** `TODO(decision):` Set upon legal approval  
**Last updated:** 2026-07-03  
**Owner:** Legal · Trust & Safety

**Plain-language summary:** [Help — Refunds & Cancellations](../docs/help-center/refunds.md)

**Operations alignment:** [Refund Processing SOP](../operations/refund-processing-sop.md) · [Dispute Resolution SOP](../operations/dispute-resolution-sop.md)

---

## 1. Purpose & Scope

This Refund & Cancellation Policy ("**Policy**") defines the framework for order cancellations, refunds, credits, and platform-mediated dispute resolution on Marketplate.

This Policy applies to all transactions facilitated through the Platform. It supplements the [Terms of Service](terms-of-service.md) and binds creators via the [Creator Agreement](creator-agreement.md).

**Policy version lock:** The version of this Policy (and any creator-specific policy) acknowledged at checkout governs that transaction. Dispute resolution uses the policy active at time of purchase.

[Dispute Resolution SOP — Policy version lock](../operations/dispute-resolution-sop.md#step-2--evidence-collection)

Strategic principles: [Marketplace Mechanics — Cancellations and refunds](../product/marketplace-mechanics.md#cancellations-and-refunds)

---

## 2. Definitions

| Term | Definition |
|------|------------|
| **Cancellation** | Order terminated before or during fulfillment per this Policy |
| **Refund** | Return of funds to customer's original payment method |
| **Credit** | Platform account credit — not a charge reversal |
| **Force-cancel** | Platform-initiated cancellation for safety, compliance, or enforcement |
| **Policy window** | Time period during which customer cancellation qualifies for stated refund terms |
| **Production started** | Creator has begun preparing the order — status tracked in order lifecycle |
| **Deposit** | Partial payment for custom, catering, or event orders with balance due later |
| **Merchant of record** | Creator — seller responsible for the transaction |

---

## 3. Pre-Checkout Disclosure

Before payment, customers see:

- Creator's cancellation and refund terms (within Platform minimums)
- Platform minimums described in this Policy
- Deposit and forfeiture rules for custom orders
- Allergen acknowledgment where applicable

Policies displayed at checkout are binding for that transaction. Creators may not offer terms less protective than Platform minimums for safety or compliance cancellations.

[Marketplace Mechanics — Transparency](../product/marketplace-mechanics.md#transparency) · [Help — Platform Policies](../docs/help-center/platform-policies.md)

---

## 4. Cancellation Rules

### 4.1 Default cancellation principles

| Scenario | Default outcome | Notes |
|----------|-----------------|-------|
| **Customer cancels within policy window** | Full refund per creator/platform policy disclosed at checkout | Window typically before production starts |
| **Customer cancels after window or production started** | Refund per creator policy — may be partial or none | Creator policy disclosed at checkout |
| **Creator-initiated cancel** | **Full refund** automatically | Impacts creator reliability metrics |
| **Custom order / catering deposit** | Per deposit forfeiture rules **disclosed pre-payment** | Balance and forfeiture terms at checkout |
| **Platform force-cancel** | **Full refund** | Safety, compliance, or enforcement issue |
| **Missed pickup (customer no-show)** | Typically **no refund** unless creator discretion or exceptional circumstances | See [Help — Pickup](../docs/help-center/pickup.md) |
| **Payment failure / platform error** | Full refund if charged in error | Platform defect — no creator penalty |

Standards: [Marketplate Standards — Default refund principles](../docs/standards/marketplate-standards.md#default-refund-principles)

### 4.2 Customer-initiated cancellation

Customers may cancel eligible orders via Order Detail when the cancellation window is open.

1. Customer selects **Cancel order**
2. System displays refund amount and applicable policy
3. Upon confirmation, refund initiates per Section 5

Cancellation eligibility depends on order status, fulfillment model, and policy window — enforced by Order Service.

### 4.3 Creator-initiated cancellation

Creators who cancel orders must provide reason. Customer receives **automatic full refund**. Creator-initiated cancellations affect:

- Order completion rate
- Trust Score / reliability metrics
- Possible enforcement review for patterns

Creators should cancel only when unable to fulfill — not as substitute for policy design.

### 4.4 Platform force-cancel

Marketplate may force-cancel orders when:

- Food safety or allergen incident requires containment
- Creator suspended for safety, fraud, or compliance failure
- Platform defect prevented proper fulfillment
- Legal or regulatory requirement

Force-cancel results in **full customer refund**. Affected creators may be investigated per [Creator Suspension SOP](../operations/creator-suspension-sop.md).

Operations paths: [Refund Processing SOP — Path B, Path C](../operations/refund-processing-sop.md#workflow)

### 4.5 Custom, catering & deposit orders

Custom and event orders may use split payment (deposit + balance):

| Element | Requirement |
|---------|-------------|
| **Deposit amount** | Disclosed at checkout |
| **Forfeiture conditions** | Explicit pre-payment — e.g., cancel within X days for full deposit refund |
| **Balance due date** | Shown at checkout |
| **Creator cancel** | Full refund including deposit |
| **Customer cancel after forfeiture window** | Per disclosed terms |

Deposit terms acknowledged at checkout are binding.

---

## 5. Refund Processing

### 5.1 Refund methods

| Type | Description |
|------|-------------|
| **Full refund** | 100% of order total returned to original payment method |
| **Partial refund** | Amount ≤ order total — proportional to issue |
| **Account credit** | Senior-approved goodwill — not cash reversal |
| **No refund** | Dispute outcome when policy excludes refund and evidence supports |

Refunds are **never** conditioned on review removal or modification.

### 5.2 Refund authorization

All refunds require **human authorization** with documented rationale. AI does not authorize refunds or select amounts.

| Trigger | Authorizing workflow |
|---------|---------------------|
| Dispute resolution | [Dispute Resolution SOP](../operations/dispute-resolution-sop.md) |
| Food safety force-cancel | [Food Safety Incident SOP](../operations/food-safety-incident-sop.md) |
| Creator/enforcement suspension | [Creator Suspension SOP](../operations/creator-suspension-sop.md) |
| Approved support cases | Support templates within authority limits |
| Chargeback | Finance + Trust parallel track |

[Refund Processing SOP](../operations/refund-processing-sop.md)

### 5.3 Refund timing

| Stage | Timeline |
|-------|----------|
| **Authorization → execution** | Immediate upon human approval (API) |
| **Customer bank posting** | **5–10 business days** after processing |
| **Food safety P0 refund** | ≤ 24 hours from containment decision |
| **Incident bulk refunds** | ≤ 72 hours for batch processing |
| **Finance manual refund** | ≤ 2 business days when API fails |

Customer-facing communication always states **5–10 business days** for card refunds.

### 5.4 Creator payout adjustment

Refunds adjust creator payouts:

- Full refund → full payout reversal for that order
- Partial refund → proportional payout adjustment
- Payout hold may apply during investigation
- Creator-fault refunds documented on creator account

Clawback disputes: escalate to Trust Lead + Finance.

### 5.5 Failed refunds

If payment processor refund fails:

- Case remains **open** until refund confirms or manual exception documented
- Retry with idempotency key (up to 3 attempts)
- Persistent failure → Finance manual refund with external reference

Never mark dispute resolved with pending refund.

---

## 6. Disputes & Platform Mediation

### 6.1 Resolution stages

| Stage | Owner | Description |
|-------|-------|-------------|
| **1 — Direct** | Customer ↔ Creator | Encouraged first via Platform messaging |
| **2 — Platform mediation** | Trust & Safety | When direct resolution fails |
| **3 — Outcome** | Trust & Safety | Refund, partial refund, credit, or no action |
| **4 — Appeal** | Senior Trust reviewer | Either party within 7 days of outcome |

[Marketplace Mechanics — Disputes](../product/marketplace-mechanics.md#disputes)

### 6.2 Opening a dispute

Customers or creators may escalate unresolved issues via:

- In-app dispute flow on Order Detail
- Support ticket — category: Payment & refund

Preferred path: 48 hours of good-faith direct communication before escalation (guidance, not hard block).

### 6.3 Mediation standards

Platform mediation is:

| Principle | Application |
|-----------|-------------|
| **Evidence-based** | Order record, messages, photos, listing snapshot at order time |
| **Policy version lock** | Policies acknowledged at checkout govern decision |
| **Neutral** | No favoritism based on platform fee or take rate |
| **Documented** | Rationale and reason code logged in audit trail |

Common categories:

| Category | Typical outcome range |
|----------|----------------------|
| Wrong/missing items | Partial or full refund |
| Quality complaint | Partial refund or credit |
| Late/no fulfillment (creator fault) | Full refund |
| Allergen concern | Full refund; food safety playbook |
| Customer unreasonable | No action |
| Platform defect | Full refund; no creator penalty |

Urgent disputes (allergen, illness, chargeback): 24-hour first action; 72-hour resolution target.

[Dispute Resolution SOP](../operations/dispute-resolution-sop.md)

### 6.4 Dispute outcomes

| Outcome | Customer | Creator |
|---------|----------|---------|
| **Full refund** | Funds returned 5–10 BD | Payout adjusted; dispute rate increases |
| **Partial refund** | Partial return | Partial payout adjustment |
| **Credit** | Account credit | No direct payout impact |
| **No action** | No payment movement | Dispute recorded |

Pattern of disputes (≥ 3 in 30 days) triggers creator account review.

### 6.5 Appeals

Either party may appeal dispute outcomes within **7 days**. Independent senior reviewer decides within **5 business days** — uphold, modify, or reverse with rationale.

[Trust & Safety Standards — Appeals](../docs/standards/trust-and-safety-standards.md#appeals)

### 6.6 Chargebacks

Payment processor chargebacks operate in parallel to platform disputes. Marketplate provides order evidence to Finance for processor response. Fraudulent chargebacks may result in account restriction.

---

## 7. Creator Refund Policies

### 7.1 Platform minimums

Creators may set policies **within these minimums**:

| Minimum | Rule |
|---------|------|
| **Creator cancel** | Always full refund |
| **Platform force-cancel** | Always full refund |
| **Safety/compliance issue** | Always full refund |
| **Allergen mislabeling confirmed** | Full refund minimum |
| **Policy disclosure** | Must be visible pre-checkout |

Creators may offer **more generous** terms (longer cancellation windows, full refunds in more scenarios).

### 7.2 Stricter creator policies

Creators may set stricter terms (shorter cancellation windows, non-refundable deposits) provided:

- Terms disclosed clearly at checkout
- Terms do not contradict Platform minimums
- Deposit forfeiture rules explicit pre-payment

### 7.3 Prohibited refund practices

- Conditioning refunds on review removal or modification
- Off-platform refund to circumvent Platform audit trail for Platform orders
- Discriminatory refund treatment

---

## 8. Non-Refundable Items & Exceptions

Framework exceptions (subject to dispute mediation and applicable law):

| Situation | Default |
|-----------|---------|
| **Customer no-show (pickup)** | No refund — per pickup policy |
| **Customer-provided incorrect address (delivery)** | Case-by-case; customer fault |
| **Change of mind after production started** | Per creator policy |
| **Subjective taste preference** | Generally no refund unless quality defect |
| **Exceptional circumstances** | Support mediation — illness, emergency, documented creator error |

`TODO(decision):` Jurisdiction-specific consumer protection overrides (e.g., EU withdrawal rights for distance contracts) — counsel to advise whether food perishables exemption applies.

---

## 9. Goodwill Credits

Senior Trust may approve **account credits** (not cash refunds) for:

- Repeat customer goodwill after minor issues
- Service recovery when partial refund insufficient
- Platform error with minimal customer impact

Credits require Senior Trust approval, documented rationale, and audit linkage.

[Refund Processing SOP — Path D](../operations/refund-processing-sop.md#path-d--goodwill-credit)

---

## 10. Customer & Creator Responsibilities

### 10.1 Customer responsibilities

- Review cancellation policy before ordering
- Cancel within policy window when eligible
- Communicate issues promptly with photos where applicable
- Attempt good-faith resolution with creator before escalation
- Provide accurate fulfillment information

### 10.2 Creator responsibilities

- Honor stated policies and fulfillment commitments
- Respond to customer issues within reasonable time
- Initiate cancel + full refund when unable to fulfill
- Cooperate with dispute investigation
- Accept payout adjustments per outcomes

---

## 11. Policy Modifications

Marketplate may update this Policy. Material changes communicated before effective date. Checkout captures version acknowledged. Disputes use version at time of purchase.

---

## 12. Contact & Escalation

| Need | Channel |
|------|---------|
| **Refund status** | Order Detail or support — Payment & refund |
| **Dispute escalation** | In-app dispute or support after creator contact |
| **Appeal** | Instructions in resolution notification |
| **Refund not received after 10 BD** | Support with refund confirmation |

Support SLAs: [Marketplate Standards — Support](../docs/standards/marketplate-standards.md)

`TODO(decision):` Legal contact for regulatory consumer complaint routing.

---

## Related Documents

- [Legal README](README.md)
- [Terms of Service](terms-of-service.md)
- [Creator Agreement](creator-agreement.md)
- [Food Commerce Compliance](food-commerce-compliance.md)
- [Refund Processing SOP](../operations/refund-processing-sop.md)
- [Dispute Resolution SOP](../operations/dispute-resolution-sop.md)
- [Food Safety Incident SOP](../operations/food-safety-incident-sop.md)
- [Creator Suspension SOP](../operations/creator-suspension-sop.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
- [Marketplate Standards — Refunds](../docs/standards/marketplate-standards.md#refunds-and-disputes-standards)
- [Help — Refunds](../docs/help-center/refunds.md)
- [Help — Platform Policies](../docs/help-center/platform-policies.md)
