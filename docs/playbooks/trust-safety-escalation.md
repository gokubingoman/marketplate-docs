# Trust & Safety Escalation

> End-to-end operational playbook for high-severity trust incidents — escalation paths, war rooms, and executive decisions.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook type:** Cross-functional orchestration

---

## Purpose

This playbook defines **when and how to escalate** trust incidents beyond standard operator workflows. It connects severity classification, incident command, cross-functional war rooms, executive notification, and resolution standards for events that threaten platform integrity, user safety, legal exposure, or brand trust.

Use specialized playbooks for detailed execution:

- [Food Safety Incident](food-safety-incident.md)
- [Fraud Response](fraud-response.md)
- [Creator Suspension & Offboarding](creator-suspension-offboarding.md)

**Governing thesis:** When values conflict, **trust wins** — [Company Values](../../company/values.md#using-values-in-decisions).

---

## Trigger

Escalation is triggered when an incident exceeds normal queue handling:

| Trigger category | Examples | Default severity |
|------------------|----------|------------------|
| **Safety** | Illness claim, allergen exposure, injury | P0 |
| **Fraud at scale** | Active fraud network, false approve with live orders | P0–P1 |
| **Enforcement dispute** | Media coverage, creator with large following suspended | P1 |
| **System failure** | Audit write failure, verification auto-approve bug | P0 |
| **Legal / regulatory** | Health dept, subpoena, cease and desist | P0–P1 |
| **Pattern escalation** | 3+ similar incidents in 72h on same creator/region | P1 |
| **SLA systemic breach** | Verification queue > 2× SLA for 48h+ | P2 |
| **AI failure** | Trust gate violation in Discovery (unverified in results) | P0 |
| **Data / privacy** | PII leak, unauthorized document access | P0 |

---

## Stakeholders

### Escalation roster

| Role | Escalation level | Contact method |
|------|------------------|----------------|
| **Trust Operator** | L0 — first response | Queue / ticket |
| **Trust Supervisor** | L1 — SLA breach, ambiguous enforcement | Slack + pager |
| **Trust Lead** | L2 — P1 incidents, fraud, safety | Pager |
| **Legal Counsel** | L2 — regulatory, liability, public statements | Pager |
| **Engineering On-Call** | L2 — system failures, containment actions | Pager |
| **Founder / Executive** | L3 — P0, brand crisis, policy exception | Phone |
| **Communications** | L2 — external narrative (Legal-approved) | Slack |

### Incident Commander (IC)

IC is assigned per incident — typically Trust Lead for safety/fraud, Eng Lead for system failures. IC owns timeline, decisions, and comms coordination until handoff or close.

---

## Severity Classification

| Level | Definition | IC assigned | Executive notify | War room |
|-------|------------|-------------|------------------|----------|
| **P0** | Active harm, legal exposure, system integrity breach, brand crisis | Immediate | Within 30 min | Required |
| **P1** | High trust impact, multi-user affected, potential P0 if unaddressed | Within 1 hour | Within 4 hours | Recommended |
| **P2** | Elevated queue item, single-user high emotion, SLA systemic | Within 4 hours | Optional | Optional |
| **P3** | Standard queue — no escalation | N/A | No | No |

**Upgrade rule:** When in doubt, classify up. Downgrade only with documented rationale and IC approval.

---

## Prerequisites

| Prerequisite | Owner |
|--------------|-------|
| PagerDuty / on-call rotation current | Trust + Eng |
| Escalation contact list reviewed quarterly | People Ops |
| War room Slack channels configured | `#incident-trust`, `#incident-food-safety`, `#incident-fraud` |
| Incident tracker template | Trust Ops |
| Executive notification template | Trust Lead |
| Platform kill switches documented | Engineering |

**Kill switches (Engineering):**

| Switch | Effect | Authority |
|--------|--------|-----------|
| Global creator order pause | No new orders platform-wide | Trust Lead + Founder |
| Market pause flag | Discovery + checkout disabled for market | Trust Lead + Market Launch Lead |
| Verification queue freeze | No approvals until review | Trust Lead |
| Discovery trust gate force-refresh | Re-index verification status | Eng on-call |

---

## Phase-by-Phase Execution

### Phase 1 — Recognize & Classify (0–15 minutes)

| Step | Actor | Action |
|------|-------|--------|
| 1.1 | First responder | Identify escalation trigger; do not defer if safety suspected |
| 1.2 | Operator or Support | Create incident record: ID, severity draft, linked entities (creator, order, case) |
| 1.3 | Operator | Notify L1 (Supervisor) if P1+ criteria met |
| 1.4 | Supervisor | Confirm or adjust severity; assign IC for P0/P1 |
| 1.5 | IC | Open war room channel; post initial situation report |

**Situation report format:**

```
INCIDENT [ID] — [P0/P1/P2]
IC: [name]
Trigger: [one line]
Impact: [users, orders, markets affected]
Actions in progress: [bullets]
Next update: [time]
Linked: [order IDs, creator IDs, case IDs]
```

---

### Phase 2 — Mobilize (15–60 minutes)

| Step | Actor | Action |
|------|-------|--------|
| 2.1 | IC | Invoke specialized playbook if applicable |
| 2.2 | IC | Assign roles: Operations Lead, Comms Lead, Scribe, Engineering Liaison |
| 2.3 | IC (P0) | Notify Trust Lead, Legal, Eng on-call |
| 2.4 | IC (P0) | Notify Founder/executive within 30 minutes |
| 2.5 | Scribe | Maintain live timeline in incident doc |
| 2.6 | Engineering | Assess system contribution; execute kill switch if IC approves |
| 2.7 | Legal | Join within SLA; advise on external comms hold |

**Parallel playbook routing:**

| Incident type | Primary playbook |
|---------------|------------------|
| Food safety / allergen / illness | [Food Safety Incident](food-safety-incident.md) |
| Fraud / identity manipulation | [Fraud Response](fraud-response.md) |
| Creator enforcement / appeal crisis | [Creator Suspension](creator-suspension-offboarding.md) |
| Feature-caused trust regression | [Launching a New Feature](launching-new-feature.md) — rollback |
| Market-wide issue | [Launching a New Market](launching-new-market.md) — pause |

---

### Phase 3 — Contain & Stabilize

IC ensures containment actions from specialized playbook are underway:

| Containment type | Typical actions | System |
|------------------|-----------------|--------|
| Creator risk | Suspend creator, hold payouts | Trust Service → `creator.suspended` |
| Customer risk | Force-cancel orders, refund | Order + Payment |
| Discovery integrity | Remove from index, trust gate audit | Discovery Service |
| Verification integrity | Queue freeze, audit recent approvals | Trust Service admin |
| Data breach | Revoke access, rotate credentials | Security + Identity Service |

**Comms hold:** No external statements until Legal approves — IC enforces.

---

### Phase 4 — Resolve & Communicate

| Step | Actor | Action |
|------|-------|--------|
| 4.1 | IC | Transition from containment to resolution plan with owners |
| 4.2 | Operations Lead | Execute specialized playbook Phases 3–4 |
| 4.3 | Comms Lead | Draft internal and external comms — Legal review |
| 4.4 | Support | Surge macros, Help article update if customer-facing |
| 4.5 | IC | Status updates to war room every [2h P0 / 4h P1] until stable |
| 4.6 | IC | Executive briefing at resolution milestone |
| 4.7 | IC | Declare incident stable — move to recovery |

---

### Phase 5 — Recovery & Close

| Step | Actor | Action |
|------|-------|--------|
| 5.1 | IC | Verify kill switches reversed (if applied) with monitoring |
| 5.2 | Trust Ops | Reinstatement decisions per specialized playbook |
| 5.3 | Engineering | Hotfixes deployed; post-deploy verification |
| 5.4 | IC | Final situation report to executives |
| 5.5 | IC | Close incident; schedule retro within 5 business days |
| 5.6 | Scribe | Archive incident timeline to immutable record |

---

## Decision Points

| Decision | Owner | Escalation to |
|----------|-------|---------------|
| P0 classification | Supervisor or IC | Trust Lead if disputed |
| Kill switch activation | IC | Trust Lead + Eng on-call; Founder for global pause |
| Public statement | Legal + Comms | Founder approval for P0 |
| Policy exception for creator | Trust Lead | Founder — `TODO(decision):` documented |
| Downgrade severity | IC | Document rationale; notify prior escalated parties |
| Law enforcement data production | Legal | Founder informed |
| Incident close vs. monitor | IC | Trust Lead sign-off for P0 |

**Values decision sequence** (from [Company Values](../../company/values.md#using-values-in-decisions)):

1. Trust check
2. Creator check (legitimate creators harmed by incident response?)
3. Clarity check (are affected users informed?)
4. Long-term check

---

## Communication Templates

### Template: Executive P0 Notification

**Channel:** Phone + email  
**Timing:** Within 30 minutes of P0 classification

```
Subject: P0 TRUST INCIDENT — [INCIDENT_ID] — [One-line summary]

Severity: P0
IC: [Name]
Started: [UTC timestamp]

Situation:
[2–3 sentences — facts only, no speculation]

Impact:
• Users affected: [N customers, N creators]
• Orders: [N active, $ exposure]
• Markets: [list or "platform-wide"]

Actions taken:
• [Containment bullets]

Immediate needs:
• [Legal / Founder decision / None at this time]

Next update: [Time] via [channel]

War room: [#channel]
```

### Template: War Room — Status Update

**Channel:** Incident Slack thread  
**Timing:** Every 2h (P0) / 4h (P1)

```
📋 UPDATE — [INCIDENT_ID] — [Time UTC]

Status: [Containing / Investigating / Resolving / Monitoring]
IC: @[name]

Since last update:
• [Action 1]
• [Action 2]

Open questions:
• [Question needing decision]

Next update: [Time]
```

### Template: Incident Stable — Internal All-Clear

```
Subject: INCIDENT STABLE — [INCIDENT_ID]

The P[P0/P1] incident opened at [time] is now stable.

Summary: [2 sentences]
Customer impact: [refunds issued, comms sent]
Creator impact: [suspensions, reinstatements]
System changes: [hotfixes, kill switches reversed]

Retro scheduled: [Date/time]
Incident doc: [link]

— [IC name]
```

### Template: External Statement (Legal-approved only)

```
[Legal drafts — template structure only]

Marketplate is aware of [general situation]. We take [trust/safety] seriously and have [action taken in plain language].

Affected customers [have been contacted / will receive refunds].

We are cooperating with [authorities if applicable].

Questions: [press contact — Legal provides]
```

---

## Metrics

| Metric | Target |
|--------|--------|
| Time to IC assignment (P0/P1) | ≤ 15 minutes |
| Time to executive notification (P0) | ≤ 30 minutes |
| Time to containment (P0) | ≤ 1 hour |
| Incident resolution time (P0) | ≤ 72 hours to stable |
| Retro completion (post-P0/P1) | Within 5 business days |
| Repeat incident (same root cause, 90d) | 0 |
| Escalation accuracy | % correctly classified — audit sample |
| War room update cadence compliance | 100% for P0 |

→ [Trust Metrics](../../product/success-metrics-overview.md#trust-metrics) · [Platform Health Metrics](../../product/success-metrics-overview.md#platform-health-metrics)

---

## Post-Incident / Retro

**Mandatory for:** All P0/P1; any kill switch activation; any executive notification.

**Participants:** IC, Scribe, Trust Lead, Eng liaison, Legal (if involved), Support Lead, specialized playbook owners.

**Agenda (90 minutes max):**

1. Timeline reconstruction (Scribe doc)
2. Severity classification — was it right?
3. Containment — fast enough? Over-broad?
4. Comms — internal and external adequacy
5. Root cause — people, process, system
6. Action items with DRI and due date
7. Playbook updates required?

**Blameless standard:** Focus on systems improvement. Individual accountability handled separately by managers if required.

---

## Related Documents

### Governance
- [Founding Constitution — Trust Philosophy](../../company/constitution.md#trust-philosophy)
- [Company Values — Using Values in Decisions](../../company/values.md#using-values-in-decisions)
- [Marketplace Mechanics — Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder)

### Engineering
- [Trust Service — Failure modes](../../engineering/services/trust-service.md#failure-modes)
- [Trust Service — Monitoring](../../engineering/services/trust-service.md#monitoring)

### Flows
- [Trust Verification Flow — SLA & Escalation](../../pages/flows/trust-verification-flow.md#sla--escalation)

### Specialized playbooks
- [Food Safety Incident](food-safety-incident.md)
- [Fraud Response](fraud-response.md)
- [Creator Suspension & Offboarding](creator-suspension-offboarding.md)
- [Launching a New Feature](launching-new-feature.md)
- [Launching a New Market](launching-new-market.md)

### Future SOPs
- [Operations SOPs](../../operations/) *(Phase 4)*
