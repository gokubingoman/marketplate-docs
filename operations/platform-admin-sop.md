# Platform Admin Operations

> Daily and exceptional workflows for Marketplate internal admin and super-admin tooling.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Platform Operations  
**Template:** [SOP Template](../templates/sop-template.md)

---

## Purpose

Define how platform operators use admin surfaces — dashboard, verification queue, moderation, disputes, creator admin detail, platform settings — safely and consistently. Complements task-specific SOPs; this covers **admin tool discipline** and cross-queue coordination.

---

## Trigger

- Scheduled ops shift start
- SLA breach alert from admin dashboard
- Escalation from support or Trust & Safety
- Platform settings change request

---

## Owner

**Primary:** Platform Operations Lead  
**Backup:** Trust & Safety Lead  
**On-call:** Rotating ops engineer + T&S reviewer

---

## Prerequisites

- MFA-enabled admin account with role-appropriate scopes
- Completed [Trust & Safety onboarding](../docs/training/trust-safety-onboarding.md)
- Access to admin dashboard, audit log viewer, platform settings (settings: senior ops only)

---

## Workflow

### Daily shift open

1. Review [Admin Dashboard](../pages/admin/admin-dashboard.md) — queue depths, SLA breaches, platform health
2. Prioritize: food safety P0 → verification SLA → moderation severity → disputes aging
3. Assign queues if team > 1 person; document handoff in ops channel

### Queue processing

| Queue | SOP | Page spec |
|-------|-----|-----------|
| Verification | [Verification Review](verification-review-sop.md) | [Verification Queue](../pages/admin/verification-queue.md) |
| Moderation | [Moderation](moderation-sop.md) | [Moderation Queue](../pages/admin/moderation-queue.md) |
| Disputes | [Dispute Resolution](dispute-resolution-sop.md) | [Dispute Detail](../pages/admin/dispute-detail.md) |
| Creator actions | [Creator Suspension](creator-suspension-sop.md) | [Creator Admin Detail](../pages/admin/creator-admin-detail.md) |

### Platform settings changes

1. Document rationale in change request (link ADR if architectural)
2. Second approver required for: trust thresholds, SLA targets, feature flags affecting verification
3. Apply in [Platform Settings](../pages/admin/platform-settings.md)
4. Verify in audit log; announce in #ops if customer/creator-visible

### Shift close

1. Zero P0 open or explicitly handed to on-call
2. Queue depth note in handoff doc
3. Log metrics snapshot for daily ops report

---

## AI Responsibilities

- Surface AI flags on verification and moderation items — never auto-action
- Summarize creator history on [Creator Admin Detail](../pages/admin/creator-admin-detail.md)
- **No autonomous admin actions** — all writes require human operator

---

## Human Responsibilities

- Every approve/reject/suspend/refund/settings change
- Rationale field completed on enforcement actions
- Separation of duties: verifier ≠ same person as payout approver for same creator (where team size allows)

---

## Escalation Rules

| Condition | Escalate to |
|-----------|-------------|
| P0 food safety | Trust & Safety Lead + [Food Safety Incident SOP](food-safety-incident-sop.md) |
| Legal exposure | Legal advisor (documentation) + executive |
| Platform outage | Engineering on-call |
| Ambiguous policy | Trust & Safety Lead; `TODO(decision):` if unresolved 24h |

See [Escalation Guide](../support/escalation-guide.md) and [Trust & Safety Escalation Playbook](../docs/playbooks/trust-safety-escalation.md).

---

## SLA

| Activity | Target |
|----------|--------|
| P0 acknowledgment | 15 minutes |
| Verification queue (standard) | Per platform settings |
| Moderation high severity | 4 hours |
| Dispute first response | 24 hours |

---

## Audit Logging

Every admin action logs: `actor_id`, `action`, `target_type`, `target_id`, `rationale`, `timestamp`, `before/after` state hash where applicable. Immutable retention per [Trust Service](../engineering/services/trust-service.md).

---

## Resolution

Shift handoff complete; queues within SLA or escalated with owner assigned.

---

## Post Mortem

Weekly ops review: SLA misses, AI flag dismissals, repeat creator issues, settings changes. Feed into SOP and product improvements.

---

## Metrics

- Queue depth and age by type
- SLA adherence %
- Actions per operator (quality audit sample weekly)
- Escalation rate

---

## Future Automation

- Auto-routing by jurisdiction and queue type
- SLA breach auto-escalation notifications
- Settings change diff preview and rollback

---

## Related Documents

- [Operations README](README.md)
- [Admin Dashboard](../pages/admin/admin-dashboard.md)
- [Platform Settings](../pages/admin/platform-settings.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Partner Handbook — Operations](../docs/internal/partner-handbook.md)
