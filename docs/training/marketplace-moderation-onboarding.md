# Marketplace Moderation Onboarding

> Onboarding guide for Content Moderators — reviews, listings, messages, and community reports. **What to do** and **why**.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Reports to:** T&S Lead

Index: [Employee Training](README.md)

---

## Role Purpose

Marketplace Moderation protects review integrity, customer safety, and platform trust signals. You investigate flagged content and apply **consistent, documented enforcement** — never pay-to-remove reviews, never opaque takedowns.

**Why this role exists:** Reviews and community accountability are a trust layer in [Marketplace Mechanics](../../product/marketplace-mechanics.md#trust-model). One compromised review system undermines the entire "verified creator" thesis. AI classifiers prioritize your queue; **you decide every enforcement action.**

Moderation is not customer support and not verification — know your boundaries.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | Shared foundation + [Trust Philosophy](../../company/company-philosophy.md#trust-philosophy) | Trust decision tree memorized |
| **1–2** | [Moderation Queue](../../pages/admin/moderation-queue.md) spec | Queue UX and action types |
| **2** | [Moderation Assist](../../ai/moderation-assist.md) | AI categories and severity — signals only |
| **2–3** | [Marketplace Mechanics — Reviews & enforcement](../../product/marketplace-mechanics.md) | Progressive enforcement ladder |
| **3** | [Trust & Safety Standards](../standards/trust-and-safety-standards.md) | Policy baseline |
| **4** | Supervised review of 10 items (mixed severity) | Apply ladder with rationale |
| **5** | [Creator Admin Detail](../../pages/admin/creator-admin-detail.md) | Full creator context for decisions |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Values — Trust Is the Product](../../company/values.md#1-trust-is-the-product) | Non-negotiable trust bar |
| [AI Philosophy](../../company/constitution.md#ai-philosophy) | AI recommends; you approve |
| [Moderation Assist](../../ai/moderation-assist.md) | What AI does and cannot do |
| [Moderation Queue](../../pages/admin/moderation-queue.md) | Primary workspace |
| [Marketplace Mechanics — Reviews & community](../../product/marketplace-mechanics.md) | Review integrity rules |
| [Trust & Safety Standards](../standards/trust-and-safety-standards.md) | Complete trust framework |

### Week 2–4 (role depth)

| Document | Why |
|----------|-----|
| [Admin Dashboard](../../pages/admin/admin-dashboard.md) | SLA and queue health |
| [Dispute Detail](../../pages/admin/dispute-detail.md) | Order-linked moderation |
| [Trust Service](../../engineering/services/trust-service.md) | Audit trail backend |
| [Brand Voice & Tone](../../brand/voice-and-tone.md) | Creator communication tone |
| [Fraud Response](../playbooks/fraud-response.md) | Fraud-linked content |
| [Creator Suspension](../playbooks/creator-suspension-offboarding.md) | Escalation path |

---

## Systems Access

| System | Access level | Purpose |
|--------|--------------|---------|
| **Moderation queue** | Moderator | Triage, investigate, enforce |
| **Creator admin** | View | History, prior enforcement |
| **Order/message context** | View | Linked reports |
| **Moderation Assist panel** | View | AI category, severity, evidence |
| **Audit log** | View (your actions) | Confirm rationale recorded |
| **Internal comms templates** | Use | Warning and education notices |

**Not granted:** Verification approve/reject, payout adjustments, platform settings write.

---

## Decision Framework

### Enforcement ladder (progressive)

**Why progressive enforcement:** Creators are livelihoods. Permanent removal is reserved for severe or repeated violations. Education first when safe.

Typical progression (see [Marketplace Mechanics](../../product/marketplace-mechanics.md) for authoritative policy):

1. **No action** — false positive; document dismissal (`ai_flags_dismissed` feeds AI eval)
2. **Education / warning** — first-time minor policy miss
3. **Content action** — remove or hide specific listing/review/message
4. **Feature restriction** — limit messaging, reviews, or listing edits
5. **Suspension** — temporary; requires T&S Lead approval above threshold
6. **Permanent removal** — T&S Lead + documented appeal path

### Per-item review process

```
1. Read AI summary — do not auto-accept category or severity
2. Gather context — content, reporter, order history, prior enforcement
3. Map to policy category and ladder step
4. Choose action with mandatory rationale on any enforcement
5. Log audit entry — actor, timestamp, evidence, rationale
6. Escalate if: legal edge case, food safety, threats, fraud ring
```

### Hard rules

| Rule | Why |
|------|-----|
| **No pay-to-remove reviews** | Review integrity is a trust pillar |
| **No autonomous AI enforcement** | [Moderation Assist](../../ai/moderation-assist.md) never removes content |
| **Rationale required** | Audit trail for appeals and legal |
| **Escalate harassment/threats** | Safety-critical SLA |

---

## Escalation

| Trigger | Escalate to | Playbook |
|---------|-------------|----------|
| Threats, doxxing, illegal content | T&S Lead (immediate) | [Trust & Safety Escalation](../playbooks/trust-safety-escalation.md) |
| Food safety claim in review/listing | T&S + Ops | [Food Safety Incident](../playbooks/food-safety-incident.md) |
| Coordinated fraud / review manipulation | T&S | [Fraud Response](../playbooks/fraud-response.md) |
| Suspension or permanent removal | T&S Lead approval | [Creator Suspension](../playbooks/creator-suspension-offboarding.md) |
| Jurisdiction-specific legal question | Legal consult | Do not enforce pending guidance |
| Policy gap (no clear ladder step) | T&S Lead | Document; propose SOP update |

---

## Success Criteria

### Week 1
- [ ] 10 supervised moderation decisions with ladder alignment review
- [ ] Explain AI vs human boundary without notes
- [ ] Zero enforcement actions without audit rationale

### Day 30
- [ ] Independent queue throughput within SLA
- [ ] Inter-rater agreement with senior moderator above team threshold
- [ ] Correct escalation on all safety-critical items in training set

### Day 90
- [ ] Contribute to policy clarification or SOP update from edge cases
- [ ] Weekly AI sample audit participation (dismissed flags)
- [ ] Mentor new moderator on context gathering workflow

---

## Related Documents

- [Employee Training](README.md)
- [Trust & Safety Onboarding](trust-safety-onboarding.md) — Adjacent role
- [Operations Onboarding](operations-onboarding.md) — Queue coordination
- [ai/Moderation Assist](../../ai/moderation-assist.md)
- [pages/admin/](../../pages/admin/)
- [docs/standards/trust-and-safety-standards.md](../standards/trust-and-safety-standards.md)
