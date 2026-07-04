# Food Safety Incident Response

> End-to-end operational playbook from report through containment, investigation, resolution, and documentation.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook type:** Cross-functional orchestration — **P0 when confirmed or suspected**

---

## Purpose

This playbook orchestrates Marketplate's response when a **food safety incident** is reported or discovered — including allergen mislabeling, contamination, illness claims, unverified production locations, or expired compliance operating without suspension. Food safety incidents directly threaten the trust thesis: [Trust is the product](../../company/values.md#1-trust-is-the-product).

This is not a single support ticket SOP. It coordinates Trust & Safety, Legal, Engineering, Creator Ops, Customer Support, and Communications across order data, verification history, enforcement actions, and customer/creator notifications.

**Governing rules:** [Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder) · [Marketplace Mechanics — Compliance verification](../../product/marketplace-mechanics.md#compliance-verification)

---

## Trigger

| Trigger type | Source | Severity default |
|--------------|--------|------------------|
| **Customer report** | Order Detail → Help, in-app report, support ticket | Medium → High if illness claimed |
| **Allergen dispute post-order** | Order messaging or dispute flow | High |
| **Creator self-report** | Creator messages support or uses "Report issue" on order | Medium |
| **Trust Operator discovery** | Verification review, moderation, compliance expiry audit | Varies |
| **Moderation Assist flag** | Listing with undeclared allergen or prohibited category | Medium |
| **External report** | Health department inquiry, media, social media escalation | High → P0 |
| **Pattern detection** | Multiple reports on same creator/item within 72h | High |

**Immediate P0 triggers:** Confirmed or strongly suspected allergen mislabeling with adverse reaction; illness cluster (≥ 2 reports); health authority contact; creator operating with expired compliance post-grace.

---

## Stakeholders

| Role | Team | Responsibility |
|------|------|----------------|
| **Incident Commander (IC)** | Trust & Safety Lead | Owns timeline, decisions, comms approval |
| **Trust & Safety Operator** | Trust & Safety | Case investigation, evidence collection |
| **Trust & Safety Supervisor** | Trust & Safety | Enforcement decisions, creator suspension |
| **Legal Counsel** | Legal | Regulatory notification obligations, liability framing |
| **Engineering On-Call** | Engineering | Trust Service actions, order/payment holds |
| **Customer Support Lead** | Support | Customer communication, refund coordination |
| **Creator Success** | Creator Ops | Creator notification (non-adversarial cases only — IC approves) |
| **Product** | Product | Customer-facing copy, Help article updates |
| **Communications** | Marketing/Comms | External statements if media/health dept involved |
| **AI Platform** | Engineering | Moderation Assist / Verification Assist audit if AI missed signal |

**War room channel:** `#incident-food-safety` (Slack) — IC creates within 15 minutes of P0/P1 classification.

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Trust Service admin access for suspension actions | `/admin/creators/:creatorId` |
| Dispute Manager operational | `/admin/disputes/:disputeId` |
| Payment Service refund capability | Test refund path in staging |
| Incident log template available | Ops wiki / incident tracker |
| Legal on-call contact list current | PagerDuty / escalation doc |
| Health authority jurisdiction contacts documented | Legal ops binder |
| Platform force-cancel capability tested | Order Service + Payment integration |

**Companion SOP:** [Food Safety Incident SOP](../../operations/food-safety-incident-sop.md)

---

## Phase-by-Phase Execution

### Phase 1 — Triage & Classification (0–30 minutes)

**Goal:** Classify severity, assign IC, protect customers.

| Step | Actor | Action | System / Page |
|------|-------|--------|---------------|
| 1.1 | First responder (Support or Trust) | Log incident with order ID, creator ID, reporter type, symptom description | Support ticket tagged `food-safety` |
| 1.2 | Trust Operator | Pull order context: items, allergens declared, customer notes, message thread | [Order Detail](../../pages/customer/order-detail.md) · Creator [Order Detail](../../pages/creator/order-detail.md) |
| 1.3 | Trust Operator | Pull creator verification history: kitchen, compliance status, prior warnings | [Creator Admin Detail](../../pages/admin/creator-admin-detail.md) |
| 1.4 | IC | Classify severity: **P0** · **P1** · **P2** | Incident tracker |
| 1.5 | IC (P0/P1) | Open war room; notify Legal + Engineering on-call | `#incident-food-safety` |

**Severity matrix:**

| Level | Criteria | Response time |
|-------|----------|---------------|
| **P0** | Illness/hospitalization claimed; confirmed allergen exposure; health dept contact | Immediate containment |
| **P1** | Allergen mislabeling suspected; multiple reports; operating out of compliance | Containment within 1 hour |
| **P2** | Single quality complaint; minor labeling inconsistency; no health claim | Standard dispute path within 24h |

---

### Phase 2 — Containment (P0/P1: 0–2 hours)

**Goal:** Stop ongoing harm; preserve evidence.

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 2.1 | Trust Supervisor | **Suspend creator** — orders + listings | Trust Service: emit `creator.suspended`; Catalog suspends listings; Order blocks new orders |
| 2.2 | Trust Operator | **Suspend affected listing(s)** if incident is item-specific | Moderation action on catalog item |
| 2.3 | Trust Operator | **Force-cancel active orders** if safety risk to pending customers | Order Service platform cancel → full refund |
| 2.4 | Engineering | Verify event propagation: Catalog, Payment (payout hold), Discovery removal | Monitor `creator.suspended` consumers |
| 2.5 | Support | Contact affected customers with active orders — cancellation + full refund notice | Notification Service |
| 2.6 | Trust Operator | Preserve evidence: order snapshot, listing version at time of order, message thread, verification docs | Audit log export; no document deletion |
| 2.7 | Legal (P0) | Assess regulatory notification requirements for jurisdiction | External comms hold until Legal approves |

**Containment checklist (IC signs off):**

- [ ] Creator suspended or listing removed
- [ ] Active orders handled (cancel/refund or case-by-case IC decision)
- [ ] Payout hold applied
- [ ] Evidence preserved with timestamps
- [ ] Customer(s) acknowledged within SLA

---

### Phase 3 — Investigation (2–72 hours)

**Goal:** Determine facts; inform enforcement and remediation.

| Step | Actor | Action |
|------|-------|--------|
| 3.1 | Trust Operator | Interview reporter (customer) — structured questionnaire: items consumed, symptoms, timing, medical care | Support script |
| 3.2 | Trust Operator | Interview creator — production details, ingredient sources, batch info, label accuracy | Record in dispute case |
| 3.3 | Trust Operator | Compare listing allergens/ingredients at order time vs. current vs. verification docs | Catalog version history |
| 3.4 | Trust Operator | Review AI flags: did Verification Assist or Moderation Assist surface prior signals? | Case + `ai_flags_json` audit |
| 3.5 | Trust Supervisor | Cross-reference creator enforcement history | Creator Admin Detail → Enforcement tab |
| 3.6 | Legal | Determine if health department report required; coordinate if external inquiry received | Legal decision log |
| 3.7 | IC | Daily status update in war room until investigation complete | Incident tracker |

**Investigation outcomes:**

| Finding | Typical enforcement |
|---------|---------------------|
| Confirmed allergen mislabeling | Suspension → [Creator Suspension playbook](creator-suspension-offboarding.md) |
| Unverified/expired compliance operation | Suspension + compliance re-verification required |
| Customer error / unsubstantiated claim | No creator action; document and close |
| Creator negligence (non-allergen) | Warning or listing restriction per ladder |
| Intentional fraud | Permanent removal — [Fraud Response](fraud-response.md) |
| Platform defect (wrong allergen displayed) | Engineering fix + customer remediation; no creator penalty |

---

### Phase 4 — Resolution & Remediation (72 hours – 14 days)

| Step | Actor | Action |
|------|-------|--------|
| 4.1 | Trust Supervisor | Final enforcement decision with required rationale (min 20 chars) | Trust Service audit log |
| 4.2 | Support | Customer resolution: refund (if not already), credit, apology per IC/Legal approval | Payment Service |
| 4.3 | Creator Success (if reinstatement path) | Creator remediation plan: re-verification, label correction, training | Only if IC approves outreach |
| 4.4 | Product | Update Help articles if systemic UX gap identified | `/help` content |
| 4.5 | Trust Ops | If compliance template gap: update jurisdiction rules in Platform Settings | Compliance Engine |
| 4.6 | IC | Close incident; transition to retro scheduling | Status → Resolved |

**Reinstatement criteria (if applicable):**

- Root cause addressed with evidence (corrected listing, renewed compliance, kitchen re-verification)
- No P0 findings of intentional misconduct
- Trust Supervisor + Legal sign-off
- See [Creator Suspension & Offboarding — Reinstatement](creator-suspension-offboarding.md)

---

### Phase 5 — Documentation & Follow-Through

| Step | Actor | Action |
|------|-------|--------|
| 5.1 | Trust Operator | Complete incident report: timeline, evidence, decisions, customer/creator comms | Immutable incident record |
| 5.2 | Trust & Safety | Update enforcement record on creator profile | Creator Admin Detail |
| 5.3 | Engineering | File bugs for any system failures (capacity, allergen display, notification gaps) | Engineering tracker |
| 5.4 | AI Platform | If AI miss: eval pipeline review, gold set update | [Verification Assist](../../ai/verification-assist.md) / [Moderation Assist](../../ai/moderation-assist.md) |
| 5.5 | All | Schedule retro within 5 business days of close | See Post-Incident section |

---

## Decision Points

| Decision | Owner | Options | Default |
|----------|-------|---------|---------|
| P0 vs. P1 classification | IC | Escalate · De-escalate with documented rationale | Escalate when illness claimed |
| Suspend creator vs. listing only | Trust Supervisor | Full suspension · Listing restriction · Monitor | Full suspension on P0/P1 allergen or illness |
| Refund active orders not yet fulfilled | IC | Force-cancel all · Case-by-case | Force-cancel all on P0 |
| Notify health department | Legal | Required · Not required · Monitor | Legal decides per jurisdiction |
| Creator reinstatement | Trust Lead + Legal | Re-verify · Permanent removal · Appeal path | No reinstatement on confirmed intentional mislabeling |
| Public statement | Comms + Legal | Statement · No comment · Direct inquiry response only | No public statement without Legal approval |
| Platform bug vs. creator fault | IC + Engineering | Creator enforcement · Platform fix only · Both | Evidence-based; never punish creator for platform defect |

---

## Communication Templates

### Template: Customer Acknowledgment (Initial)

**Channel:** Email  
**Owner:** Support  
**Timing:** Within 2 hours of report (P0/P1)

```
Subject: We're looking into your report — Order #[ORDER_ID]

Hi [Customer first name],

Thank you for reporting this. Your safety matters to us, and we're taking your report seriously.

We've opened an investigation and may temporarily pause orders from this creator while we review.

If you're experiencing a medical emergency, please contact emergency services or your healthcare provider.

A member of our team will follow up within [24 hours / 4 hours for P0].

Reference: Incident [INCIDENT_ID]

— Marketplate Trust & Safety
```

### Template: Customer Resolution — Refund

**Channel:** Email  
**Trigger:** Investigation complete; refund issued

```
Subject: Update on your report — Order #[ORDER_ID]

Hi [Customer first name],

We've completed our review of your report regarding Order #[ORDER_ID].

[Summary of finding — plain language, no legal admission unless Legal approved]

We've issued a full refund of [AMOUNT] to your original payment method. Please allow 5–10 business days for processing.

If you have additional concerns, reply with reference [INCIDENT_ID].

— Marketplate Trust & Safety
```

### Template: Creator Suspension (Safety)

**Channel:** Email + in-app  
**Owner:** Trust & Safety (not Creator Success)

```
Subject: Your Marketplate account has been temporarily suspended

Hi [Creator first name],

We've temporarily suspended your account pending investigation of a food safety report related to Order #[ORDER_ID].

During suspension:
• Your listings are hidden
• You cannot accept new orders
• Active orders [have been cancelled and refunded / are being handled individually]

We will contact you within [72 hours] with next steps. Do not fulfill any pending orders unless explicitly instructed.

Case ID: [INCIDENT_ID]

If you believe this is an error, you may submit an appeal via Help with your case ID.
```

### Template: Internal — P0 War Room Open

**Channel:** Slack `#incident-food-safety`

```
🚨 FOOD SAFETY P0 — IC: @[name]

Incident ID: [INCIDENT_ID]
Creator: [Name] / [creator_id]
Order: #[ORDER_ID]
Report: [Illness / Allergen / Other]
Reporter: Customer [customer_id]

Actions taken:
• [ ] Creator suspended
• [ ] Active orders cancelled
• [ ] Legal notified
• [ ] Evidence preserved

War room: this thread
Next update: [time]
```

---

## Metrics

| Metric | Definition | Target |
|--------|------------|--------|
| Time to containment (P0/P1) | Report → creator suspended | ≤ 1 hour |
| Customer acknowledgment time | Report → first customer reply | ≤ 2 hours (P0/P1) |
| Investigation completion time | Report → resolution decision | ≤ 72 hours (P1); ≤ 24 hours (P0) |
| Repeat incident rate | Same creator, same category within 90d | 0 |
| False suspension rate | Suspensions overturned on appeal / total | Track; minimize |
| Allergen dispute rate | Allergen disputes / completed orders | ↓ |
| Compliance expiry incidents | Orders while expired compliance | 0 (system should prevent) |

→ [Trust Metrics](../../product/success-metrics-overview.md#trust-metrics)

---

## Post-Incident / Retro

**Required for:** All P0/P1 incidents; any incident resulting in creator permanent removal; any platform bug contributing to incident.

**Retro agenda (60 minutes):**

1. **Timeline review** — report → containment → investigation → resolution
2. **What went well** — detection, response speed, comms
3. **What went wrong** — gaps in verification, listing review, system enforcement
4. **Root cause** — 5 Whys; distinguish creator fault, platform fault, process fault
5. **Action items** — owners, due dates, doc updates
6. **Regulatory review** — Legal confirms notification obligations met

**Outputs:**

| Output | Owner |
|--------|-------|
| Updated SOP in `operations/` | Trust & Safety |
| Platform Settings / compliance rule change | Trust Ops + Legal |
| Engineering fix or monitoring alert | Engineering |
| AI eval benchmark update | AI Platform |
| Help article / checkout copy change | Product + Support |
| This playbook amendment | Trust Lead |

---

## Related Documents

### Flows & mechanics
- [Order Fulfillment Flow — Edge cases](../../pages/flows/order-fulfillment-flow.md#edge-cases)
- [Marketplace Mechanics — Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder)
- [Customer Purchase Flow — Allergen acknowledgment](../../pages/flows/customer-purchase-flow.md#phase-3--menu-item-detail)

### Engineering & admin
- [Trust Service](../../engineering/services/trust-service.md)
- [Creator Admin Detail](../../pages/admin/creator-admin-detail.md)
- [Dispute Detail](../../pages/admin/dispute-detail.md)
- [Moderation Queue](../../pages/admin/moderation-queue.md)

### AI
- [Moderation Assist](../../ai/moderation-assist.md)
- [Verification Assist](../../ai/verification-assist.md)

### Policy
- [Company Values](../../company/values.md)
- [Trust & Safety Standards](../standards/trust-and-safety-standards.md) *(when published)*

### Related playbooks
- [Trust & Safety Escalation](trust-safety-escalation.md)
- [Creator Suspension & Offboarding](creator-suspension-offboarding.md)
- [Fraud Response](fraud-response.md)
