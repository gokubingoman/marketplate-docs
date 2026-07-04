# Chargeback Response SOP

> Standard Operating Procedure for payment chargebacks, Stripe disputes, and creator payout clawbacks. **Finance leads; Trust & Safety supports fraud cases.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Finance · Trust & Safety  
**Playbook companion:** [Fraud Response](../docs/playbooks/fraud-response.md) · [Payout Processing SOP](payout-processing-sop.md)

---

## Purpose

This SOP defines how Marketplate responds to **chargebacks** and **payment disputes** initiated by customers through their card issuer. Chargebacks differ from platform [Dispute Resolution](dispute-resolution-sop.md) — they involve Stripe, deadlines, evidence submission, and financial liability.

Goals: minimize unjustified losses, protect creators from fraud chargebacks, maintain Stripe account health, and feed fraud patterns to [Fraud Investigation SOP](fraud-investigation-sop.md).

---

## Trigger

| Trigger | Source | Priority |
|---------|--------|----------|
| Stripe `charge.dispute.created` webhook | Payment Service | High — response deadline |
| Stripe dispute status update | Webhook | Medium |
| Creator reports chargeback notification | Support ticket | High |
| Finance daily dispute report | Stripe Dashboard | Medium |
| Elevated chargeback rate alert | Payment Service / Stripe | P1 |

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Finance Operator** | Primary owner — evidence submission, Stripe dashboard |
| **Trust & Safety** | Fraud-related chargebacks; creator investigation |
| **Customer Support** | Customer communication (non-fraud); order context |
| **Legal Counsel** | High-value or precedent disputes |
| **Engineering** | Webhook failures, evidence export bugs |

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Stripe dispute webhooks configured | Payment Service health |
| Order + payment + audit data linkable | `order_id` → `payment_intent_id` |
| Evidence export from Admin Console | Order detail, verification status, comms log |
| Chargeback reason code mapping documented | Finance runbook |
| Creator notification template ready | [Macro Library](../support/macro-library.md) |

---

## Workflow

### Step 1 — Intake (within 4 business hours)

1. Payment Service records dispute: `{ dispute_id, order_id, amount, reason_code, evidence_due_by }`.
2. Finance Operator claims dispute in Stripe Dashboard + internal tracker.
3. Classify: **friendly fraud**, **service issue**, **fraud**, **processing error**.

### Step 2 — Evidence collection (within 2 business days)

Gather for Stripe evidence upload:

| Evidence type | Source |
|---------------|--------|
| Order confirmation + receipt | Order Service |
| Creator verification status at order time | Trust Service |
| Fulfillment proof (pickup confirmation, timestamps) | Order Service |
| Customer communication | Support threads |
| Refund policy version acknowledged at checkout | Legal version ID |
| Platform dispute resolution outcome (if any) | Dispute case |

Trust Operator assists if fraud suspected — do not delay Finance deadline.

### Step 3 — Response decision

| Classification | Action |
|----------------|--------|
| **Valid service failure** | Accept dispute; process refund if not already; creator adjustment per [Refund Processing SOP](refund-processing-sop.md) |
| **Friendly fraud (customer received order)** | Contest with evidence |
| **Creator fraud** | Contest if platform liable; open [Fraud Investigation SOP](fraud-investigation-sop.md); suspend creator |
| **Processing error** | Engineering ticket; accept if platform fault |

Senior Finance approval required to **accept** disputes > $500.

### Step 4 — Stripe submission

1. Upload evidence bundle before `evidence_due_by`.
2. Record submission in audit log with operator ID.
3. Notify creator if chargeback affects their payout — macro **Chargeback notice**.

### Step 5 — Outcome handling

| Outcome | Action |
|---------|--------|
| **Won** | Close internal case; restore creator payout if held |
| **Lost** | Record loss; clawback per [Payout Processing SOP](payout-processing-sop.md) Path D |
| **Withdrawn** | Close case; verify order state consistent |

Update chargeback rate metrics for executive dashboard.

### Step 6 — Pattern review

If ≥3 chargebacks same creator or customer in 90 days → Trust pattern review per [Fraud Response](../docs/playbooks/fraud-response.md).

---

## AI Responsibilities

None autonomous. Payment risk scoring may **alert** — humans decide response.

---

## Human Responsibilities

| Action | Owner |
|--------|-------|
| Evidence submission | Finance |
| Fraud classification | Trust & Safety |
| Creator communication | Support (template) |
| Accept/contest decision | Finance (+ Legal if > threshold) |

---

## Escalation Rules

| Condition | Escalate to | Timeline |
|-----------|-------------|----------|
| Evidence deadline < 24h and incomplete | Finance Lead | Immediate |
| Suspected fraud ring | Fraud Investigation Lead | 4 hours |
| Chargeback rate > 1% rolling 30d | Executive + Stripe rep | Same week |
| Legal threat in dispute | Legal Counsel | Same day |

---

## SLA

| Stage | Target |
|-------|--------|
| Dispute acknowledged internally | 4 business hours |
| Evidence collection complete | 2 business days |
| Stripe submission | ≥ 24h before deadline |
| Creator notification | 1 business day of intake |

---

## Audit Logging

`chargeback.{received|evidence_submitted|won|lost}` with `dispute_id`, `order_id`, `operator_id`, `amount_cents`.

---

## Metrics

| Metric | Owner |
|--------|-------|
| Chargeback rate (count / GMV) | Finance |
| Win rate | Finance |
| Disputes by reason code | Finance · Product |
| Creator chargeback concentration | Trust |

→ [Metrics Definitions](../analytics/metrics-definitions.md)

---

## Related Documents

- [Payment Service](../engineering/services/payment-service.md)
- [Dispute Resolution SOP](dispute-resolution-sop.md)
- [Refund Processing SOP](refund-processing-sop.md)
- [Payout Processing SOP](payout-processing-sop.md)
- [Fraud Investigation SOP](fraud-investigation-sop.md)
