# Creator Onboarding Ops SOP

> Standard Operating Procedure for the operations side of the creator activation funnel — signup through first fulfilled order. **Trust gates human-approved; ops monitors and activates.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Creator Operations  
**Playbook companion:** [Launching a Creator](../docs/playbooks/launching-a-creator.md) *(orchestration)*

---

## Purpose

This SOP defines Creator Operations and Trust & Safety procedures for the **supply-side activation funnel**: acquisition → verification → activation → first order. It is the operator execution layer for [Launching a Creator](../docs/playbooks/launching-a-creator.md).

Unverified creators cannot accept paid orders — [Verified to sell](../docs/standards/trust-and-safety-standards.md#platform-invariants). Creator Ops monitors funnel health, intervenes on stalled creators, and coordinates with Trust on verification SLAs. Verification **decisions** follow [Verification Review SOP](verification-review-sop.md) — this SOP covers ops handoffs, nudges, and activation support.

---

## Trigger

| Trigger | Source | Ops action |
|---------|--------|------------|
| Creator completes signup | `/creator/signup` | Funnel tracking begins |
| Identity/kitchen/compliance submitted | Trust Service events | Trust reviews per verification SOP |
| Creator verified (all layers approved) | `verification.approved` (compliance) | Activation outreach |
| Verified + no listing (5 days) | Scheduled job | Creator Success outreach |
| Verified + no order (14 days post-listing) | Funnel alert | Coaching offer |
| Verification SLA breach | Queue alert | Trust Supervisor escalation |
| Creator help ticket during onboarding | Support | Route per topic |
| Referral/partner creator signup | Partner program | Priority handling — `TODO(decision):` |
| First order placed | Order Service | Congratulations lifecycle |
| First order dispute or safety flag | Trust events | Handoff to dispute/safety SOPs |

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Creator Success Lead** | Accountable for time-to-first-order; funnel metrics |
| **Creator Success Specialist** | Stalled creator outreach, activation coaching |
| **Trust & Safety Operator** | Verification review — [Verification Review SOP](verification-review-sop.md) |
| **Trust & Safety Supervisor** | SLA breaches, fraud-flag cases |
| **Marketing** | Acquisition campaigns, welcome sequences |
| **Support** | Creator help tickets during onboarding |

**RACI:** Creator Ops **Accountable** for activation; Trust & Safety **Accountable** for verification decisions; Engineering **Responsible** for system availability.

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Jurisdiction template loaded | [Platform Settings](../pages/admin/platform-settings.md) |
| Trust Service + Verification Assist healthy | [Admin Dashboard](../pages/admin/admin-dashboard.md) queue stats |
| Trust staffing for SLAs | Identity 2 BD, kitchen 3 BD, compliance 2 BD |
| Creator-facing docs live | Chef Welcome Package, onboarding checklist |
| Notification templates configured | Approve/reject/request-info emails |
| Creator Success CRM/lifecycle access | Nudge email capability |
| Verification queue access (Trust only) | [Verification Queue](../pages/admin/verification-queue.md) |

Creator Success does **not** approve verification — view-only queue access if enabled per `TODO(decision)`.

---

## Workflow

### Phase 0 — Signup monitoring (Creator Ops)

| Step | Actor | Action |
|------|-------|--------|
| 0.1 | System | Creator account created; `verification_status: identity_not_started` |
| 0.2 | Creator Ops | Monitor daily: signup → identity submit conversion |
| 0.3 | Creator Ops | If no identity submit within **48h** of signup → automated nudge email |
| 0.4 | Marketing | Attribute acquisition source for funnel reporting |

**Exit:** Identity submission entered Trust queue.

### Phase 1 — Identity verification (Trust & Safety)

| Step | Actor | Action |
|------|-------|--------|
| 1.1 | Creator | Uploads identity documents via `/creator/verify/identity` |
| 1.2 | System | [Verification Assist](../ai/verification-assist.md) processes → [Verification Queue](../pages/admin/verification-queue.md) |
| 1.3 | Trust Operator | Reviews per [Verification Review SOP](verification-review-sop.md) |
| 1.4 | System | On approve: unlock kitchen; notify creator |
| 1.5 | Creator Ops | If stalled **7 days** at identity step → personal outreach (email/call) |

**Human approval gate:** Identity approve/reject/request info — operator only.

**Fraud flag:** Trust Supervisor claims immediately — no junior approval per [Verification Assist](../ai/verification-assist.md#confidence-thresholds).

### Phase 2 — Kitchen verification (Trust & Safety)

| Step | Actor | Action |
|------|-------|--------|
| 2.1 | Creator | Submits kitchen type, address, photos, registration |
| 2.2 | Trust Operator | Reviews per [Verification Review SOP](verification-review-sop.md) — kitchen checklist |
| 2.3 | System | On approve: unlock compliance + paid listing eligibility |
| 2.4 | Creator Ops | Monitor cottage vs. commercial kitchen persona paths |

**Persona variations:** Cottage (home + cottage reg in Phase 3), commercial tenant (facility link), food truck (commissary linkage) — see [Launching a Creator — Phase 2](../docs/playbooks/launching-a-creator.md#phase-2--kitchen-verification).

### Phase 3 — Compliance verification (Trust & Safety)

| Step | Actor | Action |
|------|-------|--------|
| 3.1 | Creator | Uploads jurisdiction-required docs at `/creator/compliance` |
| 3.2 | Trust Operator | Reviews; captures expiration dates per [Verification Review SOP](verification-review-sop.md) |
| 3.3 | System | All required docs approved → **Verified Creator** status |
| 3.4 | Creator Ops | Trigger verified welcome email + first-listing guide |

**Exit:** Verified Creator — all three trust layers approved per [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md).

### Phase 4 — Activation (Creator Ops)

| Step | Actor | Action |
|------|-------|--------|
| 4.1 | Creator | Completes dashboard checklist: profile, story, first listing, availability |
| 4.2 | Creator | Publishes listing — allergens, ingredients, production location required |
| 4.3 | System | Catalog live; Discovery indexed; publish-time [Moderation Assist](../ai/moderation-assist.md) scan |
| 4.4 | Creator Ops | If no listing within **5 days** of verified → personal outreach |
| 4.5 | Creator Ops | If no listing within **14 days** → offer setup call |
| 4.6 | Creator | Configures fulfillment windows/capacity |

**Listing hold:** If moderation AI flags prohibited item — creator sees "pending review" until human moderator decides per [Moderation SOP](moderation-sop.md).

### Phase 5 — First order (Creator Ops + Trust monitor)

| Step | Actor | Action |
|------|-------|--------|
| 5.1 | Customer | Places first order — [Customer Purchase Flow](../pages/flows/customer-purchase-flow.md) |
| 5.2 | Creator | Confirms within 2h SLA; fulfills order |
| 5.3 | Creator Ops | First-order congratulations email + success guide |
| 5.4 | Trust | Monitor disputes/safety flags only — no proactive action |
| 5.5 | Creator Ops | Mark activation complete in funnel metrics |

**Safety trigger:** First order allergen report → [Food Safety Incident SOP](food-safety-incident-sop.md).

---

## AI Responsibilities

| System | Role in onboarding | Autonomous? |
|--------|-------------------|-------------|
| [Verification Assist](../ai/verification-assist.md) | Document extraction, flags, queue priority | Pre-processing only — see Verification SOP |
| [Moderation Assist](../ai/moderation-assist.md) | Listing publish scan | Hold for review — not auto-reject |
| Lifecycle email triggers | System rules (48h nudge, verified welcome) | Automated comms — not verification decisions |
| Discovery ranking | Verified gate hard requirement | Unverified never ranked |
| Auto-approve verification | **Never** |
| Auto-publish held listings | **Never** |

Creator Ops uses funnel dashboards — not AI — to identify stalled creators.

---

## Human Responsibilities

| Action | Owner |
|--------|-------|
| All verification decisions | Trust & Safety — [Verification Review SOP](verification-review-sop.md) |
| Fraud-flag case handling | Trust Supervisor |
| Stalled creator outreach | Creator Success |
| Activation coaching calls | Creator Success |
| Commercial kitchen linkage disputes | Trust Operator — facility admin confirmation |
| First-order dispute/safety | Trust per respective SOPs |
| Policy exceptions (e.g., pre-launch market) | Trust Lead — `TODO(decision):` founder input |
| Jurisdiction template gaps | Trust Lead + Legal |

Creator Success **never** communicates rejection rationale — creators receive Trust notifications with case ID.

---

## Escalation Rules

| Condition | Escalate to | Action |
|-----------|-------------|--------|
| Verification SLA breach | Trust Supervisor | Staffing / reassign |
| SLA breach > 10 creators/week | Trust Lead | Process retro |
| Fraud flag on submission | Trust Supervisor | Immediate |
| Creator stalled 3+ resubmissions | Creator Success + Trust | Guidance review |
| Verified creator — moderation hold > 24h | Moderation Supervisor | Priority review |
| First order safety report | [Food Safety Incident SOP](food-safety-incident-sop.md) | P0/P1 |
| Verification Assist fallback > 10% | AI Platform | Manual review continues |
| Partner/referral creator blocked | Creator Success Lead | Priority Trust review |

Path: Creator Ops → Trust Supervisor → Trust Lead → [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md).

---

## SLA

| Milestone | Target | Owner |
|-----------|--------|-------|
| Signup → identity submit | Monitor; nudge at 48h | Creator Ops |
| Identity review | 2 business days | Trust |
| Kitchen review | 3 business days | Trust |
| Compliance review (per batch) | 2 business days | Trust |
| **Signup → Verified Creator (median)** | ≤ 10 business days | Trust + Creator Ops |
| Verified → first listing | ≤ 5 days median; outreach at 5d | Creator Ops |
| First listing → first order | ≤ 14 days median | Creator Ops |
| First order completion rate | ≥ 95% | Creator Ops |
| Verification SLA compliance | ≥ 95% | Trust |
| Resubmission review | 1–2 BD per type | Trust |

Resubmission gets priority bump in [Verification Queue](../pages/admin/verification-queue.md).

---

## Audit Logging

| Event | Logged by |
|-------|-----------|
| Verification decisions | Trust Service — per [Verification Review SOP](verification-review-sop.md) |
| `verification.approved` / rejected / needs_information | Immutable audit with operator ID |
| Creator Ops outreach | CRM activity log — `creator_id`, `action`, `timestamp` |
| Lifecycle email sends | Notification Service delivery log |
| Activation checklist completion | Creator dashboard events |
| First order milestone | Order Service — `order.completed` |
| Moderation hold on first listing | Moderation audit |

Cross-reference creator journey on [Creator Admin Detail](../pages/admin/creator-admin-detail.md): verification tab + enforcement tab + order history.

---

## Resolution

Onboarding is **resolved** (activation complete) when:

1. Creator achieves Verified Creator status (all trust layers approved)
2. At least one published listing with valid fulfillment configuration
3. First order **completed** (not merely placed)
4. No open verification cases or moderation holds blocking sales
5. Activation checklist marked complete in dashboard

Partial resolution states:

| State | Definition |
|-------|------------|
| **Signed up** | Account created; verification not started |
| **In verification** | One or more layers in review |
| **Verified, pre-activation** | Verified; no published listing |
| **Live, pre-order** | Listing published; no completed order |
| **Activated** | First order completed |

Abandoned leads (no activity 30 days): archive per Creator Ops policy — account retained, no deletion of verification records.

---

## Post Mortem

Required when:

- Fraudulent creator reached verified status
- False approval discovered post-order
- SLA breach affecting > 10 creators in one week
- Creator abandoned after 3+ resubmissions (guidance failure)
- First order cancelled due to platform defect
- Verified creator blocked > 48h by moderation hold on first listing

**Retro focus:** Verification checklist gap, AI flag handling, creator guidance clarity, notification failure, staffing.

Outputs: update [Launching a Creator playbook](../docs/playbooks/launching-a-creator.md), [Verification Review SOP](verification-review-sop.md), or creator-facing docs.

---

## Metrics

| Metric | Target | Owner |
|--------|--------|-------|
| Signup → identity submit (7d) | ↑ | Creator Ops |
| Time to verified (median) | ≤ 10 BD | Trust |
| Verification SLA compliance | ≥ 95% | Trust |
| Verified → first listing (median days) | ≤ 5 | Creator Ops |
| First listing → first order (median days) | ≤ 14 | Creator Ops |
| First order completion rate | ≥ 95% | Creator Ops |
| Verification abandonment by step | ↓ | Product + Creator Ops |
| False approve rate (QA) | ↓ | Trust |
| Outreach response rate | Monitor | Creator Ops |
| AI fallback rate during onboarding | < 10% | AI Platform |

→ [Success Metrics — Creator](../product/success-metrics-overview.md#creator-metrics) · [Trust Metrics](../product/success-metrics-overview.md#trust-metrics)

---

## Future Automation

| Initiative | Human gate preserved |
|------------|---------------------|
| Smart nudge timing based on funnel step | Comms only |
| Creator onboarding health score dashboard | Ops visibility |
| Automated partner/referral routing | Trust still approves |
| Pre-submit document quality feedback | Reduces resubmissions |
| Setup call scheduling integration | Human coaching |
| Bulk compliance expiration outreach | Human review on expiry |
| Queue assignment balancing | Trust operators claim |

**Never automate:** Verification approval, listing publish after moderation hold, or activation status without human-verified trust layers.

---

## Related Documents

- [Launching a Creator playbook](../docs/playbooks/launching-a-creator.md)
- [Verification Review SOP](verification-review-sop.md)
- [Moderation SOP](moderation-sop.md)
- [Creator Onboarding Flow](../pages/flows/creator-onboarding-flow.md)
- [Trust Verification Flow](../pages/flows/trust-verification-flow.md)
- [Verification Queue](../pages/admin/verification-queue.md)
- [Creator Admin Detail](../pages/admin/creator-admin-detail.md)
- [Verification Assist](../ai/verification-assist.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
