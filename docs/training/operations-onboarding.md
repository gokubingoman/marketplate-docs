# Marketplace Operations Onboarding

> Onboarding guide for Marketplace Operations — verification throughput, creator lifecycle, disputes, and platform health. **What to do** and **why**.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Marketplace Operations  
**Reports to:** Operations Lead

Index: [Employee Training](README.md)

---

## Role Purpose

Marketplace Operations keeps the platform running: verification queues moving, creators activated, disputes resolved, SLAs met, and anomalies surfaced before they become incidents.

**Why this role exists:** Creators cannot sell until verified. Customers cannot trust until supply is verified. Ops is the connective tissue between product intent and marketplace reality. Internal ops tooling must meet the same quality bar as customer product — see [Admin Dashboard purpose](../../pages/admin/admin-dashboard.md#purpose).

Operations sits adjacent to Trust & Safety (you may share queue access) but focuses on **throughput, creator success, and platform health** — not policy interpretation or enforcement ladder decisions.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | Shared foundation + [Platform Operations persona](../../product/personas.md#platform-operations-internal) | Understand accountability model |
| **1–2** | [Admin Dashboard](../../pages/admin/admin-dashboard.md) tour | Navigate queue stats, alerts, SLA widgets |
| **2–3** | [Verification Queue](../../pages/admin/verification-queue.md) (observe → supervised actions) | Process one identity submission end-to-end |
| **3** | [Creator Admin Detail](../../pages/admin/creator-admin-detail.md) | Full creator lifecycle view |
| **4** | [Launching a Creator](../playbooks/launching-a-creator.md) playbook | Signup → first order path |
| **5** | [Platform Settings](../../pages/admin/platform-settings.md) (read) | Where SLAs and thresholds live |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Company Philosophy — Operations](../../company/company-philosophy.md#operations-philosophy) | Owner, SLA, audit trail requirements |
| [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Verified-to-sell invariant, fulfillment models |
| [Trust Verification Flow](../../pages/flows/trust-verification-flow.md) | End-to-end verification pipeline |
| [Verification Assist](../../ai/verification-assist.md) | AI flags — you decide, AI does not override |
| [Admin Dashboard](../../pages/admin/admin-dashboard.md) | Operational home |
| [Verification Queue](../../pages/admin/verification-queue.md) | Primary queue workflow |

### Week 2–4 (role depth)

| Document | Why |
|----------|-----|
| [Dispute Detail](../../pages/admin/dispute-detail.md) | Case management for payment/order disputes |
| [Creator Onboarding Flow](../../pages/flows/creator-onboarding-flow.md) | Where creators get stuck |
| [Trust Service](../../engineering/services/trust-service.md) | Backend verification and audit |
| [Payment Service](../../engineering/services/payment-service.md) | Payouts and dispute mechanics |
| [Success Metrics — Platform Health](../../product/success-metrics-overview.md) | Metrics you influence |
| [Marketplate Standards](../standards/marketplate-standards.md) | Operational quality bar |

---

## Systems Access

| System | Access level | Purpose |
|--------|--------------|---------|
| **Admin console** | Operator | [Admin Dashboard](../../pages/admin/admin-dashboard.md) |
| **Verification queue** | Reviewer | Approve / reject / request info |
| **Creator admin** | Read-write (notes, status) | Lifecycle management |
| **Dispute management** | Operator | Resolution within policy |
| **Platform settings** | Read (write: Ops Lead only) | SLA targets, queue config |
| **Analytics dashboards** | View | Activation, verification TAT, dispute rate |
| **Notification logs** | View | Confirm creator/customer comms sent |

**Coordination with T&S:** Moderation queue and suspension actions may require T&S approval. Know your write boundaries before day 1 production access.

---

## Decision Framework

### Verification review (human approval required)

Per [Human approval on high stakes](../../product/marketplace-mechanics.md#marketplace-model-overview):

1. **Read AI summary** — [Verification Assist](../../ai/verification-assist.md) flags are signals, not decisions
2. **Check checklist** — identity, kitchen, compliance per submission type
3. **Decide:** Approve · Reject (mandatory rationale) · Request additional info
4. **Audit** — every action logged with actor, timestamp, rationale
5. **Sync** — creator-facing status updates on [Identity Verification](../../pages/auth/identity-verification.md), [Kitchen Verification](../../pages/auth/kitchen-verification.md), [Compliance Center](../../pages/auth/compliance-center.md)

**Why no auto-approve:** False approvals weaken the trust thesis. Speed without integrity is growth we cannot afford.

### Creator activation

| Signal | Action | Why |
|--------|--------|-----|
| Verification complete, catalog empty | Creator Success outreach | Activation metric; creator may not know next step |
| Verification stalled > SLA | Request info or escalate fraud | Respect creator time; prevent queue gaming |
| Compliance expiring | Proactive notification | Prevent silent delisting |

### Dispute resolution

- Link case to order, messages, policies — full context in one view
- Apply marketplace policies consistently; document exception rationale
- Escalate legal/jurisdiction edge cases — do not improvise policy

---

## Escalation

| Trigger | Escalate to | Reference |
|---------|-------------|-----------|
| Fraud signals on verification | T&S | [Fraud Response](../playbooks/fraud-response.md) |
| Food safety allegation | T&S (immediate) | [Food Safety Incident](../playbooks/food-safety-incident.md) |
| Policy exception (verification) | T&S Lead | ADR if recurring pattern |
| Creator suspension | T&S | [Creator Suspension](../playbooks/creator-suspension-offboarding.md) |
| Payout system error | Engineering + Finance | Incident protocol |
| SLA systemic miss | Ops Lead | Root cause + SOP update |

---

## Success Criteria

### Week 1
- [ ] Process 5 supervised verification reviews with checklist compliance
- [ ] Navigate creator admin from signup through verification status
- [ ] Explain AI-assist vs human decision boundary without notes

### Day 30
- [ ] Independent verification queue throughput within SLA
- [ ] Dispute resolution within team target
- [ ] Zero audit trail gaps on negative verification actions
- [ ] Creator activation follow-up within 48h of verification complete

### Day 90
- [ ] Identify one workflow automation candidate (document in SOP)
- [ ] Contribute to queue SLA post-mortem or playbook update
- [ ] Mentor new ops hire on admin console navigation

---

## Related Documents

- [Employee Training](README.md)
- [Trust & Safety Onboarding](trust-safety-onboarding.md) — Adjacent role, shared queues
- [Engineering — Trust Service](../../engineering/services/trust-service.md)
- [AI — Verification Assist](../../ai/verification-assist.md)
- [docs/standards/](../standards/)
- [docs/playbooks/](../playbooks/)
