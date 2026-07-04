# Refund Processing SOP

> Standard Operating Procedure for customer and creator-side refund execution. **Humans authorize; Payment Service executes.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety (policy) · Finance (reconciliation)  
**Playbook companion:** [Dispute Resolution](../docs/playbooks/) via [Dispute Resolution SOP](dispute-resolution-sop.md) · [Food Safety Incident](../docs/playbooks/food-safety-incident.md)

---

## Purpose

This SOP defines when and how Marketplate processes refunds to customers and payout adjustments for creators. Refunds originate from dispute resolution, food safety incidents, order cancellations, enforcement actions, and platform errors. Every refund requires human authorization with documented rationale and immutable audit linkage to Payment Service transaction IDs.

Refunds are **never** initiated autonomously by AI. [Trust Service](../engineering/services/trust-service.md) triggers Payment Service via `dispute.resolved` and admin refund endpoints with idempotency keys.

---

## Trigger

| Trigger | Source | Authorizing SOP / playbook |
|---------|--------|----------------------------|
| Dispute resolved — full/partial refund | [Dispute Detail](../pages/admin/dispute-detail.md) | [Dispute Resolution SOP](dispute-resolution-sop.md) |
| Food safety containment — force-cancel | Incident workflow | [Food Safety Incident SOP](food-safety-incident-sop.md) |
| Creator suspension — safety/fraud | Enforcement | [Creator Suspension SOP](creator-suspension-sop.md) |
| Platform-initiated order cancel | Order Service / Support | Support escalation |
| Creator-initiated cancel (customer-requested) | Creator dashboard | Creator policy — logged |
| Payment processor chargeback | Payment webhook | Finance + Trust parallel |
| Goodwill credit (not cash refund) | Senior Trust approval | This SOP — credit path |
| Refund retry after API failure | Dispute case still open | This SOP — retry path |
| Voluntary creator offboarding — open orders | Creator Success | [Creator Suspension playbook](../docs/playbooks/creator-suspension-offboarding.md) Track B |

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Trust & Safety Operator** | Authorize refunds within limit via dispute/incident resolution |
| **Senior Trust & Safety** | Refunds above operator limit; goodwill exceptions |
| **Customer Support** | Execute templated refunds for approved support cases |
| **Finance** | Reconciliation, chargeback response, payout clawback |
| **Engineering On-Call** | Payment API failures, idempotency issues |

**Accountable for policy:** Trust & Safety  
**Accountable for money movement accuracy:** Finance

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Refund authorized in source case (dispute/incident) | Case status allows resolve |
| Order payment data loaded | Charge captured; amount confirmed |
| Operator within refund authority limit | Server-side RBAC |
| Payment Service refund endpoint operational | Health check |
| Idempotency key available | `dispute_id` or `order_id` + reason code |
| Rationale recorded in case | Min 20 chars before refund executes |

Refunds without linked audit case are **prohibited** except Finance manual correction with dual approval.

---

## Workflow

### Path A — Dispute-initiated refund

1. Operator completes [Dispute Resolution SOP](dispute-resolution-sop.md) Steps 1–4.
2. Select outcome: full refund, partial refund (enter amount), or credit.
3. Confirm modal displays: order total, refund amount, payment method, creator payout impact.
4. Submit resolve → Trust Service calls Payment Service `/api/v1/admin/payments/refund` with idempotency key = `dispute_id`.
5. On success: store `payment_transaction_id` in case audit; emit `payment.refund_completed` → dispute status updated.
6. On failure: case remains **open**; display processor error; alert Finance; retry per Step 6 below.

### Path B — Incident-initiated refund (force-cancel)

1. Trust Supervisor executes force-cancel per [Food Safety Incident SOP](food-safety-incident-sop.md) Phase 2.
2. Order Service platform cancel triggers full refund for each affected order.
3. Trust Operator verifies refund status on each order in incident log.
4. Failed refunds → open dispute case or manual refund ticket linked to `incident_id`.

### Path C — Enforcement-initiated refund

1. Per [Creator Suspension SOP](creator-suspension-sop.md) active order matrix:
   - Safety/fraud suspension → force-cancel all → full refund
   - Compliance expiry → existing orders may fulfill; no automatic refund
2. Supervisor documents order-by-order decision in enforcement audit.
3. Support notifies customers with refund expectation (5–10 business days).

### Path D — Goodwill credit

1. Senior Trust approves credit amount and rationale (no cash refund).
2. Payment Service applies account credit — not a charge reversal.
3. Audit: `refund.type=credit`, linked to case ID.

### Step 5 — Creator payout adjustment

1. Payment Service adjusts creator payout per refund — may trigger payout hold during investigation.
2. Finance reconciles in daily settlement report.
3. Clawback for creator-fault refunds documented on [Creator Admin Detail](../pages/admin/creator-admin-detail.md).

### Step 6 — Failed refund retry

| Failure type | Action |
|--------------|--------|
| Processor timeout | Retry with same idempotency key (3 attempts, exponential backoff) |
| Insufficient capture | Escalate Finance — partial capture edge case |
| Invalid payment method | Support contacts customer for alternate resolution |
| Persistent failure | Finance manual refund; case note with external reference |

Never mark dispute resolved until refund confirms or manual exception documented.

### Step 7 — Customer notification

1. Notification Service sends resolution email with amount and timeline.
2. Template per [Food Safety playbook — Customer Resolution](../docs/playbooks/food-safety-incident.md#template-customer-resolution--refund) or dispute standard template.
3. Notification failure logged — operator sees warning; refund still valid.

---

## AI Responsibilities

**None for refund execution.** AI does not:

- Calculate refund amounts
- Initiate payment API calls
- Approve financial outcomes
- Notify customers of refunds

Dispute message summarization (optional AI assist) does not include refund recommendations per [Dispute Resolution SOP](dispute-resolution-sop.md).

---

## Human Responsibilities

| Action | Human requirement |
|--------|-------------------|
| Refund authorization | Operator or Senior per authority matrix |
| Partial refund amount | Operator enters — validated ≤ order total |
| Force-cancel decision | Trust Supervisor |
| Goodwill credit | Senior Trust approval |
| Manual Finance refund | Finance dual approval + Trust case link |
| Chargeback response evidence | Finance + Trust — human files |
| Refund without dispute (exception) | Trust Lead + Finance sign-off |
| Creator payout hold release | Finance + Trust Lead per investigation outcome |

Authority limits (configurable [Platform Settings](../pages/admin/platform-settings.md)):

| Role | Refund limit (v1 default) |
|------|---------------------------|
| Dispute investigator | Up to order total per case |
| Senior Trust | Unlimited |
| Support (pre-approved templates) | Up to $50 — `TODO(decision):` |

---

## Escalation Rules

| Condition | Escalate to |
|-----------|-------------|
| Refund > operator limit | Senior Trust |
| Payment API failure after 3 retries | Finance + Engineering |
| Chargeback received | Finance + Trust — urgent |
| Refund exceeds captured amount | Finance |
| Customer disputes refund amount post-resolution | New dispute or appeal |
| Creator disputes payout clawback | Trust Lead + Finance |
| Suspected refund abuse (customer) | Fraud playbook |
| Bulk refunds from incident (> 10 orders) | IC + Finance coordination |

---

## SLA

| Scenario | Target |
|----------|--------|
| Refund execution after authorized resolve | Immediate (API); 5–10 BD customer bank posting |
| Failed refund first retry | Within 1 hour |
| Finance manual refund | 2 business days |
| Chargeback evidence submission | Per processor deadline — urgent |
| Food safety P0 refund | ≤ 24 hours from containment |
| Incident bulk refund completion | ≤ 72 hours |

Customer-facing expectation: always communicate 5–10 business days for card refunds.

---

## Audit Logging

| Event | Required fields |
|-------|-----------------|
| `refund.authorized` | `operator_id`, `case_id`, `order_id`, `amount`, `type` (full/partial/credit), `rationale`, `timestamp` |
| `refund.executed` | `payment_transaction_id`, `idempotency_key`, `processor_response`, `timestamp` |
| `refund.failed` | `error_code`, `retry_count`, `case_id` |
| `refund.manual` | `finance_approver_id`, `external_reference`, `case_id` |
| `payout.adjusted` | `creator_id`, `order_id`, `adjustment_amount`, `reason` |

Trust Service links refund to dispute/incident audit chain. Finance reconciliation export matches `payment_transaction_id`.

Audit write failure **blocks** refund authorization submit per [Trust Service — Failure Modes](../engineering/services/trust-service.md#failure-modes).

---

## Resolution

Refund **complete** when:

1. Payment Service returns success with `payment_transaction_id`, OR
2. Finance documents manual refund with external reference
3. Case audit updated — dispute may then close
4. Customer notified
5. Creator payout adjustment reflected in settlement

Case cannot be `resolved` with pending refund — invariant enforced in [Dispute Detail](../pages/admin/dispute-detail.md).

---

## Post Mortem

Required when:

- Double refund issued (idempotency failure)
- Refund issued without authorization audit
- Wrong amount refunded (> $5 or > 10% error)
- Bulk incident refunds incomplete after 72h
- Chargeback lost due to missing refund evidence

Finance leads monetary post-mortem; Trust leads process failure. Corrective: idempotency fix, limit adjustment, template update.

---

## Metrics

| Metric | Target |
|--------|--------|
| Refund success rate (first attempt) | ≥ 99% |
| Refund failure rate | 0 unresolved > 24h |
| Time authorize → execute | < 5 min (API) |
| Dispute refund alignment | 100% resolved disputes with correct payment action |
| Chargeback rate | ↓ |
| Chargeback win rate | ↑ |
| Manual refund rate | ↓ |
| Creator clawback disputes | Monitor |

→ [Success Metrics — Trust](../product/success-metrics-overview.md#trust-metrics)

---

## Future Automation

| Initiative | Human gate preserved |
|------------|---------------------|
| Automated retry queue for failed refunds | Retry only — auth human |
| Refund status webhook to customer | Notification only |
| Finance reconciliation auto-match | Exception handling human |
| Bulk refund orchestration for incidents | IC authorizes batch |
| Chargeback evidence auto-assembly from case | Human submits to processor |

**Never automate:** Refund authorization or amount selection.

---

## Related Documents

- [Dispute Resolution SOP](dispute-resolution-sop.md)
- [Food Safety Incident SOP](food-safety-incident-sop.md)
- [Creator Suspension SOP](creator-suspension-sop.md)
- [Dispute Detail](../pages/admin/dispute-detail.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Creator Admin Detail](../pages/admin/creator-admin-detail.md)
- [Platform Settings](../pages/admin/platform-settings.md)
- [Marketplate Standards — Refunds](../docs/standards/marketplate-standards.md)
