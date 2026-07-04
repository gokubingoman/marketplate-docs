# Food Safety Incident SOP

> Standard Operating Procedure for P0/P1 allergen, illness, and food safety incidents. **Contain first; human commands all enforcement.** — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook companion:** [Food Safety Incident Response](../docs/playbooks/food-safety-incident.md) *(orchestration)* · [Creator Suspension & Offboarding](../docs/playbooks/creator-suspension-offboarding.md)

---

## Purpose

This SOP defines Trust & Safety operator procedures for food safety incidents — allergic reactions, foodborne illness claims, allergen mislabeling, contamination, and unverified/expired compliance operation. Food safety is P0/P1 priority because [Trust is the product](../company/values.md#1-trust-is-the-product).

This SOP is the **operator execution layer** for the cross-functional [Food Safety Incident playbook](../docs/playbooks/food-safety-incident.md). AI systems flag signals; **humans classify severity, suspend accounts, and authorize refunds**.

---

## Trigger

| Trigger | Source | Default severity |
|---------|--------|------------------|
| Customer reports illness after order | Support ticket, in-app report, dispute | P0 if hospitalization; P1 otherwise |
| Allergen reaction claimed | Order help, dispute, messaging | **P0** if adverse reaction; **P1** if suspected mislabeling |
| Allergen dispute post-order | [Dispute Detail](../pages/admin/dispute-detail.md) | P1 |
| Multiple reports same creator/item (72h) | Pattern detection | P1 |
| [Moderation Assist](../ai/moderation-assist.md) — undeclared allergen | [Moderation Queue](../pages/admin/moderation-queue.md) | P1 |
| Trust Operator discovers expired compliance with active orders | Compliance audit | P1 |
| Health department inquiry | External | **P0** |
| Creator self-reports batch issue | Creator support | P1 |

**Immediate P0 triggers:** Confirmed or strongly suspected allergen mislabeling with adverse reaction; illness cluster (≥ 2 reports); health authority contact; creator operating with expired compliance post-grace.

---

## Owner

| Role | Responsibility |
|------|----------------|
| **Incident Commander (IC)** | Trust & Safety Lead — timeline, decisions, comms approval |
| **Trust & Safety Operator** | Investigation, evidence preservation, customer/creator contact |
| **Trust & Safety Supervisor** | Containment actions — suspend, force-cancel |
| **Legal Counsel** | Regulatory notification, liability framing |
| **Customer Support Lead** | Customer acknowledgment and resolution comms |
| **Engineering On-Call** | Event propagation verification, evidence export |

**War room:** `#incident-food-safety` (Slack) — IC creates within 15 minutes of P0/P1 classification per playbook.

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Trust Service admin — suspend creator | [Creator Admin Detail](../pages/admin/creator-admin-detail.md) |
| Force-cancel capability | Order Service + Payment integration tested |
| [Dispute Detail](../pages/admin/dispute-detail.md) operational | Refund path verified |
| Legal on-call contact current | Escalation doc |
| Incident log template | Ops wiki / incident tracker |
| IC designation for shift | Trust Lead coverage calendar |
| Familiarity with playbook Phase 1–5 | [Food Safety Incident playbook](../docs/playbooks/food-safety-incident.md) |

Operators must not delay containment waiting for AI processing.

---

## Workflow

### Phase 1 — Triage & classification (0–30 minutes)

| Step | Actor | Action |
|------|-------|--------|
| 1.1 | First responder | Log incident: order ID, creator ID, reporter type, symptoms — tag `food-safety` |
| 1.2 | Trust Operator | Pull order: items, allergens declared, customer notes, messages | Order Detail |
| 1.3 | Trust Operator | Pull creator: verification, compliance status, prior warnings | [Creator Admin Detail](../pages/admin/creator-admin-detail.md) |
| 1.4 | IC | Classify **P0** · **P1** · **P2** using severity matrix below |
| 1.5 | IC (P0/P1) | Open war room; notify Legal + Engineering on-call | `#incident-food-safety` |

**Severity matrix:**

| Level | Criteria | Response time |
|-------|----------|---------------|
| **P0** | Illness/hospitalization; confirmed allergen exposure; health dept contact | Immediate containment |
| **P1** | Allergen mislabeling suspected; multiple reports; out-of-compliance operation | Containment ≤ 1 hour |
| **P2** | Single quality complaint; minor labeling inconsistency; no health claim | Route to [Dispute Resolution SOP](dispute-resolution-sop.md) within 24h |

**Human approval gate:** IC confirms P0/P1 classification — AI severity suggestions are advisory only.

### Phase 2 — Containment (P0/P1: 0–2 hours)

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 2.1 | Trust Supervisor | **Suspend creator** — orders + listings | `creator.suspended` via Trust Service |
| 2.2 | Trust Operator | Suspend affected listing(s) if item-specific | Moderation → Catalog |
| 2.3 | Trust Operator | **Force-cancel active orders** if ongoing risk | Order Service → full refund |
| 2.4 | Engineering | Verify Catalog, Payment (payout hold), Discovery consumed event | Monitor dashboards |
| 2.5 | Support | Notify affected customers — cancellation + refund notice | Notification Service |
| 2.6 | Trust Operator | Preserve evidence: order snapshot, listing version, messages, verification docs | Audit export — no deletion |
| 2.7 | Legal (P0) | Assess regulatory notification requirements | Hold external comms until approved |

**Containment checklist (IC sign-off):**

- [ ] Creator suspended or listing removed
- [ ] Active orders handled (cancel/refund or IC case-by-case)
- [ ] Payout hold applied
- [ ] Evidence preserved with timestamps
- [ ] Customer(s) acknowledged within SLA

Use [Creator Suspension SOP](creator-suspension-sop.md) for active order matrix details.

### Phase 3 — Investigation (2–72 hours)

| Step | Actor | Action |
|------|-------|--------|
| 3.1 | Trust Operator | Customer interview — structured questionnaire: items, symptoms, timing, medical care |
| 3.2 | Trust Operator | Creator interview — production, ingredients, batch, label accuracy |
| 3.3 | Trust Operator | Compare listing allergens at order time vs. current vs. verification docs |
| 3.4 | Trust Operator | Review AI flags: [Verification Assist](../ai/verification-assist.md) / [Moderation Assist](../ai/moderation-assist.md) prior signals |
| 3.5 | Trust Supervisor | Cross-reference enforcement history |
| 3.6 | Legal | Health department report determination |
| 3.7 | IC | Daily war room update until complete |

**Investigation outcomes → enforcement:**

| Finding | Enforcement |
|---------|-------------|
| Confirmed allergen mislabeling | Suspension → [Creator Suspension SOP](creator-suspension-sop.md) |
| Expired/unverified compliance operation | Suspension + re-verification required |
| Unsubstantiated claim | Document; no creator penalty |
| Creator negligence (non-allergen) | Warning or listing restriction per ladder |
| Intentional fraud | Permanent removal — [Fraud Response](../docs/playbooks/fraud-response.md) |
| Platform defect (wrong allergen displayed) | Engineering fix + customer remediation; **no creator penalty** |

### Phase 4 — Resolution (72 hours – 14 days)

| Step | Actor | Action |
|------|-------|--------|
| 4.1 | Trust Supervisor | Final enforcement with rationale (min 20 chars) | Trust Service audit |
| 4.2 | Support / Trust | Customer resolution: refund, credit, apology per IC/Legal | [Refund Processing SOP](refund-processing-sop.md) |
| 4.3 | Trust Ops | Update jurisdiction rules if template gap | [Platform Settings](../pages/admin/platform-settings.md) |
| 4.4 | IC | Close incident → schedule retro | Status: Resolved |

Reinstatement criteria: root cause addressed, no intentional misconduct P0, Trust Supervisor + Legal sign-off — see playbook Phase 4.

---

## AI Responsibilities

AI **flags and prioritizes** — never contains or resolves incidents:

| System | Role | Autonomous? |
|--------|------|-------------|
| [Moderation Assist](../ai/moderation-assist.md) | Undeclared allergen, prohibited food imagery | Flags only — hold listing for human review |
| [Verification Assist](../ai/verification-assist.md) | Compliance doc expiry, kitchen mismatch | Flags only |
| Risk scoring | Pattern: multiple reports same creator | Signal only |
| Incident classification | **Not in v1** | IC human classifies P0/P1/P2 |
| Suspend creator / force-cancel | **Never** |
| Customer/creator notification | **Never** without human-triggered templates |
| Regulatory notification | **Never** — Legal only |

Post-incident: if AI missed signal, AI Platform reviews eval pipeline per playbook Phase 5.

---

## Human Responsibilities

| Action | Human requirement |
|--------|-------------------|
| P0/P1 classification | IC decision |
| Creator suspension | Trust Supervisor executes |
| Force-cancel orders | Trust Supervisor / IC |
| Refund authorization | Trust + Support per [Refund Processing SOP](refund-processing-sop.md) |
| Customer acknowledgment | Support within 2h (P0/P1) |
| Creator safety suspension comms | Trust & Safety only — not Creator Success |
| Health department notification | Legal decision |
| Final enforcement | Trust Supervisor + rationale |
| Reinstatement | Trust Lead + Legal |
| Public statement | Comms + Legal approval |

**Default:** Escalate when illness claimed — do not de-escalate without documented rationale.

---

## Escalation Rules

| Condition | Escalate to | Timeline |
|-----------|-------------|----------|
| Illness/hospitalization claimed | IC + P0 war room | Immediate |
| Health department contact | Legal + IC | Immediate |
| Containment not executed within 1h (P1) | Trust Lead | Immediate |
| Engineering event propagation failure | Engineering on-call P1 | Immediate |
| Media/social escalation | Comms + Legal | Per [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Platform bug contributed | Engineering IC | Parallel track |
| Repeat incident same creator (90d) | Trust Lead — permanent removal review | Same day |
| Regulatory notification uncertainty | Legal | Before external contact |

Founder escalation for policy exceptions: `TODO(decision):` per playbook.

---

## SLA

| Milestone | P0 | P1 | P2 |
|-----------|----|----|-----|
| IC assigned | 15 min | 30 min | N/A |
| Containment (suspend) | Immediate | ≤ 1 hour | N/A |
| Customer acknowledgment | ≤ 2 hours | ≤ 2 hours | ≤ 24 hours |
| Investigation complete | ≤ 24 hours | ≤ 72 hours | ≤ 3 BD (dispute path) |
| Customer resolution (refund) | ≤ 24 hours | ≤ 72 hours | Per dispute SLA |
| Retro scheduled | ≤ 5 BD from close | ≤ 5 BD | If pattern |

→ Playbook [Metrics](../docs/playbooks/food-safety-incident.md#metrics)

---

## Audit Logging

| Event | Required fields |
|-------|-----------------|
| `incident.opened` | `incident_id`, `order_id`, `creator_id`, `severity`, `reporter_type`, `ic_id`, `timestamp` |
| `creator.suspended` | `operator_id`, `creator_id`, `incident_id`, `rationale`, `reason_code` |
| `order.force_cancelled` | `operator_id`, `order_id`, `incident_id`, `refund_id` |
| `evidence.preserved` | `operator_id`, `artifact_ids[]`, `timestamp` |
| `incident.resolved` | `ic_id`, `finding`, `enforcement_action`, `customer_resolution`, `timestamp` |
| AI flag review | `operator_id`, `case_id`, `ai_flags_reviewed`, `miss_noted` |

Immutable incident record separate from dispute case — linked by IDs. Evidence retention per [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md#evidence-preservation): order snapshot life of dispute + 7 years.

All document access logged. Audit write failure blocks enforcement actions.

---

## Resolution

Incident **resolved** when:

1. Containment complete and verified
2. Investigation finding documented
3. Final enforcement applied (if any)
4. Customer resolution executed (refund/credit/communication)
5. Creator notified (suspension/resolution template)
6. IC closes incident tracker entry
7. Retro scheduled (P0/P1 mandatory)

| Finding | Typical end state |
|---------|-------------------|
| Confirmed mislabeling | Creator suspended pending [Creator Suspension SOP](creator-suspension-sop.md); customers refunded |
| Unsubstantiated | Creator reinstated if suspended; incident documented |
| Platform defect | Engineering fix ticket; customers remediated |
| Fraud | Permanent removal path |

P2 incidents may resolve via [Dispute Resolution SOP](dispute-resolution-sop.md) without full incident record — IC discretion.

---

## Post Mortem

**Required for:** All P0/P1; any permanent removal; any platform bug contribution.

**Agenda (60 min, within 5 business days)** — per [playbook retro section](../docs/playbooks/food-safety-incident.md#post-incident--retro):

1. Timeline: report → containment → investigation → resolution
2. What went well / what went wrong
3. Root cause — 5 Whys (creator fault, platform fault, process fault)
4. Action items with owners
5. Regulatory review — Legal confirms obligations met
6. AI miss review if applicable

**Outputs:** SOP update, Platform Settings change, engineering fix, AI eval update, Help article change.

---

## Metrics

| Metric | Target |
|--------|--------|
| Time to containment (P0/P1) | ≤ 1 hour |
| Customer acknowledgment (P0/P1) | ≤ 2 hours |
| Investigation completion (P0) | ≤ 24 hours |
| Investigation completion (P1) | ≤ 72 hours |
| Repeat incident rate (same creator, 90d) | 0 |
| Orders while expired compliance | 0 (system should prevent) |
| False suspension overturned on appeal | Track — minimize |
| Allergen dispute rate | ↓ |

→ [Success Metrics — Trust](../product/success-metrics-overview.md#trust-metrics)

---

## Future Automation

| Initiative | Human gate preserved |
|------------|---------------------|
| Allergen-specific dispute checklist auto-populated | Operator completes investigation |
| Pattern detection alerts (≥ 2 reports / 72h) | IC classifies |
| Automated evidence snapshot on P0 trigger | Human confirms severity first |
| Compliance expiry hard block (prevent orders) | Engineering — reduces incidents |
| Health authority contact registry by jurisdiction | Legal maintains; human notifies |
| AI incident classification assist | Advisory only — IC decides |

**Never automate:** Suspension, force-cancel, regulatory notification, or customer resolution without human approval.

---

## Related Documents

- [Food Safety Incident playbook](../docs/playbooks/food-safety-incident.md)
- [Creator Suspension SOP](creator-suspension-sop.md)
- [Dispute Resolution SOP](dispute-resolution-sop.md)
- [Refund Processing SOP](refund-processing-sop.md)
- [Moderation SOP](moderation-sop.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Moderation Assist](../ai/moderation-assist.md)
- [Verification Assist](../ai/verification-assist.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
- [Creator Admin Detail](../pages/admin/creator-admin-detail.md)
