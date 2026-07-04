# Content Moderation SOP

> Standard Operating Procedure for content moderation and progressive enforcement. **AI recommends; moderators decide.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook companion:** [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md) · [Creator Suspension & Offboarding](../docs/playbooks/creator-suspension-offboarding.md)

---

## Purpose

This SOP defines how Trust & Safety moderators investigate flagged content and apply enforcement actions through the [Moderation Queue](../pages/admin/moderation-queue.md). It implements the [Trust enforcement ladder](../product/marketplace-mechanics.md#trust-enforcement-ladder):

```
Education → Warning → Listing restriction → Order suspension → Account suspension → Permanent removal
```

[Moderation Assist](../ai/moderation-assist.md) triages and classifies content; **humans are the sole enforcement authority**. No pay-to-remove reviews — invariant enforced at API layer per [Trust Service](../engineering/services/trust-service.md#security).

---

## Trigger

| Trigger | Content type | Default severity |
|---------|--------------|------------------|
| Listing publish or edit to flagged fields | Listing / menu item | MEDIUM |
| Publish-time scan ≥ 0.85 prohibited item score | Listing | HIGH — hold for review |
| Review post-submit fraud flag | Review | MEDIUM–HIGH |
| User report (in-product) | Any UGC type | Per reporter category |
| Message toxicity flag | Message thread excerpt | HIGH if threat |
| Storefront photo/story flag | Storefront content | MEDIUM |
| `catalog.item.flagged` event | Listing | Per AI score |
| Moderation Assist spam cluster detection | Reviews (batch) | MEDIUM — batch human review |
| Escalation from dispute or verification | Cross-case | Per source |

All flagged items create moderation case records in [Trust Service — Moderation Engine](../engineering/services/trust-service.md#architecture).

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Trust & Safety Moderator** | Triage, investigate, dismiss/warn/remove |
| **Senior Trust & Safety** | Account suspension, permanent removal, dual approval |
| **Trust Lead** | Policy edge cases, appeal decisions, ladder calibration |
| **Legal** | Escalated items — regulatory, defamation, law enforcement |

**Accountable team:** Trust & Safety  
**System of record:** Trust Service moderation schema + immutable audit log

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Moderator or Senior T&S role | RBAC — suspend requires senior |
| Access to [Moderation Queue](../pages/admin/moderation-queue.md) | `/admin/moderation` |
| Policy snippets loaded | `/api/v1/admin/moderation/policies` |
| [Moderation Assist](../ai/moderation-assist.md) operational or fallback understood | Async/sync pipeline health |
| Familiarity with enforcement ladder | [Trust & Safety Standards — Enforcement Ladder](../docs/standards/trust-and-safety-standards.md#enforcement-ladder) |
| Sensitive content protocol | Blur-until-reveal; view events audited |

Creator Success has **no** moderation queue access by default.

---

## Workflow

### Step 1 — Triage

1. Open [Moderation Queue](../pages/admin/moderation-queue.md); default sort: severity (HIGH first), then AI priority score.
2. Review SLA badge — HIGH severity: 4h first action per [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md#moderator-slas).
3. Open item; content blurred until "Show content" clicked — view logged.
4. Read [Moderation Assist](../ai/moderation-assist.md) panel: policy match scores, suggested categories, severity recommendation, confidence, content summary.
5. Pull context: reporter credibility, subject account history on [Creator Admin Detail](../pages/admin/creator-admin-detail.md), order linkage if applicable.

### Step 2 — Investigate

1. Read full content (review text, listing, message excerpt, images).
2. Verify AI evidence spans — AI shows "policy match," not "violation certainty."
3. Check enforcement history — determine current ladder position.
4. For food-safety flags (undeclared allergen, prohibited category): cross-reference listing allergens vs. jurisdiction rules.
5. For review integrity: confirm verified-purchase flag; check spam cluster ID for related cases.
6. Link to [Dispute Detail](../pages/admin/dispute-detail.md) if order dispute open.

### Step 3 — Select enforcement action (human approval gate)

Moderator **explicitly selects** action — AI does not pre-select:

| Action | Ladder step | Requirements |
|--------|-------------|--------------|
| **Dismiss** | N/A — false positive | Brief internal note |
| **Education** | First-time minor issue | In-app notice; no functional block |
| **Warn creator** | Warning | Policy category + editable template + rationale |
| **Remove content** | Content action | Rationale required; notify affected parties |
| **Restrict listings** | Listing restriction | Specify affected items; remediation steps |
| **Suspend account** | Order/account suspension | **Senior role** + confirmation modal + duration |
| **Permanent removal** | Terminal | **Senior + dual approval** + Legal consult if warranted |
| **Escalate** | Handoff | Assign senior/legal; status `escalated` |

**Enforcement selection rules:**

- Apply **lowest effective ladder step** — escalate only if insufficient or repeat offense
- Rationale required for all non-dismiss actions (min 20 chars)
- Suspend never automatic regardless of AI score
- Permanent removal never from junior moderator

### Step 4 — Submit decision

1. Enter rationale (internal + creator-visible where applicable).
2. Confirm modal for suspend/removal.
3. Submit via `/api/v1/admin/moderation/items/:id/decide`.
4. Trust Service emits `moderation.decided` → Notification Service, Catalog updates.
5. Row removed from open queue; audit entry written.

### Step 5 — Follow-up

| Action taken | Follow-up |
|--------------|-----------|
| Remove review | Creator may respond per policy — no pay-to-remove |
| Listing restriction | Creator notified with remediation steps |
| Suspend | Invoke [Creator Suspension SOP](creator-suspension-sop.md) for active order handling |
| Food safety HIGH | Invoke [Food Safety Incident SOP](food-safety-incident-sop.md) if illness/allergen exposure |
| Fraud signal | Open [Fraud Response](../docs/playbooks/fraud-response.md) |

---

## AI Responsibilities

[Moderation Assist](../ai/moderation-assist.md) — assist only:

| Function | Autonomous? |
|----------|-------------|
| Policy violation scoring (0.0–1.0) | Yes — recommendation |
| Suggested policy categories with evidence spans | Yes |
| Severity recommendation (low/medium/high) | Yes |
| Priority score for queue sort | Yes |
| Content summary (internal) | Yes |
| Spam/duplicate cluster linking | Yes |
| Publish-time listing hold (≥ 0.85 prohibited) | Yes — **hold only**, not reject |
| Dismiss / warn / remove / suspend | **Never** |
| Advance enforcement ladder | **Never** |
| Permanent deletion | **Never** |

Sync listing scan target: < 2s. Async for reviews/messages.

**Explicit prohibition:** No threshold configuration enables autonomous suspension, removal, or account action per [Moderation Assist — Confidence thresholds](../ai/moderation-assist.md#confidence-thresholds).

---

## Human Responsibilities

| Action | Human requirement |
|--------|-------------------|
| All enforcement decisions | Moderator selects action explicitly |
| Policy category selection | Moderator confirms or overrides AI suggestion |
| Severity override | Moderator may upgrade/downgrade with note |
| Suspend account | Senior role + modal confirmation |
| Permanent removal | Senior + dual approval |
| Escalate to legal | Moderator action |
| Dismiss high-score AI case | Moderator confirms false positive — feeds eval |
| Food safety escalation | Human judgment — do not dismiss HIGH allergen flags without investigation |
| Batch spam cluster dismiss | Human batch confirm — not auto |

Moderators judge **policy violations**, not food quality. Verified-purchase context required for review cases.

---

## Escalation Rules

| Condition | Escalate to | Timeline |
|-----------|-------------|----------|
| HIGH severity unactioned approaching SLA | Senior moderator | Before 4h breach |
| Threat, harassment with doxxing | Senior + Legal | Immediate |
| Confirmed allergen mislabeling in listing | [Food Safety Incident SOP](food-safety-incident-sop.md) | Immediate |
| Suspected identity fraud in content | [Verification Queue](../pages/admin/verification-queue.md) + Fraud playbook | Same day |
| Public figure / media attention | Trust Lead + Comms | Per [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Moderator wellbeing — graphic content | Supervisor for reassignment | As needed |
| Policy gap — no matching category | Trust Lead + Product | Document decision |
| Appeal on moderation decision | Independent moderator | 5 business days |

Escalation path: Moderator → Senior T&S → Trust Lead → Legal/Executive.

---

## SLA

Per [Trust & Safety Standards — Moderator SLAs](../docs/standards/trust-and-safety-standards.md#moderator-slas) (configurable in [Platform Settings](../pages/admin/platform-settings.md)):

| Severity | First action SLA | Resolution target |
|----------|------------------|-------------------|
| HIGH | 4 hours | Same business day |
| MEDIUM | 24 hours | 2 business days |
| LOW | 72 hours | 5 business days (batch allowed) |

**Clock starts:** Case creation timestamp.  
**Publish-time holds:** Creator sees "pending review" until moderator decides — not auto-reject.

Backlog alert: > 50 open items → Supervisor staffing review per [Trust Service — Monitoring](../engineering/services/trust-service.md#monitoring).

---

## Audit Logging

Every decision emits immutable audit via [Trust Service — Audit Writer](../engineering/services/trust-service.md):

| Event | Required fields |
|-------|-----------------|
| `moderation.decided` | `operator_id`, `case_id`, `entity_type`, `entity_id`, `action`, `policy_ids[]`, `rationale`, `ai_score_at_decision`, `severity`, `before_state`, `after_state`, `timestamp` |
| `moderation.escalated` | `operator_id`, `case_id`, `escalated_to`, `reason` |
| `moderation.content_view` | `operator_id`, `case_id` — sensitive content access |
| `moderation.dismiss` | `operator_id`, `case_id`, `ai_score`, `dismiss_note` |

Dual approval for permanent removal: both `approver_id` values logged.

Customer/creator notifications logged with template ID and delivery status. Audit write failure **blocks** mutating action.

---

## Resolution

Case **resolved** when moderator submits decision and `moderation.decided` event propagates:

| Outcome | Case status | Platform effect |
|---------|-------------|-----------------|
| Dismiss | `closed` — false positive | Content restored if held |
| Warn / education | `closed` | Enforcement tab updated on creator profile |
| Remove content | `closed` | Content hidden; parties notified |
| Restrict / suspend | `closed` | Catalog/Order/Payment consumers process events |
| Escalate | `escalated` | Assigned reviewer continues |

Appeal window: 14 days for enforcement actions per [Trust & Safety Standards — Appeals](../docs/standards/trust-and-safety-standards.md#appeals).

---

## Post Mortem

Required when:

- Wrong content removed — restored on appeal
- Creator suspended for platform bug (wrong allergen displayed)
- HIGH severity item breached SLA with customer harm
- Inter-moderator agreement sample below threshold
- Auto-enforcement code path detected (zero tolerance alert)

**Agenda (60 min, within 5 business days):**

1. Timeline and enforcement ladder position at time of action
2. AI assist accuracy — override or miss
3. Customer/creator impact
4. Root cause: policy, training, tooling, staffing
5. Action items: eval set, policy snippet, template, threshold tuning

Update this SOP or [Moderation Assist](../ai/moderation-assist.md) eval requirements as needed.

---

## Metrics

| Metric | Definition | Target |
|--------|------------|--------|
| Moderation SLA adherence | First action within SLA / total by severity | ≥ 95% HIGH |
| Queue depth | Open items | ↓ — alert > 50 |
| Override rate on AI category | Moderator changed suggested category | Monitor weekly |
| HIGH severity dismiss rate | Dismissed HIGH / total HIGH | Daily review — tune thresholds |
| Appeal overturn rate | Upheld appeals / total appeals | Monitor calibration |
| Time-to-decision vs. AI score decile | Efficiency | Bi-weekly |
| Inter-moderator agreement | Monthly sample | ↑ |
| Repeat enforcement (90d) | Same creator same policy | ↓ |
| Auto-enforcement attempts | Must be zero | **Zero tolerance** |

→ [Success Metrics — Trust](../product/success-metrics-overview.md#trust-metrics) · [Moderation Queue analytics](../pages/admin/moderation-queue.md#analytics)

---

## Future Automation

| Initiative | Human gate preserved |
|------------|---------------------|
| Appeals queue linked to moderation decisions | Human appeal reviewer |
| Image region overlays for policy violations | Moderator confirms |
| Moderator specialization routing (food safety vs. harassment) | Human decides |
| Bulk dismiss spam clusters | Human batch confirm with batch audit ID |
| SLA auto-escalation for unactioned HIGH items | Escalates to human — no auto-action |
| In-product report categories aligned with AI taxonomy | Reduces mismatch only |

**Never automate:** Suspension, removal, permanent deletion, or ladder advancement.

---

## Related Documents

- [Moderation Queue](../pages/admin/moderation-queue.md)
- [Moderation Assist](../ai/moderation-assist.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
- [Marketplace Mechanics — Trust enforcement ladder](../product/marketplace-mechanics.md#trust-enforcement-ladder)
- [Creator Suspension SOP](creator-suspension-sop.md)
- [Food Safety Incident SOP](food-safety-incident-sop.md)
- [Dispute Detail](../pages/admin/dispute-detail.md)
- [Platform Settings](../pages/admin/platform-settings.md)
