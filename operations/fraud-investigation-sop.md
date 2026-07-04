# Fraud Investigation SOP

> Standard Operating Procedure for identity, payment, and payout fraud investigation. **AI flags; humans investigate and enforce.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook companion:** [Fraud Response](../docs/playbooks/fraud-response.md) · [Creator Suspension SOP](creator-suspension-sop.md)

---

## Purpose

This SOP defines Trust & Safety operator procedures for investigating suspected fraud — document manipulation, duplicate identity, stolen payment methods, review fraud, multi-account abuse, and payout fraud. Fraud directly violates the trust thesis; confirmed fraud may result in permanent removal per [Trust enforcement ladder](../product/marketplace-mechanics.md#trust-enforcement-ladder).

[Verification Assist](../ai/verification-assist.md) and Payment Service risk signals **flag only** — operators decide outcomes.

---

## Trigger

| Trigger | Source | Priority |
|---------|--------|----------|
| Verification Assist fraud flag | Tampered document, duplicate hash, font inconsistency | High — 4h SLA |
| Payment fraud alert | Chargebacks, stolen card patterns | High |
| Payout anomaly | Payment Service risk score, negative balance pattern | High |
| Operator suspicion during verification | Manual review | High |
| Customer or creator report | Impersonation, scam listing | Medium |
| Review fraud cluster | [Moderation Assist](../ai/moderation-assist.md) cluster ID | Medium |
| Law enforcement inquiry | Subpoena, referral | P0 |
| Internal QA false approve with fraud characteristics | Audit sampling | High |

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Fraud Investigation Lead** | Case ownership, containment, recommendation |
| **Trust & Safety Supervisor** | Suspension and permanent removal approval |
| **Trust Lead** | Network-level decisions, policy exceptions |
| **Finance** | Chargeback response, payout clawback |
| **Legal Counsel** | Law enforcement, preservation notices |
| **Engineering On-Call** | Account locks, payment blocks |

**War room:** `#incident-fraud` for P0 or active network fraud — see [Fraud Response playbook](../docs/playbooks/fraud-response.md).

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Operator cannot approve own test accounts | RBAC enforced |
| Junior operators cannot close fraud-flag cases | [Access Control](../engineering/access-control.md) |
| Document hash cross-account detection active | Trust Service |
| Audit log export available | Admin Console |
| Fraud reason codes configured | `fraud_suspected` on reject/suspend |

---

## Workflow

### Phase 1 — Triage (0–4 hours)

1. Operator claims case from Verification Queue (`Fraud suspect` priority) or payment alert queue.
2. **Do not approve** pending verification until investigation completes.
3. Gather linked accounts: document hash, IP, device fingerprint, payment method, shared addresses.
4. Classify scope: **single actor**, **linked network**, or **unknown scale**.
5. If ≥3 linked accounts or active orders with stolen payment suspicion → escalate to Supervisor; open war room if P0.

### Phase 2 — Containment

| Finding | Action |
|---------|--------|
| Document manipulation confirmed | Reject verification; suspend if already verified |
| Duplicate identity across accounts | Suspend all linked accounts; preserve evidence |
| Stolen payment method pattern | Block checkout; refund affected customers per [Refund Processing SOP](refund-processing-sop.md) |
| Active fraudulent orders | Force-cancel; full refund; notify customers |
| Payout fraud suspected | Apply payout hold — [Payout Processing SOP](payout-processing-sop.md) Path B |

Document every action on [Creator Admin Detail](../pages/admin/creator-admin-detail.md) with immutable audit entries.

### Phase 3 — Investigation

1. Review Verification Assist flags — dismiss only with written rationale.
2. Compare submitted documents to prior submissions and cross-account hashes.
3. Interview creator only when policy allows — never tip off active network investigations.
4. Coordinate with Finance on chargebacks and clawbacks.
5. Preserve evidence per Legal retention requirements — do not delete documents during open investigation.

### Phase 4 — Resolution

| Outcome | Action |
|---------|--------|
| **False positive** | Clear fraud flag; resume normal verification with supervisor sign-off |
| **Confirmed fraud — first offense (non-safety)** | Reject + suspend; appeal path documented |
| **Confirmed fraud — identity manipulation** | Permanent removal — no reinstatement |
| **Network fraud** | Bulk suspend; Trust Lead approval; postmortem required |
| **Law enforcement** | Legal owns external comms; Trust preserves logs |

Enforcement per [Creator Suspension SOP](creator-suspension-sop.md).

### Phase 5 — Recovery & hardening

1. Postmortem within 5 business days for P0/P1 cases.
2. Feed patterns to AI Platform for model review if fraud evaded detection.
3. Update fraud reason codes or queue routing if systemic gap found.

---

## AI Responsibilities

| System | Role | Autonomous? |
|--------|------|-------------|
| [Verification Assist](../ai/verification-assist.md) | Tamper detection, duplicate hash, priority boost | Flag only |
| Payment risk scoring | Chargeback and velocity alerts | Alert only |
| [Moderation Assist](../ai/moderation-assist.md) | Review fraud clusters | Flag only |

---

## Human Responsibilities

| Action | Owner |
|--------|-------|
| All fraud case decisions | Trust & Safety — Supervisor minimum for confirmed fraud |
| Permanent removal | Trust Lead or Supervisor per ladder |
| Payout hold and clawback | Trust + Finance |
| Law enforcement response | Legal |
| Customer refund authorization | Trust per Refund SOP |

---

## Escalation Rules

| Condition | Escalate to | Timeline |
|-----------|-------------|----------|
| ≥3 linked fraudulent accounts | Trust Lead | 4 hours |
| Active orders with payment fraud | Supervisor + Eng on-call | 1 hour |
| Law enforcement contact | Legal | Immediate |
| Media or social amplification | T&S IC + Comms | 1 hour |
| Verification auto-approve suspected | Eng + Trust | Immediate freeze |

→ [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md)

---

## SLA

| Stage | Target |
|-------|--------|
| Fraud-flag case claimed | 4 hours |
| Containment (active commerce risk) | 1 hour |
| Investigation complete (single actor) | 2 business days |
| Network fraud IC assigned | 15 minutes (P0) |

---

## Audit Logging

Every action requires: `{ operator_id, creator_id(s), action, reason_code, case_id, timestamp, rationale }`.

Evidence exports logged separately with Trust Lead approval.

---

## Resolution

Case closed when: false positive cleared, enforcement executed, refunds initiated, and postmortem scheduled if required.

---

## Post Mortem

Required for: confirmed network fraud, false approve with commerce impact, or evasion of AI detection.

Template: [Incident Response — Postmortem](../engineering/incident-response.md#postmortem-process).

---

## Metrics

| Metric | Definition |
|--------|------------|
| Fraud case volume | New cases / week by type |
| Time to containment | Alert → suspend or hold |
| False positive rate | Cleared / total flagged |
| Repeat fraud attempts blocked | Hash matches prevented |

→ [Trust Metrics](../product/success-metrics-overview.md#trust-metrics)

---

## Future Automation

- Auto-hold checkout on high-confidence payment fraud score (human release required)
- Cross-account graph visualization in admin console
- Automated evidence preservation packages for Legal

---

## Related Documents

- [Fraud Response](../docs/playbooks/fraud-response.md)
- [Verification Review SOP](verification-review-sop.md)
- [Payout Processing SOP](payout-processing-sop.md)
- [Refund Processing SOP](refund-processing-sop.md)
- [Creator Suspension SOP](creator-suspension-sop.md)
- [Trust Service](../engineering/services/trust-service.md)
