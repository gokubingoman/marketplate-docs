# Customer Support Onboarding

> Onboarding guide for Customer Support specialists. **What to do** and **why** Marketplate operates this way.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Customer Support  
**Reports to:** Support Lead → Operations

Index: [Employee Training](README.md)

---

## Role Purpose

Customer Support reduces uncertainty for creators and customers. You are often the human face of Marketplate when something goes wrong — order status, verification delays, payout questions, or policy confusion.

**Why this role exists:** Creators bet their livelihood on Marketplate. Customers make trust decisions with their money and health. Unclear or slow support erodes the same trust that verification and product design build. Operational excellence is respect — see [Value 5](../../company/values.md#5-operational-excellence-is-respect).

You do **not** approve verification, moderate content, or suspend accounts. You triage, inform, and escalate.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | Read shared foundation ([Training README](README.md#before-you-start-all-roles)) | Can explain trust thesis |
| **1–2** | [Brand Voice & Tone](../../brand/voice-and-tone.md) + [Personas](../../product/personas.md) (End Customer + creator sections) | Match tone to audience |
| **2–3** | [Support Assist](../../ai/support-assist.md) + [Help page spec](../../pages/customer/help.md) | Understand AI-assisted search and ticket routing |
| **3–4** | Shadow 10 tickets across order, verification, and payout categories | See escalation patterns |
| **4–5** | [Order Fulfillment Flow](../../pages/flows/order-fulfillment-flow.md) + [Customer Purchase Flow](../../pages/flows/customer-purchase-flow.md) | Trace customer journey end-to-end |
| **5** | [Trust & Safety Standards](../standards/trust-and-safety-standards.md) (support-relevant sections) | Know mandatory escalation triggers |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Founding Constitution](../../company/constitution.md) | Governing principles — especially operations and trust |
| [Company Philosophy — Operations](../../company/company-philosophy.md#operations-philosophy) | Every interaction should reduce uncertainty |
| [Product Overview](../../product/overview.md) | What Marketplate is and is not — avoid delivery-app assumptions |
| [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Disputes, fulfillment models, trust invariants |
| [Support Assist](../../ai/support-assist.md) | How AI classifies tickets; what it cannot do |
| [Brand Voice & Tone](../../brand/voice-and-tone.md) | External communication standards |

### Week 2–4 (role depth)

| Document | Why |
|----------|-----|
| [Value Props](../../product/value-props.md) | What creators and customers expect from us |
| [Success Metrics — Customer](../../product/success-metrics-overview.md) | CSAT, contact rate, time-to-trust |
| [Creator Onboarding docs](../onboarding/) | Answer "how do I get verified?" accurately |
| [Order Service](../../engineering/services/order-service.md) | Order states you will reference in tickets |
| [Payment Service](../../engineering/services/payment-service.md) | Payout timing, dispute basics |
| [Chef Quality Standards](../standards/chef-quality-standards.md) | Creator-side expectations you may reference |

---

## Systems Access

Request through IT / Support Lead on day 1.

| System | Access level | Purpose |
|--------|--------------|---------|
| **Support ticket platform** | Agent | Primary workspace — respond, tag, escalate |
| **Help center CMS** | Read (+ draft if content team) | Verify FAQ accuracy before citing |
| **Creator profile (admin read-only)** | View | [Creator Admin Detail](../../pages/admin/creator-admin-detail.md) — order and verification context |
| **Order lookup** | View | Status, fulfillment, payment state |
| **Support Assist dashboard** | View | See AI classification, suggested macros |
| **Internal wiki / this repo** | Read + PR for doc fixes | Institutional memory |
| **Slack** `#support` · `#trust-safety` · `#incidents` | Member | Team coordination and escalation |

**Not granted:** Verification queue write access, moderation actions, platform settings, payout adjustments without supervisor approval.

---

## Decision Framework

Apply [Operations Philosophy](../../company/company-philosophy.md#operations-philosophy): reduce uncertainty, document outcomes, escalate trust-impacting cases.

### Can I resolve this ticket?

```
1. Is this a food safety or illness report?
   YES → Stop. Escalate immediately to Trust & Safety.
         Use [Food Safety Incident](../playbooks/food-safety-incident.md) playbook.
   NO  → Continue

2. Does this require verification, moderation, or account enforcement?
   YES → Do not promise outcomes. Acknowledge, set expectation,
         escalate to T&S or Moderation with full context.
   NO  → Continue

3. Is this a payment dispute or refund over policy threshold?
   YES → Follow dispute macro. Escalate to Ops if amount/policy edge case.
   NO  → Continue

4. Can I answer from Help center + order/creator context?
   YES → Respond with macro (personalized). Log resolution category.
   NO  → Escalate to Support Lead or specialist queue.
```

### Response principles

| Principle | Why | Do |
|-----------|-----|-----|
| **Plain language** | Cottage food operators and first-time customers | No internal jargon; use [Glossary](../../company/glossary.md) terms |
| **Explicit states** | Uncertainty erodes trust | Say what happened, what happens next, and by when |
| **Never guess on trust** | Wrong verification info is worse than "I'll find out" | Escalate rather than speculate |
| **AI assists; you decide** | Support Assist suggests macros — you own the reply | Edit macros; never send blind |

---

## Escalation

| Trigger | Escalate to | Playbook |
|---------|-------------|----------|
| Food safety, illness, allergen injury | T&S on-call (immediate) | [Food Safety Incident](../playbooks/food-safety-incident.md) |
| Harassment, threats, illegal content | Moderation / T&S | [Trust & Safety Escalation](../playbooks/trust-safety-escalation.md) |
| Fraud suspicion (creator or customer) | T&S | [Fraud Response](../playbooks/fraud-response.md) |
| Payout missing > SLA | Operations | Ops lead + [Dispute Detail](../../pages/admin/dispute-detail.md) |
| Platform outage affecting orders | `#incidents` | Engineering on-call |
| Policy exception request | Support Lead → Product/T&S | Document as `TODO(decision):` if unresolved |

**Escalation quality bar:** Include ticket ID, user IDs, order IDs, timeline, what you told the customer, and recommended next action.

---

## Success Criteria

### Week 1
- [ ] Completed shadow sessions with annotated ticket notes
- [ ] Passed trust escalation quiz (food safety, verification, moderation boundaries)
- [ ] Sent first supervised customer reply using brand voice checklist

### Day 30
- [ ] Handle Tier 1 tickets independently (order status, FAQ, basic creator questions)
- [ ] First-contact resolution rate within team target
- [ ] Zero trust-boundary violations (no verification promises, no moderation actions)
- [ ] Average response time within SLA
- [ ] Identified and submitted ≥1 Help center gap or macro improvement

### Day 90
- [ ] Mentor new hire on escalation patterns
- [ ] CSAT at or above team median
- [ ] Contribute to post-mortem doc after one escalated incident

---

## Related Documents

- [Employee Training](README.md)
- [AI Platform — Support Assist](../../ai/support-assist.md)
- [Customer Help](../../pages/customer/help.md)
- [Marketplate Standards](../standards/marketplate-standards.md)
- [Onboarding a New Employee](../playbooks/onboarding-new-employee.md)
