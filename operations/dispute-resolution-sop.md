# Dispute Resolution SOP

> Standard Operating Procedure for order dispute mediation and refund outcomes. **Evidence-based; human decides all financial resolutions.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook companion:** [Food Safety Incident](../docs/playbooks/food-safety-incident.md) · [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md)

---

## Purpose

This SOP defines how Trust & Safety operators investigate and resolve order disputes when creators and customers cannot reach agreement through messaging. Disputes are mediated in [Dispute Detail](../pages/admin/dispute-detail.md) with full order context, policy version lock, and immutable case records per [Trust & Safety Standards — Dispute Resolution](../docs/standards/trust-and-safety-standards.md#dispute-resolution).

Financial outcomes — full refund, partial refund, credit, or no action — require human approval, documented rationale, and audit trail. Refund execution flows through [Trust Service — Dispute Manager](../engineering/services/trust-service.md) to Payment Service.

---

## Trigger

| Trigger | Source | Priority |
|---------|--------|----------|
| Customer opens dispute on order | In-app dispute flow | Standard |
| Creator escalates unresolved customer issue | Creator support / order detail | Standard |
| Support ticket tagged `dispute` | Customer Support | Per ticket urgency |
| Allergen concern post-order | Order messaging → dispute | **Urgent** |
| Moderation escalation with open order | [Moderation Queue](../pages/admin/moderation-queue.md) | Urgent |
| Pattern detection — repeat disputes on creator | Trust Service risk scoring | Elevated review |
| Chargeback initiated | Payment processor webhook | **Urgent** — parallel track |

**Preferred path:** Creator ↔ customer direct resolution via messaging before platform escalation per [Marketplace Mechanics — Disputes](../product/marketplace-mechanics.md#disputes).

System event: `dispute.opened` → admin queue + party notifications.

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Dispute Investigator (Trust Operator)** | Case investigation, evidence collection, resolution recommendation |
| **Senior Trust & Safety** | Urgent cases, refunds above limit, reopen, appeal review |
| **Customer Support** | Initial triage, customer acknowledgment, template comms |
| **Finance** | Payment reconciliation, chargeback coordination |
| **Trust Lead** | Pattern disputes, creator account review, policy exceptions |

**Accountable team:** Trust & Safety  
**System of record:** Trust Service dispute schema + Payment Service transaction IDs

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Dispute investigator role | RBAC — refund limits enforced server-side |
| Access to [Dispute Detail](../pages/admin/dispute-detail.md) | `/admin/disputes/:id` |
| Order payment data loaded before resolve enabled | UI blocks premature action |
| Policy version at checkout visible in case | Policy lock displayed |
| Refund API operational | Payment Service staging verified |
| Familiarity with refund standards | [Marketplate Standards — Refunds](../docs/standards/marketplate-standards.md) |
| Allergen checklist for safety disputes | Cross-link [Food Safety Incident SOP](food-safety-incident-sop.md) |

Senior role required for: refunds above operator limit, case reopen, dispute appeal decisions.

---

## Workflow

### Step 1 — Case intake

1. Open case from disputes list or [Admin Dashboard](../pages/admin/admin-dashboard.md) urgent alert.
2. Read case header: order ID, amount, parties, status, urgency flag, SLA timer.
3. Review customer claim summary and creator response (if any).
4. Pull [Creator Admin Detail](../pages/admin/creator-admin-detail.md): dispute rate, prior disputes, enforcement history.
5. Tag `food-safety` if allergen or illness claimed — **stop standard path**; invoke [Food Safety Incident SOP](food-safety-incident-sop.md).

### Step 2 — Evidence collection

1. **Order details:** line items, allergens declared at order time, fulfillment method, completion timestamp.
2. **Message thread:** chronological customer ↔ creator messages; platform messages read-only.
3. **Photos:** customer-uploaded evidence; request additional if missing.
4. **Listing snapshot:** catalog version at time of order — compare to current listing.
5. **Payment breakdown:** subtotal, fees, tax, total — required before financial resolution.
6. **Policy:** refund/cancellation policy version customer acknowledged at checkout.

Use **Request information** action to send templated messages; status → `pending_info`. Clock may pause per platform settings.

### Step 3 — Analysis

Apply mediation standards:

| Principle | Application |
|-----------|-------------|
| Evidence-based | Decisions cite order record, messages, photos — not assumptions |
| Policy version lock | Use policy active at checkout |
| Neutral tone | No platform favoritism toward take rate |
| Pattern awareness | Repeat creator disputes → escalation to account review |

Common dispute categories:

| Category | Typical evidence | Outcome range |
|----------|------------------|---------------|
| Wrong/missing items | Order ticket, photos, messages | Partial or full refund |
| Quality complaint | Photos, repeat pattern | Partial refund or credit |
| Late/no fulfillment | Fulfillment timeline | Full refund if creator fault |
| Allergen concern | Listing at order time, medical claim | Full refund; safety playbook |
| Customer unreasonable | Creator evidence, policy | No action |
| Platform defect | Engineering confirmation | Full refund; no creator penalty |

AI may summarize message threads internally — **AI does not select outcome**.

### Step 4 — Resolution decision (human approval gate)

Operator **explicitly selects** outcome in resolution panel:

| Outcome | When | Payment action |
|---------|------|----------------|
| **Full refund** | Creator fault clear; safety issue; platform defect | Refund 100% order total |
| **Partial refund** | Partial fault; goodwill gesture | Amount ≤ order total — validated |
| **Credit** | Repeat customer goodwill; minor issue | Account credit via Payment Service |
| **No action** | Insufficient evidence; customer error; policy excludes | No payment movement |

Requirements:

- Rationale required (min 20 chars) — visible in audit
- Partial refund amount validated server-side ≤ order total
- Double confirmation modal for all financial resolutions
- Notify parties checkbox — default on

Submit via `/api/v1/admin/disputes/:id/resolve` — idempotent with `dispute_id`.

### Step 5 — Post-resolution

1. Trust Service emits `dispute.resolved` → Payment Service executes refund/credit.
2. If refund fails: case remains open; alert Finance; retry with idempotency key.
3. Parties notified via Notification Service with calm, precise copy.
4. If pattern detected (≥ 3 disputes / 30 days on creator): flag for [Creator Admin Detail](../pages/admin/creator-admin-detail.md) review — possible [Moderation SOP](moderation-sop.md) or [Creator Suspension SOP](creator-suspension-sop.md).
5. Appeal window: 7 days — either party may appeal to Senior Trust reviewer.

---

## AI Responsibilities

Dispute resolution is **human-only** for outcomes. Limited AI assist:

| Function | Role |
|----------|------|
| Message thread summarization | Internal context card — optional, not binding |
| Allergen keyword flagging on intake | Routes to urgent / food safety — human confirms |
| Duplicate dispute pattern detection | Risk signal on creator profile — human investigates |
| Refund amount suggestion | **Not in v1** — operator enters amount |
| Resolve dispute / execute refund | **Never** |

[Moderation Assist](../ai/moderation-assist.md) and [Verification Assist](../ai/verification-assist.md) are not in the dispute resolution chain. Fraud signals from other systems may appear as context only.

---

## Human Responsibilities

| Action | Human requirement |
|--------|-------------------|
| All dispute outcomes | Investigator selects and submits |
| Financial amounts | Operator enters; senior approves above limit |
| Request information messages | Operator reviews template before send |
| Food safety escalation | Human classifies — never auto-close safety disputes |
| Chargeback response | Finance + Trust collaborate — human files evidence |
| Case reopen | Senior role only — new audit entry |
| Appeal decision | Independent senior reviewer — uphold/modify/reverse |
| Creator penalty from dispute | Separate enforcement action via [Moderation SOP](moderation-sop.md) — not bundled in refund |

Operators must not resolve disputes involving their own orders or test accounts.

---

## Escalation Rules

| Condition | Escalate to | Action |
|-----------|-------------|--------|
| Allergen exposure or illness claimed | [Food Safety Incident SOP](food-safety-incident-sop.md) | P0/P1 path |
| Refund amount > operator limit | Senior Trust & Safety | Senior resolves |
| Payment refund API failure | Finance + Engineering | Manual refund track |
| Creator dispute rate anomaly | Trust Lead | Account review |
| Legal threat in messages | Legal | Hold public statements |
| Chargeback received | Finance + Trust | Parallel investigation |
| SLA breach imminent (3 BD standard) | Supervisor | Reassign |
| Platform bug caused dispute | Engineering + IC | Fix + customer remediation |
| Either party appeals | Senior reviewer (not original) | 5 business days |

Escalation: Investigator → Senior T&S → Trust Lead → [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md).

---

## SLA

Per [Trust & Safety Standards — Dispute Resolution](../docs/standards/trust-and-safety-standards.md#dispute-resolution):

| Case type | Resolution SLA |
|-----------|----------------|
| Standard dispute | 3 business days from platform escalation |
| Urgent (allergen, chargeback) | 24 hours first action; 72 hours resolution |
| `pending_info` | Clock pauses until party responds (max 5 BD wait, then decide on available evidence) |
| Appeal | 5 business days from appeal submit |

Configurable: [Platform Settings](../pages/admin/platform-settings.md) → Trust & SLAs.

SLA breach triggers alert on [Admin Dashboard](../pages/admin/admin-dashboard.md).

---

## Audit Logging

Immutable audit per [Trust Service](../engineering/services/trust-service.md):

| Event | Required fields |
|-------|-----------------|
| `dispute.opened` | `dispute_id`, `order_id`, `initiator`, `category`, `timestamp` |
| `dispute.request_info` | `operator_id`, `dispute_id`, `recipient`, `message`, `timestamp` |
| `dispute.resolved` | `operator_id`, `dispute_id`, `outcome`, `amount`, `rationale`, `policy_version`, `payment_transaction_id`, `notify_parties`, `timestamp` |
| `dispute.escalated` | `operator_id`, `dispute_id`, `escalated_to`, `reason` |
| `dispute.reopened` | `senior_operator_id`, `dispute_id`, `original_outcome`, `reason` |
| `dispute.appeal_decided` | `reviewer_id`, `decision`, `rationale` |

Payment refund includes idempotency key = `dispute_id`. Audit write failure blocks resolution.

Evidence artifacts: order snapshot, listing version, message exports — case-linked retention per [Trust & Safety Standards — Evidence preservation](../docs/standards/trust-and-safety-standards.md#evidence-preservation).

---

## Resolution

Case **resolved** when:

1. Operator submits outcome with rationale
2. `dispute.resolved` event emitted
3. Payment action completes (or documented manual exception)
4. Parties notified (or notification failure logged with warning)
5. Case status → `resolved`

| Outcome | Creator impact | Customer impact |
|---------|----------------|-----------------|
| Full refund | Payout adjusted; dispute rate increases | Funds returned 5–10 BD |
| Partial refund | Partial payout adjustment | Partial return |
| Credit | None direct | Account credit |
| No action | Dispute recorded | No payment movement |

Unresolved refunds keep case `open` — never mark resolved without payment confirmation.

---

## Post Mortem

Required when:

- Refund issued incorrectly — clawback or goodwill correction needed
- Safety dispute closed without food safety playbook
- SLA breach on urgent allergen dispute
- Chargeback lost due to insufficient evidence collection
- Pattern of disputes indicating systemic product defect

**Process (5 business days):**

1. Case timeline reconstruction from audit trail
2. Evidence adequacy review
3. Policy clarity — was checkout policy ambiguous?
4. Corrective actions: template update, checklist, product fix, creator coaching
5. Update this SOP or [Dispute Detail](../pages/admin/dispute-detail.md) spec

Trust Lead signs off on process failures; Engineering owns product defects.

---

## Metrics

| Metric | Definition | Target |
|--------|------------|--------|
| Dispute rate | Disputes / completed orders | ↓ |
| Dispute resolution SLA | Resolved within SLA / total | ≥ 90% |
| Median time to resolution | Hours open → resolved | ↓ |
| Full vs. partial refund ratio | By category | Monitor |
| Appeal rate | Appeals / resolved | Monitor |
| Appeal overturn rate | Modified or reversed / appeals | Monitor calibration |
| Repeat dispute creators | Creators with ≥ 3 disputes / 30d | ↓ — trigger review |
| Refund failure rate | Failed payment actions / attempts | 0 |
| Chargeback win rate | Won / total chargebacks | ↑ |

→ [Success Metrics — Trust](../product/success-metrics-overview.md#trust-metrics)

---

## Future Automation

| Initiative | Human gate preserved |
|------------|---------------------|
| Disputes list with bulk assign | Human resolves each case |
| Policy precedent search from past cases | Operator decides |
| Allergen-specific investigation checklist template | Human classifies and resolves |
| SLA timer with auto-escalation to senior | Escalation only — no auto-refund |
| Payment processor chargeback integration | Human files response |
| Post-resolution satisfaction survey | Feedback only |

**Never automate:** Refund execution, outcome selection, or case closure without human submission.

---

## Related Documents

- [Dispute Detail](../pages/admin/dispute-detail.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Refund Processing SOP](refund-processing-sop.md)
- [Food Safety Incident SOP](food-safety-incident-sop.md)
- [Moderation SOP](moderation-sop.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
- [Creator Admin Detail](../pages/admin/creator-admin-detail.md)
- [Platform Settings](../pages/admin/platform-settings.md)
