# Escalation Guide

> Severity matrix, owners, timelines, and decision paths — when to involve Trust & Safety, Legal, Operations, and executive leadership.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Customer Support · Trust & Safety  
**Companion:** [Support Playbook](support-playbook.md) · [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md)

---

## Purpose

Not every ticket belongs in Support forever. This guide defines **when to escalate**, **to whom**, **by when**, and **what context to include**. It bridges Tier 1 support workflows with cross-functional playbooks for safety, fraud, legal exposure, and platform integrity.

**Upgrade rule:** When in doubt, classify severity up. Downgrade only with documented rationale and incident commander (IC) or Support Lead approval.

**v1 rule:** Support Assist may *suggest* escalation — operators confirm. Keyword rules for food safety always win.

---

## Severity Levels

Aligned with [Trust & Safety Escalation — Severity Classification](../docs/playbooks/trust-safety-escalation.md#severity-classification):

| Level | Definition | Support action | IC assigned | Executive notify |
|-------|------------|----------------|-------------|------------------|
| **P0** | Active harm, legal exposure, system integrity breach, brand crisis | Stop normal workflow; page on-call | Immediate | Within 30 min |
| **P1** | High trust impact, multi-user affected, potential P0 if unaddressed | Escalate within 1 hour | Within 1 hour | Within 4 hours |
| **P2** | Elevated emotion, single-user high stakes, SLA systemic breach | Escalate same business day | Within 4 hours | Optional |
| **P3** | Standard support — no escalation | Resolve in Support | N/A | No |

---

## Escalation Matrix

### P0 — Immediate (page on-call)

| Scenario | Owner | Timeline | Playbook / SOP |
|----------|-------|----------|----------------|
| Allergic reaction with medical care | T&S on-call | Ack 15 min; T&S lead 30 min | [Food Safety Incident](../docs/playbooks/food-safety-incident.md) |
| Illness cluster (≥2 reports) or hospitalization | T&S IC | War room 15 min | [Food Safety Incident](../docs/playbooks/food-safety-incident.md) · [T&S Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Health department contact | T&S + Legal | Immediate | [T&S Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Confirmed allergen mislabeling + adverse reaction | T&S IC | Containment ≤1 hr | [Food Safety Incident](../docs/playbooks/food-safety-incident.md) |
| Active fraud network / identity manipulation at scale | T&S IC | War room 15 min | [Fraud Response](../docs/playbooks/fraud-response.md) |
| Account takeover with orders placed | T&S + Eng on-call | Lock account ≤1 hr | [Security](../docs/help-center/security.md) · Eng runbook |
| PII leak / unauthorized document access | Security + Legal | Immediate | [T&S Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Platform outage blocking fulfillment | Eng on-call | `#incidents` immediately | Engineering incident response |
| Verification auto-approve bug / audit failure | T&S + Eng | Immediate freeze | [Trust Verification Flow](../pages/flows/trust-verification-flow.md) |

**Support must not close P0 tickets.** Hand off to named owner; remain available for customer comms under IC direction.

---

### P1 — Within 1 hour

| Scenario | Owner | Timeline | Playbook / SOP |
|----------|-------|----------|----------------|
| Suspected allergen mislabeling (no ER claim yet) | T&S Supervisor | Investigate ≤1 hr | [Food Safety Incident](../docs/playbooks/food-safety-incident.md) |
| Single illness claim (non-hospital) | T&S Operator | Triage ≤1 hr | [Food Safety Incident](../docs/playbooks/food-safety-incident.md) |
| Creator operating with expired compliance | T&S | Suspend review ≤1 hr | [Creator Suspension](../docs/playbooks/creator-suspension-offboarding.md) |
| Fraud suspicion (single actor) | T&S | Case open ≤4 hr | [Fraud Response](../docs/playbooks/fraud-response.md) |
| Harassment or credible threat | Moderation / T&S | Review ≤4 hr | [T&S Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Media / social escalation on trust issue | T&S + Comms + Legal | IC ≤1 hr | [T&S Escalation](../docs/playbooks/trust-safety-escalation.md) |
| 3+ similar incidents same creator/region (72h) | T&S | Pattern review ≤4 hr | [T&S Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Refund dispute > policy threshold | Ops + Support Lead | Same day | [Dispute Resolution](../operations/README.md) |
| Payout missing > 2× documented SLA | Ops | Same day | [Payment Service](../engineering/services/payment-service.md) |

---

### P2 — Same business day

| Scenario | Owner | Timeline | Playbook / SOP |
|----------|-------|----------|----------------|
| High-emotion customer; no safety claim | Support Lead | Coach + respond ≤4 hr | [Support Playbook](support-playbook.md) |
| Verification delay > 2× SLA | T&S queue + CS notify | Update customer ≤1 business day | [Verification](../docs/help-center/verification.md) |
| Payment refund delayed > 10 business days | Ops | Trace ≤1 business day | [Refund Processing](../operations/README.md) |
| Policy exception request | Support Lead → Product/T&S | Decision ≤2 business days | Document `TODO(decision):` if unresolved |
| Repeat buyer dispute (3+ tickets) | Support → CS | Handoff ≤24 hr | [Customer Lifecycle](../docs/customer-success/customer-lifecycle.md#internal-handoffs) |
| Creator quality pattern (completion rate drop) | CS | Coaching outreach | [Success Metrics](../docs/customer-success/success-metrics.md) |
| Verification queue systemic > 2× SLA (48h+) | T&S Lead | P2 incident | [T&S Escalation](../docs/playbooks/trust-safety-escalation.md) |

---

### P3 — Resolve in Support

| Scenario | Resolution path |
|----------|-----------------|
| Order status inquiry | [Orders](../docs/help-center/orders.md) + admin lookup |
| Standard refund mediation | [Refunds](../docs/help-center/refunds.md) + [Macro Library](macro-library.md) |
| Account settings help | [Account](../docs/help-center/account.md) |
| Pickup / delivery timing | [Pickup](../docs/help-center/pickup.md) · [Delivery](../docs/help-center/delivery.md) |
| Verification status read-only | [Verification](../docs/help-center/verification.md) — no outcome promises |
| General policy questions | Help article + macro |

---

## When to Involve Each Function

### Trust & Safety

**Always:**

- Food safety, allergen injury, illness claims
- Fraud, identity manipulation, fake reviews
- Harassment, threats, illegal content
- Verification enforcement, suspensions, appeals
- Pattern detection across creators or markets

**Never promise:** Investigation outcome, suspension duration, or reinstatement timeline without T&S confirmation.

→ [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md) · [Moderation Queue](../pages/admin/moderation-queue.md)

### Legal

**Involve when:**

- Health authority or regulatory inquiry
- Subpoena, cease and desist, attorney correspondence
- Public statement required (any P0)
- Liability assessment for illness or injury claims
- Law enforcement data production request

**Support rule:** Do not respond to legal correspondence. Forward to Legal; acknowledge receipt to customer only if Legal approves.

→ Legal docs: [`legal/`](../legal/) *(Phase 5)*

### Operations / Payments

**Involve when:**

- Refund execution beyond agent authority
- Payout failure or dispute resolution deadlocked
- Creator onboarding ops blocker (non-verification)
- Refund processing SOP required

→ [Operations README](../operations/README.md)

### Engineering

**Involve when:**

- Platform bug affecting orders, payments, or auth
- Kill switch needed (market pause, creator order pause)
- Trust Service event propagation failure
- Support tooling outage

→ [Trust Service — Failure modes](../engineering/services/trust-service.md#failure-modes)

### Customer Success

**Involve when:**

- Repeat buyer at risk; high relationship value
- Creator health score drop correlated with support tickets
- Post-incident creator reactivation planning (IC-approved)

→ [Customer Success — Team Scope](../docs/customer-success/README.md#team-scope--handoffs)

### Founder / Executive

**Involve when (via T&S IC, not Support directly):**

- P0 classification confirmed
- Global order pause or market shutdown
- Brand crisis with media exposure
- Policy exception with platform-wide precedent
- Law enforcement or regulatory escalation

**Support does not page executives directly** except where Support Lead is acting IC for non-trust P0 (e.g., extended platform outage) per on-call runbook.

→ [Trust & Safety Escalation — Executive notification](../docs/playbooks/trust-safety-escalation.md#template-executive-p0-notification)

---

## Food Safety and Allergen Incidents

Dedicated path — overrides standard escalation timing.

```
Report received (Support)
    │
    ├─ Allergic reaction / ER / emergency ──► P0 ──► T&S on-call (15 min)
    │                                              └─► Food Safety playbook
    │
    ├─ Illness claim ──► P0/P1 ──► T&S (1 hr)
    │
    ├─ Mislabeling suspected ──► P1 ──► T&S Supervisor
    │
    └─ Quality issue (no health claim) ──► P3 ──► Order issue macro
                                              └─► NOT food safety queue
```

| Step | Actor | Action | Max time |
|------|-------|--------|----------|
| 1 | Support | Acknowledge; confirm medical care if applicable | 15 min (critical) / 30 min (urgent) |
| 2 | Support | Tag `food-safety`; attach order + creator IDs | Immediate |
| 3 | Support | Page T&S; **do not use standard refund/satisfaction macros** | Immediate |
| 4 | T&S | Classify P0/P1/P2; open war room if P0/P1 | 30 min |
| 5 | T&S IC | Containment: suspend, force-cancel, preserve evidence | P0: 1 hr |
| 6 | Support | Customer updates per IC-approved copy only | Ongoing |

→ [Food Safety Help article](../docs/help-center/food-safety.md) · [Food Safety Incident SOP](../operations/README.md) *(Phase 4)*

---

## Escalation Contacts

| Role | Escalation level | Contact method |
|------|------------------|----------------|
| Support Agent | L0 — first response | Ticket queue |
| Support Lead | L1 — SLA breach, P2, policy edge | Slack `#support` + DM |
| Trust Operator | L1 — trust intake | Trust queue |
| Trust Supervisor | L1 — enforcement ambiguity | Slack + pager |
| Trust Lead / IC | L2 — P0/P1 incidents | Pager |
| Legal Counsel | L2 — regulatory, liability | Pager |
| Engineering On-Call | L2 — system failures | Pager |
| Founder / Executive | L3 — P0, brand crisis | Phone (via IC) |
| Communications | L2 — external narrative | Slack (Legal-approved) |

Roster maintained in PagerDuty — reviewed quarterly by People Ops.

---

## How to Escalate (Quality Bar)

Every escalation must include:

| Field | Example |
|-------|---------|
| **Ticket / incident ID** | `tkt_4412` |
| **Severity draft** | P1 — suspected mislabeling |
| **User IDs** | Customer `cus_…`, Creator `cre_…` |
| **Order ID** | `ord_…` |
| **Timeline** | Ordered Sat 11 AM; reaction Sat 2 PM; ticket Sun 9 AM |
| **Customer statement** | Verbatim symptom/description |
| **Actions taken** | Acknowledged; pulled order snapshot; told customer T&S reviewing |
| **Recommended next action** | Suspend creator pending label review |
| **Customer comms** | What you already promised (avoid over-promising) |

Post escalation in ticket note + Slack thread ( `#trust-safety` or war room). Assign owner before marking yourself done.

---

## Response Timelines by Path

| Path | First ack | Owner assigned | Customer next update |
|------|-----------|----------------|----------------------|
| P0 food safety | 15 min | 30 min | IC-directed; ≤2 hr unless IC specifies |
| P1 trust | 1 hr | 4 hr | Within 4 hr with status |
| P2 elevated | 4 hr | Same day | Within 24 hr |
| Ops refund | 24 hr | 48 hr | Refund trace result |
| CS handoff | 24 hr | 1 business day | CS introduces themselves |
| P3 standard | Per SLA | Self | Resolution or 24 hr update |

---

## De-escalation

Downgrade severity only when:

1. IC or Support Lead documents rationale (e.g., quality complaint reclassified — no health claim).
2. Affected parties notified if expectations changed.
3. Ticket re-tagged; SLA recalculated.

**Never de-escalate** food safety tickets without T&S sign-off.

---

## Decision Tree (Support Agent)

```
START: New ticket
│
├─ Food safety keyword or category?
│   YES → P0/P1 path → T&S (see Food Safety section)
│
├─ Account compromised / unauthorized orders?
│   YES → P0/P1 → T&S + Eng
│
├─ Fraud, harassment, illegal content?
│   YES → P1 → T&S / Moderation
│
├─ Platform broken / mass impact?
│   YES → P0/P1 → #incidents
│
├─ Refund > threshold or 5+ days unresolved?
│   YES → P1/P2 → Ops
│
├─ Verification outcome dispute?
│   YES → P2 → T&S (Support does not decide)
│
├─ Repeat buyer / creator at-risk pattern?
│   YES → P2 → Customer Success
│
└─ ELSE → P3 → Resolve with Help + macros
```

→ Training version: [Support Onboarding — Decision Framework](../docs/training/support-onboarding.md#decision-framework)

---

## Playbook Index

| Incident type | Primary playbook | Support role |
|---------------|------------------|--------------|
| Food safety / allergen / illness | [Food Safety Incident](../docs/playbooks/food-safety-incident.md) | Triage, ack, hand off, IC-directed comms |
| Cross-functional trust crisis | [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md) | Initial report; surge macros |
| Fraud | [Fraud Response](../docs/playbooks/fraud-response.md) | Evidence collection; no accuse customer/creator |
| Creator enforcement | [Creator Suspension & Offboarding](../docs/playbooks/creator-suspension-offboarding.md) | Route; do not announce suspension to other party prematurely |
| Feature-caused regression | [Launching a New Feature](../docs/playbooks/launching-new-feature.md) | Customer impact comms |
| Market-wide issue | [Launching a New Market](../docs/playbooks/launching-new-market.md) | Pause notifications |

### Operations SOPs (Phase 4)

| SOP | When Support routes here |
|-----|--------------------------|
| [Food Safety Incident](../operations/README.md) | All P0/P1 food safety |
| [Dispute Resolution](../operations/README.md) | Deadlocked refund/dispute |
| [Refund Processing](../operations/README.md) | Approved refund execution |
| [Moderation](../operations/README.md) | Content reports (with T&S) |
| [Verification Review](../operations/README.md) | Status questions only — not decisions |
| [Creator Suspension](../operations/README.md) | Enforcement actions |

---

## Metrics

| Metric | Target |
|--------|--------|
| P0 ack time (Support → T&S engaged) | ≤ 15 minutes |
| Escalation package completeness | 100% required fields |
| Mis-routed escalation rate | ↓ — weekly audit |
| P0 customer update within 2 hr | ≥ 95% |
| De-escalation without documentation | 0 |

→ [Support Playbook — Metrics](support-playbook.md#metrics--reporting) · [Trust Metrics](../product/success-metrics-overview.md#trust-metrics)

---

## Related Documents

- [Support Playbook](support-playbook.md)
- [Macro Library — When NOT to use macros](macro-library.md#when-not-to-use-a-macro)
- [Support Assist](../ai/support-assist.md)
- [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md)
- [Food Safety Incident](../docs/playbooks/food-safety-incident.md)
- [Contact Support](../docs/help-center/contact-support.md)
- [Support Onboarding](../docs/training/support-onboarding.md)
