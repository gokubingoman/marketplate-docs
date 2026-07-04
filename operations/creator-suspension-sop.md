# Creator Suspension SOP

> Standard Operating Procedure for creator suspension, restriction, removal, and appeals. **Human approval required; AI flags only.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook companion:** [Creator Suspension & Offboarding](../docs/playbooks/creator-suspension-offboarding.md) *(orchestration)*

---

## Purpose

This SOP defines Trust & Safety procedures for progressive enforcement against creator accounts — from warnings through permanent removal — and for processing appeals and reinstatement. It implements the [Trust enforcement ladder](../product/marketplace-mechanics.md#trust-enforcement-ladder):

```
Education → Warning → Listing restriction → Order suspension → Account suspension → Permanent removal
```

This SOP is the **operator execution layer** for the [Creator Suspension playbook](../docs/playbooks/creator-suspension-offboarding.md). [Moderation Assist](../ai/moderation-assist.md) and [Verification Assist](../ai/verification-assist.md) may flag accounts; **humans enforce** with documented rationale and immutable audit per [Trust Service — Security](../engineering/services/trust-service.md#security).

---

## Trigger

| Trigger | Source | Typical enforcement level |
|---------|--------|---------------------------|
| Moderation decision — pattern of violations | [Moderation SOP](moderation-sop.md) | Warning → suspension |
| Food safety incident conclusion | [Food Safety Incident SOP](food-safety-incident-sop.md) | Account suspension → removal |
| Fraud confirmation | [Fraud Response](../docs/playbooks/fraud-response.md) | Permanent removal |
| Compliance expiry post-grace | Compliance Engine (`compliance.expired`) | Listing restriction → order suspension |
| Dispute pattern (≥ 3 / 30 days) | Trust risk scoring | Account review |
| Verification fraud discovery | [Verification Review SOP](verification-review-sop.md) | Hold → suspension |
| Legal/regulatory order | Legal | Per counsel direction |
| Voluntary creator closure | Creator request | Offboarding Track B — playbook |
| Trust Supervisor escalation | Manual | Per ladder assessment |

**Automatic system actions (not human suspension):** Post-grace compliance expiry suspends **listings** via Catalog — operator may escalate to full account suspension if creator attempts circumvention.

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Trust Supervisor** | Approve suspension/removal; active order decisions |
| **Trust Operator** | Case documentation, customer order review |
| **Trust Lead** | Permanent removal, appeal decisions, reinstatement |
| **Legal Counsel** | Regulatory orders, appeal liability, fraud holds |
| **Finance** | Payout holds, final payout, clawback |
| **Customer Support** | Customer notifications, refund execution |
| **Engineering On-Call** | Verify `creator.suspended` propagation |

**Separation rule:** Creator Success does **not** communicate enforcement actions — Trust & Safety owns all suspension/removal messaging.

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Rationale min 20 chars enforced | Trust Service API |
| Reason codes configured | `policy_violation`, `fraud_suspected`, `food_safety`, `compliance_expired`, etc. |
| Senior role for suspension/removal | RBAC |
| Dual approval for permanent removal | Two senior approvers logged |
| [Creator Admin Detail](../pages/admin/creator-admin-detail.md) access | Enforcement tab + order list |
| Payout hold capability | Payment Service |
| Appeal Help article published | Creator-facing |
| Specialized playbook invoked if P0 | Food Safety / Fraud complete or in parallel |

---

## Workflow

### Track A — Involuntary enforcement

#### Step A1 — Case preparation

1. Open [Creator Admin Detail](../pages/admin/creator-admin-detail.md) — review enforcement tab, verification history, disputes, moderation, AI flags.
2. Confirm current ladder position — apply **lowest effective level** unless severity demands escalation.
3. Identify active orders and pending payouts (Order Service + Payment Service).
4. For P0 safety or confirmed fraud: ensure [Food Safety Incident](../docs/playbooks/food-safety-incident.md) or [Fraud Response](../docs/playbooks/fraud-response.md) playbook invoked first.
5. Trust Supervisor **approves enforcement level and rationale before action** — human approval gate.

#### Step A2 — Execute enforcement

| Level | Creator impact | Trust Service event |
|-------|----------------|---------------------|
| Education | In-app notice | Internal log + notification |
| Warning | Documented on enforcement tab | `moderation.decided` |
| Listing restriction | Affected listings hidden | `moderation.decided` → Catalog |
| Order suspension | Cannot accept new orders | `creator.suspended` (partial) |
| Account suspension | Listings hidden; orders blocked | `creator.suspended` |
| Permanent removal | Account deactivated | `creator.suspended` + deactivate |

Execution:

1. Trust Supervisor submits action with reason code + rationale via admin API / [Creator Admin Detail](../pages/admin/creator-admin-detail.md) quick actions.
2. System emits events — Engineering verifies Catalog, Order, Payment, Discovery consumers.
3. Audit entry written — **blocks on audit failure**.

#### Step A3 — Active order handling (human decision matrix)

| Scenario | Action | Refund |
|----------|--------|--------|
| Safety suspension (P0/P1) | Force-cancel all active orders | Full — [Refund Processing SOP](refund-processing-sop.md) |
| Fraud confirmed | Force-cancel all | Full refund |
| Compliance expiry | Allow fulfill existing; block new | N/A for existing |
| Policy suspension — safely fulfillable | Creator completes OR platform cancels | Per Supervisor decision |
| Open dispute on order | Resolve dispute first | Per [Dispute Resolution SOP](dispute-resolution-sop.md) |

Support notifies affected customers within **4 hours** of suspension.

#### Step A4 — Creator and customer notification

1. Trust & Safety sends enforcement email + in-app notice — templates in [playbook](../docs/playbooks/creator-suspension-offboarding.md#communication-templates).
2. Include case ID and appeal instructions if eligible.
3. Finance applies payout hold pending investigation outcome.

#### Step A5 — Appeals (if eligible)

| Step | Actor | Action |
|------|-------|--------|
| A5.1 | Creator | Submits appeal via Help with case ID within **14 days** |
| A5.2 | Support | Triage to Trust queue — not Creator Success |
| A5.3 | Trust Operator | Independent reviewer (not original decider if possible) |
| A5.4 | Trust Lead | Decision: uphold · reinstate · modify enforcement |
| A5.5 | Trust & Safety | Notify creator of outcome |
| A5.6 | System | If reinstated: emit `creator.reinstated` |

**Non-appealable:** Confirmed fraudulent identity; permanent removal with Legal hold.

Appeal standards: [Trust & Safety Standards — Appeals](../docs/standards/trust-and-safety-standards.md#appeals) — 5 business days decision SLA.

#### Step A6 — Reinstatement (if approved)

1. Trust Lead defines conditions: re-verification, compliance renewal, listing corrections.
2. Creator completes remediation.
3. Trust Operator verifies — may re-run [Verification Review SOP](verification-review-sop.md) checklists.
4. Trust Supervisor approves reinstatement with rationale.
5. System: `creator.reinstated` → Catalog restores eligible listings.
6. Finance releases payout hold per policy.
7. Creator Success **may** engage post-reinstatement for activation — Trust Lead approves.

**Reinstatement blocked:** Permanent removal for fraud; unaddressed food safety root cause; active legal prohibition.

### Track B — Voluntary offboarding (summary)

Full detail: [Creator Suspension playbook — Track B](../docs/playbooks/creator-suspension-offboarding.md#track-b--voluntary-offboarding).

1. Creator requests closure — Creator Success confirms intent and alternatives.
2. Complete or cancel active orders; block new orders.
3. Finance processes final payout after dispute window.
4. Trust Operator deactivates account — not "permanent removal" unless requested.
5. Creator Success sends offboarding confirmation — reactivation path preserved.

Voluntary offboarding: no enforcement stigma; Creator Success owns comms.

---

## AI Responsibilities

AI systems **flag only** — never suspend or remove:

| System | Role |
|--------|------|
| [Moderation Assist](../ai/moderation-assist.md) | Policy scores, severity — moderator applies ladder via [Moderation SOP](moderation-sop.md) |
| [Verification Assist](../ai/verification-assist.md) | Fraud flags — Supervisor review |
| Risk scoring | Elevated scrutiny routing — no auto-suspend |
| Compliance Engine | Post-grace listing suspension — system restriction, not full account |
| Auto account suspension | **Never** |
| Auto permanent removal | **Never** |
| Appeal decision | **Never** |

Monitor: zero-tolerance alert on any code path attempting auto-enforcement per [Moderation Assist — Monitoring](../ai/moderation-assist.md#monitoring).

---

## Human Responsibilities

| Action | Human requirement |
|--------|-------------------|
| Enforcement level selection | Trust Supervisor |
| Suspension/removal execution | Trust Supervisor (Senior role) |
| Permanent removal | Senior + **dual approval** |
| Active order force-cancel | Trust Supervisor / IC (safety) |
| Payout hold/release | Finance + Trust Lead |
| Appeal review | Independent Trust Operator |
| Appeal decision | Trust Lead |
| Reinstatement approval | Trust Supervisor + Trust Lead conditions |
| Enforcement comms to creator | Trust & Safety only |
| Voluntary offboarding comms | Creator Success |
| Customer refund authorization | Per [Refund Processing SOP](refund-processing-sop.md) |

Rationale required on **all** enforcement actions — minimum 20 characters, creator-visible category + internal detail.

---

## Escalation Rules

| Condition | Escalate to |
|-----------|-------------|
| P0 food safety — pre-suspension | [Food Safety Incident SOP](food-safety-incident-sop.md) IC |
| Confirmed fraud | [Fraud Response](../docs/playbooks/fraud-response.md) + Trust Lead |
| Permanent removal consideration | Trust Lead + Legal |
| Public creator dispute (social media) | Trust Lead + Comms — [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Wrong creator suspended | Trust Lead — immediate retro |
| Payout hold exceeds policy duration | Finance + Trust Lead |
| `creator.suspended` propagation failure | Engineering on-call P1 |
| Appeal involves Legal hold | Legal |
| Regulatory/court order | Legal directs enforcement level |

---

## SLA

| Milestone | Target |
|-----------|--------|
| Customer notification post-suspension | ≤ 4 hours |
| Active order handling (force-cancel) | ≤ 4 hours (safety/fraud) |
| Creator enforcement notification | ≤ 24 hours of action |
| Appeal acknowledgment | ≤ 2 business days |
| Appeal decision | ≤ 5 business days (standard); ≤ 10 business days (complex) |
| Reinstatement review after remediation | ≤ 3 business days |
| Payout hold resolution | Per Finance policy — escalate if > 30 days |
| Documented rationale on enforcement | 100% — immediate |

Compliance expiry listing suspension: automatic at grace end — creator notification via Compliance Engine reminders at 60/30/0 days.

---

## Audit Logging

| Event | Required fields |
|-------|-----------------|
| `creator.suspended` | `operator_id`, `creator_id`, `level`, `reason_code`, `rationale`, `case_id`, `active_orders_handled`, `timestamp` |
| `creator.reinstated` | `approver_id`, `creator_id`, `conditions[]`, `rationale`, `timestamp` |
| `moderation.decided` (restriction/warning) | Full moderation audit |
| `enforcement.appeal_opened` | `creator_id`, `case_id`, `original_action` |
| `enforcement.appeal_decided` | `reviewer_id`, `decision`, `rationale` |
| `payout.hold_applied` / `released` | `finance_id`, `creator_id`, `amount`, `case_id` |
| Permanent removal dual approval | `approver_id_1`, `approver_id_2`, `timestamp` |

All entries immutable via [Trust Service — Audit Writer](../engineering/services/trust-service.md). Visible on [Creator Admin Detail](../pages/admin/creator-admin-detail.md) enforcement tab.

Audit write failure **blocks** enforcement action — transaction rollback.

---

## Resolution

Enforcement case **resolved** when:

| Track | Resolution state |
|-------|------------------|
| Warning/restriction | Action logged; creator notified; remediation deadline set if applicable |
| Suspension | Creator suspended; orders handled; payout hold applied; appeal window open |
| Permanent removal | Account deactivated; final payouts/clawbacks settled; appeal if eligible |
| Appeal upheld | Original enforcement stands — documented |
| Appeal granted | Modified or reversed — `creator.reinstated` if applicable |
| Voluntary offboarding | Account deactivated; final payout scheduled; confirmation sent |

Open items block resolution: unhandled active orders (safety/fraud), pending refund failures, undisclosed payout hold without documented reason.

---

## Post Mortem

Required when:

- Suspension overturned on appeal with customer harm
- Wrong creator suspended (identity mix-up)
- High-profile creator — public dispute
- Payout hold exceeded policy without resolution
- System failed to propagate `creator.suspended`
- Customer refunds incomplete after involuntary suspension

**Outputs:** Process fix, Trust Service monitoring alert, template update, operator training, playbook amendment.

Schedule within 5 business days — Trust Lead owns.

---

## Metrics

| Metric | Target |
|--------|--------|
| Enforcement with documented rationale | 100% |
| Customer notification SLA post-suspension | ≤ 4 hours |
| Appeal response time | ≤ 5 business days |
| Appeal overturn rate | Monitor — calibration signal |
| Reinstatement rate | Track — quality over volume |
| Repeat enforcement (90d post-reinstate) | ↓ |
| Voluntary offboarding completion | ≤ 14 days to final payout |
| Customer refund completion (involuntary) | 100% |
| Auto-enforcement attempts | **Zero** |

→ [Success Metrics — Trust](../product/success-metrics-overview.md#trust-metrics)

---

## Future Automation

| Initiative | Human gate preserved |
|------------|---------------------|
| Enforcement ladder position dashboard on Creator Admin | Visibility only |
| Active order summary auto-populated on suspend modal | Supervisor decides handling |
| Appeal queue with independent assignment | Human reviewer decides |
| Payout hold auto-apply on suspension | Hold yes — release human |
| Reinstatement checklist tracking | Supervisor approves reinstate |
| Compliance expiry reminders to creators | System restriction only post-grace |

**Never automate:** Suspension, removal, reinstatement, appeal decisions, or enforcement comms.

---

## Related Documents

- [Creator Suspension & Offboarding playbook](../docs/playbooks/creator-suspension-offboarding.md)
- [Moderation SOP](moderation-sop.md)
- [Food Safety Incident SOP](food-safety-incident-sop.md)
- [Verification Review SOP](verification-review-sop.md)
- [Refund Processing SOP](refund-processing-sop.md)
- [Dispute Resolution SOP](dispute-resolution-sop.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Creator Admin Detail](../pages/admin/creator-admin-detail.md)
- [Moderation Assist](../ai/moderation-assist.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
- [Marketplace Mechanics — Trust enforcement ladder](../product/marketplace-mechanics.md#trust-enforcement-ladder)
- [Fraud Response](../docs/playbooks/fraud-response.md)
- [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md)
