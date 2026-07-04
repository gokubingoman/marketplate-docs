# Trust & Safety Onboarding

> Onboarding guide for Trust & Safety analysts and leads — verification, compliance, disputes, enforcement, and incidents. **What to do** and **why**.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Reports to:** Head of Trust & Safety / Executive

Index: [Employee Training](README.md)

---

## Role Purpose

Trust & Safety is the human gate for Marketplate's core thesis: **trust is the product.** You approve verification, resolve high-stakes disputes, interpret policy at the edge, and respond when integrity fails.

**Why this role exists:** Generic marketplaces race to maximize listings. Marketplate races to maximize **verified, trustworthy supply.** One false verification approval is a food safety risk. One false rejection destroys a livelihood. AI scales your capacity; **you own every high-stakes decision.**

When trust and growth conflict, trust wins — without exception.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | Shared foundation + [Trust Decision Tree](../../company/company-philosophy.md#trust-philosophy) | Can apply tree to scenarios |
| **1–2** | [Marketplace Mechanics — Trust model](../../product/marketplace-mechanics.md#trust-model) | All five layers + invariants |
| **2** | [Trust Verification Flow](../../pages/flows/trust-verification-flow.md) | Pipeline end-to-end |
| **2–3** | [Verification Queue](../../pages/admin/verification-queue.md) + [Verification Assist](../../ai/verification-assist.md) | Supervised approvals |
| **3** | [Trust & Safety Standards](../standards/trust-and-safety-standards.md) | Complete framework |
| **4** | [Moderation Queue](../../pages/admin/moderation-queue.md) + [Moderation Assist](../../ai/moderation-assist.md) | Enforcement oversight |
| **5** | Tabletop: [Food Safety Incident](../playbooks/food-safety-incident.md) + [Fraud Response](../playbooks/fraud-response.md) | Incident response paths |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Founding Constitution — Trust Philosophy](../../company/constitution.md#trust-philosophy) | Non-negotiable pillars |
| [Company Philosophy — Trust](../../company/company-philosophy.md#trust-philosophy) | Decision tree and anti-patterns |
| [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Identity, kitchen, compliance, enforcement |
| [Trust Verification Flow](../../pages/flows/trust-verification-flow.md) | Security and access model |
| [Verification Assist](../../ai/verification-assist.md) | AI boundaries on verification |
| [Moderation Assist](../../ai/moderation-assist.md) | AI boundaries on enforcement |
| [Trust Service](../../engineering/services/trust-service.md) | Backend audit and state |

### Week 2–4 (role depth)

| Document | Why |
|----------|-----|
| [Platform Settings](../../pages/admin/platform-settings.md) | Thresholds, SLAs, discovery weights |
| [Dispute Detail](../../pages/admin/dispute-detail.md) | High-stakes case management |
| [Creator Admin Detail](../../pages/admin/creator-admin-detail.md) | Full lifecycle |
| [AI Platform README](../../ai/README.md) | Eval pipeline, human sign-off |
| [Discovery Ranking](../../ai/discovery-ranking.md) | Trust gates in discovery |
| [Success Metrics — Trust](../../product/success-metrics-overview.md) | False positive/negative rates |
| [Personas — Platform Operations](../../product/personas.md#platform-operations-internal) | Your internal user |

### Playbooks (memorize triggers)

| Playbook | When |
|----------|------|
| [Trust & Safety Escalation](../playbooks/trust-safety-escalation.md) | High-severity incidents |
| [Food Safety Incident](../playbooks/food-safety-incident.md) | Illness, contamination reports |
| [Fraud Response](../playbooks/fraud-response.md) | Identity fraud, payment fraud |
| [Creator Suspension](../playbooks/creator-suspension-offboarding.md) | Enforcement with appeals |

---

## Systems Access

| System | Access level | Purpose |
|--------|--------------|---------|
| **Verification queue** | T&S Reviewer | Approve / reject / request info |
| **Moderation queue** | T&S / Senior Moderator | Enforcement and appeals |
| **Dispute management** | T&S | Policy exceptions, high-value disputes |
| **Creator admin** | Full | Suspension, notes, compliance status |
| **Platform settings** | T&S Lead write | Trust thresholds, SLAs |
| **Document viewer** | Watermarked access | Verification docs — audited |
| **AI eval dashboards** | View | Model quality, fallback rates |
| **Audit logs** | Full read | Investigations |

---

## Decision Framework

### Trust Decision Tree (authoritative)

From [Company Philosophy](../../company/company-philosophy.md#trust-philosophy):

```
1. Weakens food safety compliance? → STOP. Do not ship / do not approve.
2. Allows unverified creators to transact? → STOP unless time-bounded ADR exception.
3. Reduces customer transparency? → Redesign or do not ship.
4. Weakens review integrity? → Redesign.
5. Else → Proceed with standard review + audit trail.
```

### Verification decisions

| Outcome | When | Requirement |
|---------|------|-------------|
| **Approve** | Checklist complete; AI flags resolved or documented | Audit log entry |
| **Reject** | Failed criteria, fraud, or unresolvable mismatch | Mandatory rationale; creator notification path |
| **Request info** | Incomplete but good faith | Clear ask; SLA for resubmission |

**Why no auto-approve:** Platform Settings default — [no auto-approve verification](../../ai/README.md#configuration). Changing this requires executive + legal review.

### AI governance (T&S sign-off)

Trust-critical AI changes require your approval:

- Verification confidence thresholds
- Moderation severity thresholds
- Discovery trust gate changes
- Model promotion after eval pipeline

See [AI Platform — Evaluation pipeline](../../ai/README.md#evaluation-pipeline).

---

## Escalation

| Trigger | Escalate to | Action |
|---------|-------------|--------|
| Active food safety harm | Executive + Legal (immediate) | [Food Safety Incident](../playbooks/food-safety-incident.md) |
| Regulatory inquiry | Legal | Preserve audit logs; no ad-hoc statements |
| Media / PR risk | Executive + Comms | Coordinate single voice |
| Systemic verification failure | Eng + AI Platform | Incident + halt promotions |
| Policy exception for growth | Executive | ADR with time bound |
| Criminal activity | Legal + law enforcement protocol | Document chain of custody |

You are often the **final escalation point** for support and moderation — respond with documented rationale.

---

## Success Criteria

### Week 1
- [ ] Pass verification scenario exam (approve, reject, request info, fraud escalate)
- [ ] Complete food safety tabletop exercise
- [ ] Process 5 supervised verification items with zero audit gaps

### Day 30
- [ ] Independent verification SLA compliance
- [ ] False approval rate within team target (quality over speed)
- [ ] Lead one moderation appeal review with documented outcome
- [ ] Sign off on one AI eval sample audit

### Day 90
- [ ] Own trust metric dashboard slice (TAT, false positives, gate violations)
- [ ] Author or update one SOP from operational learnings
- [ ] Train ops or moderation hire on escalation boundaries

---

## Related Documents

- [Employee Training](README.md)
- [Marketplace Moderation Onboarding](marketplace-moderation-onboarding.md)
- [Operations Onboarding](operations-onboarding.md)
- [AI Systems Onboarding](ai-systems-onboarding.md)
- [company/](../../company/) · [ai/](../../ai/) · [engineering/services/trust-service.md](../../engineering/services/trust-service.md)
- [pages/admin/](../../pages/admin/) · [docs/standards/](../standards/) · [docs/playbooks/](../playbooks/)
