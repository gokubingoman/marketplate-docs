# Payout Processing SOP

> Standard Operating Procedure for creator payout execution, holds, failures, and clawbacks. **Humans authorize holds and exceptions; Payment Service executes transfers.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Finance · Trust & Safety (holds)  
**Playbook companion:** [Fraud Response](../docs/playbooks/fraud-response.md) · [Refund Processing SOP](refund-processing-sop.md)

---

## Purpose

This SOP defines how Marketplate processes scheduled creator payouts via Stripe Connect — including payout aggregation, compliance and dispute holds, failed transfer recovery, and clawbacks after refunds or fraud findings.

Payouts affect creator livelihood. Every hold, delay, or clawback requires documented rationale, customer/creator communication where applicable, and immutable audit linkage to Payment Service ledger entries.

`TODO(decision):` Stripe Connect model, commission structure, and payout schedule (daily vs. weekly).

---

## Trigger

| Trigger | Source | Action |
|---------|--------|--------|
| Scheduled payout cycle | Payment Service cron | Aggregate eligible balance → transfer |
| Dispute opened on settled order | Trust Service | Place payout hold on affected creator balance |
| Compliance expiry detected | Trust Service scheduled job | Hold new payouts until re-verified |
| Fraud investigation active | Fraud Investigation SOP | Hold or freeze per supervisor |
| Refund completed | Refund Processing SOP | Adjust payout; clawback if already transferred |
| Stripe Connect onboarding incomplete | Creator dashboard | Block payout until `payouts_enabled` |
| Creator reports missing payout | Support ticket | Trace per this SOP |
| Chargeback received | Payment webhook | Finance + Trust parallel review |
| Manual payout exception | Finance + Trust Lead | Documented override |

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Finance Operator** | Daily payout reconciliation, failed transfer retry, Stripe dashboard review |
| **Trust & Safety Supervisor** | Authorize holds and releases tied to disputes, fraud, compliance |
| **Senior Trust & Safety** | Extended holds, clawback approval above operator limit |
| **Customer Support** | Creator payout status inquiries — macros only; escalate per SLA |
| **Engineering On-Call** | Webhook failures, idempotency issues, Connect API errors |

**Accountable for money movement accuracy:** Finance  
**Accountable for hold policy:** Trust & Safety

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Creator Connect account `payouts_enabled` | Payment Service status |
| No active compliance block | Trust Service creator status |
| No unresolved fraud hold | Case status in Trust Service |
| Ledger balance matches Stripe balance | Daily reconciliation report |
| Payout period closed | Finance cutoff confirmed |

---

## Workflow

### Path A — Standard scheduled payout

1. Payment Service aggregates captured payments minus refunds and platform fees for the payout period.
2. Hold Manager evaluates active holds (dispute, compliance, fraud) — skip or reduce eligible amount.
3. Payout Engine creates Stripe transfer to creator Connect account with idempotency key = `creator_id` + period.
4. On `payout.completed` webhook: Notification Service sends creator payout confirmation email.
5. Finance reconciles transfer ID against daily settlement report.

### Path B — Payout hold (dispute or compliance)

1. Trust Operator or system places hold with reason code and linked case ID.
2. Creator dashboard shows hold status and next review date — no specific dispute details to creator during active investigation.
3. Support uses macro **Payout hold — under review** for inquiries.
4. On case resolution: Supervisor releases hold or converts to clawback per [Refund Processing SOP](refund-processing-sop.md).
5. Audit: `{ operator_id, creator_id, hold_reason, case_id, action, timestamp }`.

### Path C — Missing payout investigation (Support → Ops)

1. Support confirms: order completed, refund window passed, Connect onboarding complete.
2. Support escalates to Finance if payout age exceeds **2× documented SLA** — [Escalation Guide](../support/escalation-guide.md).
3. Finance traces: ledger → Stripe transfer → bank deposit timeline.
4. Outcomes: retry transfer, explain Stripe delay, identify hold reason, or open fraud case.
5. Support responds with precise dates — [Voice and Tone — Precise timing](../brand/voice-and-tone.md#3-precise).

### Path D — Clawback after refund or fraud

1. Refund or fraud finding reduces creator balance after transfer already sent.
2. Finance applies negative balance on next payout cycle or initiates Stripe reversal where supported.
3. Trust documents clawback rationale on [Creator Admin Detail](../pages/admin/creator-admin-detail.md).
4. Creator notified with amount, reason, and next payout expectation.
5. Persistent negative balance → Creator Success outreach before suspension review.

### Path E — Failed transfer retry

| Failure type | Action |
|--------------|--------|
| Stripe API timeout | Retry with same idempotency key (3 attempts) |
| Invalid bank account | Notify creator via dashboard + email; block until updated |
| Connect account restricted | Escalate Trust + Finance; may require suspension |
| Persistent failure | Finance manual intervention; case note with Stripe support ticket |

---

## AI Responsibilities

| System | Role | Autonomous? |
|--------|------|-------------|
| Payment Service hold rules | Auto-hold on dispute open, compliance expiry | Yes — holds only, never release |
| Risk scoring | Flag anomalous payout patterns | Alert only — human review |
| Support Assist | Retrieve payout status macros | Suggest only |

**Never autonomously:** release holds, waive clawbacks, or modify payout amounts.

---

## Human Responsibilities

| Action | Owner |
|--------|-------|
| Hold release after dispute resolution | Trust Supervisor |
| Fraud payout freeze | Fraud Investigation Lead |
| Clawback approval above limit | Senior Trust + Finance |
| Manual payout exception | Finance + Trust Lead dual approval |
| Creator escalation response | Support → Finance handoff |

---

## Escalation Rules

| Condition | Escalate to | Timeline |
|-----------|-------------|----------|
| Payout missing > 2× SLA | Finance | Same business day |
| Suspected payout fraud | Fraud Investigation SOP | 4 hours |
| Stripe Connect account takeover | Engineering + Trust | 1 hour |
| Creator threatening legal action over hold | Trust Lead + Legal | Same day |
| Reconciliation mismatch > $500 | Finance + Engineering | Immediate |

---

## SLA

| Stage | Target |
|-------|--------|
| Support acknowledgment of payout inquiry | 4 business hours |
| Finance trace initiated after escalation | 1 business day |
| Hold review (dispute-linked) | Per [Dispute Resolution SOP](dispute-resolution-sop.md) |
| Standard payout delivery post-period close | `TODO(decision):` Document in Platform Settings |
| Failed transfer first retry | 4 hours |

---

## Audit Logging

| Event | Required fields |
|-------|-----------------|
| `payout.transfer_initiated` | creator_id, amount_cents, period, stripe_transfer_id, idempotency_key |
| `payout.hold_applied` | creator_id, reason_code, case_id, operator_id |
| `payout.hold_released` | creator_id, case_id, operator_id, rationale |
| `payout.clawback_applied` | creator_id, amount_cents, linked_refund_id, operator_id |

Retention: 7 years — [Data Protection](../engineering/data-protection.md).

---

## Resolution

Case closes when: transfer confirmed, hold released with creator notified, or clawback applied and documented.

---

## Post Mortem

Required when: systemic payout failure (>5 creators), reconciliation mismatch, or fraud clawback exceeding `TODO(decision):` threshold.

---

## Metrics

| Metric | Definition | Owner |
|--------|------------|-------|
| Payout success rate | Successful transfers / attempted | Finance |
| Payout SLA adherence | On-time / total eligible | Finance |
| Active payout holds | Count by reason | Trust |
| Clawback rate | Clawback volume / GMV | Finance |

→ [Metrics Definitions — Creator metrics](../analytics/metrics-definitions.md)

---

## Future Automation

- Automated hold release when dispute resolves with no refund
- Creator self-service payout schedule visibility
- Proactive notification before compliance-driven hold

---

## Related Documents

- [Payment Service](../engineering/services/payment-service.md)
- [Refund Processing SOP](refund-processing-sop.md)
- [Fraud Investigation SOP](fraud-investigation-sop.md)
- [Creator Agreement — Payouts](../legal/creator-agreement.md)
- [Escalation Guide](../support/escalation-guide.md)
