# Verification Review SOP

> Standard Operating Procedure for identity, kitchen, and compliance verification review. **AI recommends; operators approve.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook companion:** [Launching a Creator](../docs/playbooks/launching-a-creator.md) · [Trust Verification Flow](../pages/flows/trust-verification-flow.md)

---

## Purpose

This SOP defines how Trust & Safety operators review creator verification submissions — identity, kitchen, and compliance — in the [Verification Queue](../pages/admin/verification-queue.md). Verification is a hard gate: unverified creators cannot accept paid orders per [Trust & Safety Standards — Verified to sell](../docs/standards/trust-and-safety-standards.md#platform-invariants).

Every approval, rejection, and request-for-information action requires human judgment, a completed checklist, and an immutable audit record. [Verification Assist](../ai/verification-assist.md) pre-processes documents but **never** changes verification status.

---

## Trigger

| Trigger | Source | Queue item type |
|---------|--------|-----------------|
| Creator submits identity documents | `/creators/me/verification/identity/submit` | Identity |
| Creator submits kitchen verification | `/creators/me/verification/kitchen/submit` | Kitchen |
| Creator uploads compliance document | `/creators/me/compliance/submit` | Compliance |
| Creator resubmits after request info | Resubmission flow | Same type; priority bump |
| Compliance expiry re-verification | Scheduled job + creator upload | Compliance |
| Fraud signal on existing account | Risk scoring / duplicate hash | Identity or compliance |

System flow: submission → [Trust Service](../engineering/services/trust-service.md) creates `VerificationRecord` (`in_review`) → [Verification Assist](../ai/verification-assist.md) async processing → item appears in queue.

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Trust & Safety Operator** | Primary reviewer — claim case, complete checklist, decide |
| **Trust & Safety Supervisor** | Fraud-suspect cases, SLA breach escalation, QA sampling |
| **Trust Lead** | Policy exceptions, jurisdiction template gaps, appeal review |
| **AI Platform** | Pipeline health — not verification decisions |

**Accountable team:** Trust & Safety  
**System of record:** [Trust Service](../engineering/services/trust-service.md) `trust` schema

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Admin MFA enabled | Identity provider check |
| Trust & Safety reviewer role assigned | RBAC in Admin Console |
| Access to [Verification Queue](../pages/admin/verification-queue.md) | `/admin/verification` loads |
| Jurisdiction template loaded for creator's market | [Platform Settings](../pages/admin/platform-settings.md) → Compliance |
| Verification Assist pipeline operational or fallback understood | AI Platform dashboard; fallback = manual review |
| Operator not reviewing own test account | Separation of duties enforced server-side |
| Checklist familiarity per verification type | [Trust Verification Flow — Operator checklists](../pages/flows/trust-verification-flow.md) |

Junior operators cannot approve fraud-suspect (`Fraud suspect` priority) cases — senior reviewer role required per [Verification Assist — Confidence thresholds](../ai/verification-assist.md#confidence-thresholds).

---

## Workflow

### Step 1 — Claim and triage

1. Open [Verification Queue](../pages/admin/verification-queue.md); sort by SLA urgency, then priority (fraud-suspect first).
2. Select item; system marks `in_progress` and applies optimistic lock (`locked_by`).
3. Review header: creator name, verification type, jurisdiction, submission age, SLA badge.
4. Open [Creator Admin Detail](../pages/admin/creator-admin-detail.md) in parallel for prior decisions and enforcement history.

### Step 2 — Review AI assist panel

1. Read [Verification Assist](../ai/verification-assist.md) outputs: extracted fields, quality score, mismatch flags, fraud flags, confidence.
2. If `ai_status: unavailable`, proceed with manual checklist only — do not delay review.
3. Compare extracted fields to self-declared values and documents in preview pane (watermarked with operator ID).
4. For each AI flag: investigate or dismiss with audit note — flags are immutable; dismissal requires rationale.

### Step 3 — Complete type-specific checklist

**Identity**

- Government ID legible, unexpired, matches declared entity type
- Name matches business registration (if applicable)
- Selfie/liveness matches ID (if required)
- Tax identity captured per jurisdiction
- No duplicate document hash across accounts

**Kitchen**

- Kitchen type matches declared persona (cottage, commercial, commissary, mobile)
- Address confirmation matches facility photos and declared location
- Facility photos current: prep, storage, hand-washing visible
- Multi-tenant linkage verified (facility admin approval if applicable)
- Inspection/registration docs valid for jurisdiction

**Compliance**

- Document type matches jurisdiction template requirement
- Certificate/license numbers valid; expiration date captured
- Named individual matches verified identity or registered staff
- Insurance (if required): named insured matches entity, coverage adequate
- Category eligibility confirmed — prohibited items blocked

Checklist reference: [Trust Verification Flow — Phase 4–5](../pages/flows/trust-verification-flow.md#phase-4--case-review).

### Step 4 — Decision (human approval gate)

Choose exactly one outcome:

| Decision | When | Creator-visible message |
|----------|------|-------------------------|
| **Approve** | All checklist items satisfied; fraud flags resolved or dismissed with note | System notification: approved |
| **Request info** | Fixable gaps — blurry scan, missing page, ambiguous address | Specific items listed; status → `needs_information` |
| **Reject** | Failed verification; fraud; ineligible jurisdiction | Reason code + rationale (min 20 chars) |

**Approve blocked if:**

- Required checklist incomplete (server-side validation)
- Unresolved high-severity AI flag without explicit confirmation modal acknowledgment
- Fraud-suspect priority without senior reviewer role

### Step 5 — Post-decision system effects

On **approve**:

1. Trust Service updates `VerificationRecord` → `approved`
2. Emits `verification.approved` → Catalog enables listings; Payment releases holds where applicable
3. Creator cache updated; next verification layer unlocked per [Launching a Creator — Phases 1–3](../docs/playbooks/launching-a-creator.md)
4. Notification Service sends creator email

On **reject** or **request info**:

1. Status updated; creator notified with case ID
2. Resubmission re-enters queue with priority bump

### Step 6 — Internal notes and handoff

1. Add internal notes for ambiguous cases — visible on [Creator Admin Detail](../pages/admin/creator-admin-detail.md).
2. If fraud suspected beyond case scope: open [Fraud Response](../docs/playbooks/fraud-response.md) playbook — do not approve pending investigation.
3. Release lock; select next item or end session.

---

## AI Responsibilities

[Verification Assist](../ai/verification-assist.md) handles **assist only**:

| Function | Autonomous? |
|----------|-------------|
| OCR and field extraction | Yes — output is recommendation |
| Document type classification | Yes |
| Quality scoring | Yes — may warn creator pre-submit |
| Mismatch and fraud flag generation | Yes — flags only |
| Priority routing (Elevated, Fraud suspect) | Yes — metadata only |
| Approve / reject / request info | **Never** |
| Dismiss flags | **Never** — operator dismisses with note |
| Change verification status | **Never** |

Every AI run logs `{ case_id, model_version, latency_ms, flag_count, ai_status }` — no raw document content in logs.

Fallback: AI timeout or outage → case enters queue without pre-fill; operator reviews manually per [Trust Verification Flow — Phase 2](../pages/flows/trust-verification-flow.md#phase-2--ai-pre-processing).

---

## Human Responsibilities

| Action | Human requirement |
|--------|-------------------|
| All verification decisions | Operator completes checklist and submits |
| AI flag dismissal | Operator note in audit — mandatory |
| Approve with unresolved high-severity flags | Senior confirmation modal |
| Fraud-suspect approval | Senior reviewer role only |
| Reject rationale | Creator-visible text + reason code |
| Request info message | Creator-visible; specific and actionable |
| Policy interpretation edge cases | Escalate to Supervisor — do not guess |
| Jurisdiction template gaps | Escalate to Trust Lead + Legal |

Operators are accountable for every decision. AI outputs are advisory — displayed subordinate to checklist and document viewer per [Verification Queue UI contract](../pages/admin/verification-queue.md).

---

## Escalation Rules

| Condition | Escalate to | Action |
|-----------|-------------|--------|
| Fraud flag high severity | Trust Supervisor | Claim immediately; hold approval |
| Duplicate ID across accounts | Trust Supervisor + Fraud playbook | Account hold possible |
| SLA breach imminent (< 4h to breach) | Trust Supervisor | Reassign or assist |
| SLA breached | Trust Lead | Root cause: staffing vs. volume |
| Jurisdiction rule unclear | Trust Lead + Legal | Document `TODO(decision)` if blocked |
| Operator disagreement on approve | Second senior reviewer | Independent review |
| Creator appeals rejection | Independent verifier (not original operator) | See [Trust & Safety Standards — Appeals](../docs/standards/trust-and-safety-standards.md#appeals) |
| AI pipeline fallback rate > 10% / 1 hr | AI Platform on-call | Manual review continues; no SLA waiver |
| Audit write failure | Engineering P1 | **Block mutating action** — transaction rollback |

Escalation path: Operator → Supervisor → Trust Lead → [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md).

---

## SLA

Review SLAs from [Platform Settings](../pages/admin/platform-settings.md) → Trust & Verification (v1 defaults):

| Verification type | First decision SLA | Resubmission SLA |
|-------------------|-------------------|------------------|
| Identity | 2 business days | 1 business day |
| Kitchen | 3 business days | 2 business days |
| Compliance (per batch) | 2 business days | 1 business day |
| Fraud-suspect priority | 4 business hours | 4 business hours |

**Clock starts:** `verification.submitted` event timestamp.  
**Clock pauses:** Status `needs_information` until creator resubmits.

SLA breach triggers dashboard alert on [Admin Dashboard](../pages/admin/admin-dashboard.md) and Supervisor notification.

---

## Audit Logging

Every mutating action writes an immutable [AuditLog](../engineering/data/core-entities.md#auditlog) entry via [Trust Service — Audit Writer](../engineering/services/trust-service.md#architecture). **Audit write failure blocks the action.**

| Event | Required fields |
|-------|-----------------|
| `verification.approved` | `operator_id`, `record_id`, `type`, `creator_id`, `checklist_json`, `before_status`, `after_status`, `ai_flags_dismissed_count`, `timestamp` |
| `verification.rejected` | Above + `reason_code`, `rationale` (creator-visible), `internal_notes` |
| `verification.needs_information` | Above + `creator_message` |
| `ai_flag.dismissed` | `operator_id`, `flag_id`, `dismiss_rationale` |
| `document.preview` / `document.download` | `operator_id`, `doc_id`, `timestamp` |

Log format (application logs):

```
service=trust action=verification.approved actor_id= entity_id= record_id= ai_flags_dismissed=2
```

Audit trail visible on [Creator Admin Detail](../pages/admin/creator-admin-detail.md) verification tab. Retention: immutable; replicated with WORM policy per Trust Service DR.

---

## Resolution

A verification case is **resolved** when:

| Outcome | Resolution state | Creator impact |
|---------|------------------|----------------|
| Approved | `approved` — removed from active queue | Next layer unlocked or Verified Creator status granted |
| Rejected | `rejected` — appeal window opens (14 days) | Cannot proceed; may appeal |
| Request info | `needs_information` — pending creator | Blocked until resubmission |

**Verified Creator** achieved when identity, kitchen, and all required compliance documents are `approved` — triggers [Creator Onboarding Ops SOP](creator-onboarding-ops-sop.md) Phase 4 activation.

Close operator session: confirm item no longer in `in_review` queue; no dangling locks.

---

## Post Mortem

Required when:

- False approval discovered (creator reached verified status incorrectly)
- Fraudulent creator approved despite AI fraud flags
- SLA breach affecting > 10 creators in one week
- Audit gap identified (action without log)
- Customer harm traced to verification failure

**Process (within 5 business days):**

1. Timeline: submission → AI processing → operator actions → downstream impact
2. Root cause: checklist gap, AI miss, operator error, policy ambiguity, tooling failure
3. Corrective actions: checklist update, eval set addition, staffing, template change
4. QA sample expansion for affected verification type
5. Update this SOP, [Trust Verification Flow](../pages/flows/trust-verification-flow.md), or jurisdiction template

Outputs assigned in ops tracker; Trust Lead signs off.

---

## Metrics

| Metric | Definition | Target |
|--------|------------|--------|
| Verification SLA adherence | Decided within SLA / total | ≥ 95% |
| Median queue age | Hours from submit to first decision | ↓ by type |
| False approve rate (QA sample) | Incorrect approvals / sample | ↓ |
| AI flag dismiss rate | Dismissed / total flags | Monitor — tune thresholds |
| Resubmission rate | Resubmit after request info / total | Monitor |
| Appeal overturn rate (verification) | Overturned / appealed | Monitor calibration |
| Time-in-queue vs. AI flag count | Efficiency review | Bi-weekly |
| `ai_flags_dismissed` by type | Weekly tuning input | Stable trend |
| Verification approval rate anomaly | Rubber-stamping detection | Alert on spike |

→ [Success Metrics — Trust](../product/success-metrics-overview.md#trust-metrics) · [Trust Service — Monitoring](../engineering/services/trust-service.md#monitoring)

---

## Future Automation

| Initiative | Human gate preserved |
|------------|---------------------|
| Side-by-side ID vs. selfie comparison UI | Approve still requires checklist |
| Third-party identity provider ingestion (Jumio, Persona) | Operator confirms provider result |
| Queue assignment and workload balancing | No auto-approve |
| Bulk compliance expiration review batch | Human batch confirm per item |
| Pre-submit quality feedback to creators | Reduces low-quality scans |
| Automated jurisdiction rule updates from Legal Ops | Rules affect eligibility; approval human |
| QA sampling workflow for approved items | Human QA review |

**Explicit prohibition:** No roadmap item may enable autonomous verification approval — invariant `verification.human_approval_required: true` at API layer per [Trust Service — Security](../engineering/services/trust-service.md#security).

---

## Related Documents

- [Verification Queue](../pages/admin/verification-queue.md)
- [Trust Verification Flow](../pages/flows/trust-verification-flow.md)
- [Verification Assist](../ai/verification-assist.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
- [Launching a Creator](../docs/playbooks/launching-a-creator.md)
- [Platform Settings](../pages/admin/platform-settings.md)
- [AI Contributor Constitution](../company/ai-contributor-constitution.md)
