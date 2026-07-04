# Creator Suspension & Offboarding

> End-to-end operational playbook for enforcement, voluntary departure, appeals, and reinstatement.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook type:** Cross-functional orchestration

---

## Purpose

This playbook orchestrates **creator account suspension, restriction, permanent removal, and voluntary offboarding** — including customer impact mitigation, payout handling, appeals, and reinstatement. It implements the [Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder):

```
Education → Warning → Listing restriction → Order suspension → Account suspension → Permanent removal
```

Suspension is a high-stakes action requiring human approval, documented rationale, and immutable audit trails — [Trust Service security](../../engineering/services/trust-service.md#security). AI may flag; humans enforce — [Moderation Assist](../../ai/moderation-assist.md).

**Related specialized playbooks:** [Food Safety Incident](food-safety-incident.md) · [Fraud Response](fraud-response.md) · [Trust & Safety Escalation](trust-safety-escalation.md)

---

## Trigger

| Trigger type | Source | Typical enforcement level |
|--------------|--------|---------------------------|
| **Trust enforcement ladder** | Pattern of disputes, warnings exhausted | Account suspension |
| **Food safety incident** | Confirmed allergen mislabeling, illness | Account suspension → permanent removal |
| **Fraud confirmation** | [Fraud Response](fraud-response.md) complete | Permanent removal |
| **Compliance expiry post-grace** | Compliance Engine scheduled job | Listing restriction → order suspension |
| **Moderation decision** | Policy violation on listing/review/message | Warning → listing restriction |
| **Voluntary creator request** | Creator closes business | Offboarding |
| **Platform policy violation** | Unresolved policy breach after education | Escalating enforcement |
| **Legal requirement** | Court order, regulatory mandate | Per Legal direction |

**Automatic system actions (not human suspension):**

- `compliance.expired` post-grace → Catalog suspends listings ([Trust Service data flow](../../engineering/services/trust-service.md#compliance-expiry))
- These are restrictions, not full account suspension — operator may escalate

---

## Stakeholders

| Role | Team | Responsibility |
|------|------|----------------|
| **Trust Supervisor** | Trust & Safety | Suspension/removal approval |
| **Trust Operator** | Trust & Safety | Case documentation, customer order review |
| **Trust Lead** | Trust & Safety | Permanent removal, appeal decisions, reinstatement |
| **Legal Counsel** | Legal | Regulatory orders, appeal liability |
| **Finance** | Finance | Payout holds, final payout, clawback |
| **Engineering On-Call** | Engineering | Event propagation verification |
| **Customer Support** | Support | Customer notifications, refund execution |
| **Creator Success** | Creator Ops | Voluntary offboarding support only — not enforcement comms |

**Separation rule:** Creator Success does not communicate enforcement actions. Trust & Safety owns all suspension/removal messaging.

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Rationale required on all enforcement actions (min 20 chars) | Trust Service API validation |
| Reason codes configured | `document_invalid`, `fraud_suspected`, `policy_violation`, etc. |
| Appeal workflow documented in Help | `/help` creator appeals article |
| Payout hold capability | Payment Service |
| Creator Admin Detail quick actions tested | `/admin/creators/:creatorId` |
| Audit log immutability | No mutating action on audit failure |

---

## Enforcement Levels

| Level | Creator impact | Customer impact | Reversible |
|-------|----------------|-----------------|------------|
| **Education** | In-app notice, no functional block | None | N/A |
| **Warning** | Documented on enforcement tab | None | Yes |
| **Listing restriction** | Affected listings hidden | Cannot purchase restricted items | Yes |
| **Order suspension** | Cannot accept new orders; listings may remain visible | Cannot checkout | Yes |
| **Account suspension** | Listings hidden; orders blocked; dashboard limited | Active orders handled per playbook | Yes, with review |
| **Permanent removal** | Account deactivated; storefront removed | Refunds per policy | No — appeal exception only |

---

## Phase-by-Phase Execution

### Track A — Involuntary Suspension / Removal

#### Phase A1 — Case Preparation

| Step | Actor | Action | System |
|------|-------|--------|--------|
| A1.1 | Trust Operator | Confirm enforcement level per ladder history | Creator Admin Detail → Enforcement tab |
| A1.2 | Trust Operator | Review: verification history, disputes, moderation, AI flags | Full case file |
| A1.3 | Trust Operator | Identify active orders and pending payouts | Order Service · Payment Service |
| A1.4 | Trust Supervisor | Approve enforcement level and rationale | Sign-off before action |
| A1.5 | Trust Operator | For P0 safety/fraud: invoke specialized playbook first | [Food Safety](food-safety-incident.md) / [Fraud](fraud-response.md) |

---

#### Phase A2 — Execute Enforcement

| Step | Actor | Action | System |
|------|-------|--------|--------|
| A2.1 | Trust Supervisor | Apply enforcement action with reason code + rationale | Trust Service admin API |
| A2.2 | System | Emit events per level | See event table below |
| A2.3 | Engineering | Verify consumers processed: Catalog, Order, Payment, Discovery | Monitor dashboards |
| A2.4 | Trust Operator | Handle active orders (see decision matrix) | Order force-cancel or fulfill |
| A2.5 | Finance | Apply payout hold or process final payout per policy | Payment Service |
| A2.6 | Support | Notify affected customers | Notification Service |
| A2.7 | Trust & Safety | Notify creator — enforcement template | Email + in-app |

**Trust Service events by level:**

| Level | Event | Consumers |
|-------|-------|-----------|
| Listing restriction | `moderation.decided` | Catalog |
| Order / account suspension | `creator.suspended` | Catalog, Order, Payment, Discovery |
| Permanent removal | `creator.suspended` + account deactivate | All + Identity |
| Reinstatement | `creator.reinstated` | Catalog, Payment |

→ [Trust Service — Events](../../engineering/services/trust-service.md#events)

---

#### Phase A3 — Active Order Handling

| Scenario | Action | Refund |
|----------|--------|--------|
| Safety suspension (P0/P1) | Force-cancel all active orders | Full refund |
| Fraud confirmed | Force-cancel all | Full refund |
| Compliance expiry | Allow fulfill existing; block new | N/A for existing |
| Policy suspension — orders fulfillable safely | Creator completes OR platform cancels | Per case — IC/Supervisor |
| Customer-initiated dispute open | Resolve dispute before close | Per dispute outcome |

→ [Order Fulfillment Flow — Cancelled](../../pages/flows/order-fulfillment-flow.md#state-7--cancelled--refunded)

---

#### Phase A4 — Appeals (if eligible)

| Step | Actor | Action |
|------|-------|--------|
| A4.1 | Creator | Submits appeal via Help with case ID within appeal window (`TODO(decision):` window length) |
| A4.2 | Support | Triage appeal ticket → Trust queue — not Creator Success |
| A4.3 | Trust Operator (different from original if possible) | Review new evidence; full case re-read |
| A4.4 | Trust Lead | Appeal decision: uphold · reinstate · modify enforcement |
| A4.5 | Trust & Safety | Notify creator of appeal outcome |
| A4.6 | System | If reinstated: `creator.reinstated`; restore listings per compliance status | 

**Non-appealable:** Confirmed fraudulent identity; permanent removal with Legal hold.

---

#### Phase A5 — Reinstatement (if approved)

| Step | Actor | Action |
|------|-------|--------|
| A5.1 | Trust Lead | Define reinstatement conditions: re-verification, compliance renewal, listing corrections |
| A5.2 | Creator | Complete required remediation |
| A5.3 | Trust Operator | Verify remediation; re-run verification checklists if needed |
| A5.4 | Trust Supervisor | Approve reinstatement with rationale |
| A5.5 | System | `creator.reinstated`; Catalog restores eligible listings |
| A5.6 | Finance | Release payout hold per policy |
| A5.7 | Creator Success | **May** engage post-reinstatement for activation support — IC/Trust Lead approves |

**Reinstatement blocked when:**

- Permanent removal for fraud
- Unaddressed food safety root cause
- Active legal order prohibiting operation

---

### Track B — Voluntary Offboarding

#### Phase B1 — Creator Initiated

| Step | Actor | Action |
|------|-------|--------|
| B1.1 | Creator | Requests account closure via Help or dashboard setting (future) |
| B1.2 | Creator Success | Confirm intent; explain impact: listings, orders, payouts, data retention |
| B1.3 | Creator Success | Offer alternatives: pause availability, seasonal closure before full close |
| B1.4 | Creator | Confirms closure request in writing |

---

#### Phase B2 — Order & Payout Wind-Down

| Step | Actor | Action |
|------|-------|--------|
| B2.1 | Creator Success | Creator completes or cancels all active orders |
| B2.2 | System | Block new orders — voluntary closure flag |
| B2.3 | Finance | Process final payout after order completion + dispute window |
| B2.4 | Creator | Export data if available (orders, customers per policy) |
| B2.5 | Trust Ops | Retain verification documents per retention policy — Legal |

---

#### Phase B3 — Account Deactivation

| Step | Actor | Action |
|------|-------|--------|
| B3.1 | Trust Operator | Deactivate account; hide storefront | Not "permanent removal" unless creator requests no return |
| B3.2 | System | Listings removed from Discovery; slug reserved or released per policy |
| B3.3 | Creator Success | Send offboarding confirmation with reactivation path if applicable |
| B3.4 | Marketing | Remove from featured collections |

**Voluntary vs. involuntary:** Voluntary offboarding preserves appeal/reactivation path by default. No enforcement stigma on profile.

---

## Decision Points

| Decision | Owner | Options | Default |
|----------|-------|---------|---------|
| Enforcement level | Trust Supervisor | Per ladder matrix | Lowest effective level — escalate if insufficient |
| Force-cancel active orders | Trust Supervisor / IC | All · Complete safe orders · Case-by-case | Force-cancel on safety/fraud |
| Payout release on suspension | Finance + Trust Lead | Hold · Partial · Release earned | Hold pending investigation |
| Appeal eligibility | Trust Lead | Allow · Deny | Deny for confirmed fraud |
| Reinstatement | Trust Lead | Full · Conditional · Deny | Conditional with re-verification |
| Voluntary close with open orders | Creator Success | Complete first · Cancel with refunds | Complete first |
| Public creator dispute (social media) | Trust Lead + Comms | Escalate — [Trust & Safety Escalation](trust-safety-escalation.md) | Escalate at P1 |

---

## Communication Templates

### Template: Warning (Enforcement Ladder)

**Owner:** Trust & Safety  
**Channel:** Email + in-app

```
Subject: Important notice about your Marketplate account

Hi [Creator first name],

We've identified [issue — specific, plain language] on your account.

This is a warning. Your account remains active, but continued issues may result in listing restrictions or suspension.

Required action:
• [Specific step by date if applicable]

Reference: [CASE_ID]

Help center: [link]

— Marketplate Trust & Safety
```

### Template: Account Suspension

**Owner:** Trust & Safety  
**Channel:** Email + in-app

```
Subject: Your Marketplate account has been suspended

Hi [Creator first name],

We've suspended your account due to [general category — policy violation / safety review / compliance issue].

What this means:
• Your storefront is hidden
• You cannot accept new orders
• [Active orders: cancelled and refunded / please complete existing orders — per case]

Case ID: [CASE_ID]

If you believe this is an error, you may submit an appeal within [N days]: [Help link]

— Marketplate Trust & Safety
```

### Template: Permanent Removal

**Owner:** Trust & Safety  
**Channel:** Email

```
Subject: Your Marketplate account has been closed

Hi [Creator first name],

We've permanently closed your account for violations of our [Seller Agreement / Trust policies].

Case ID: [CASE_ID]

[Appeal sentence if eligible / removal of appeal if not]

— Marketplate Trust & Safety
```

### Template: Reinstatement Approved

**Owner:** Trust & Safety  
**Channel:** Email + in-app

```
Subject: Your account has been reinstated

Hi [Creator first name],

After reviewing your appeal (Case [CASE_ID]), we've reinstated your account.

Before accepting orders:
• [Any remaining conditions — e.g., update compliance doc by DATE]

[Go to dashboard →]

— Marketplate Trust & Safety
```

### Template: Voluntary Offboarding Confirmation

**Owner:** Creator Success  
**Channel:** Email

```
Subject: Your Marketplate account closure is complete

Hi [Creator first name],

Your account closure is complete as requested.

• Final payout: [AMOUNT] — expected [date]
• Your storefront is no longer visible
• Verification records retained per our privacy policy

We're grateful you were part of Marketplate. If you return to selling in the future, contact us at [email].

— The Marketplate team
```

---

## Metrics

| Metric | Definition | Target |
|--------|------------|--------|
| Suspension with documented rationale | % with rationale ≥ 20 chars | 100% |
| Active order handling SLA | Time to customer notification post-suspension | ≤ 4 hours |
| Appeal response time | Appeal submit → decision | ≤ 10 business days |
| Reinstatement rate | Reinstated / appealed | Track — quality over volume |
| Repeat enforcement (90d post-reinstate) | Same creator re-suspended | ↓ |
| Voluntary offboarding completion time | Request → final payout | ≤ 14 days |
| Customer refund completion (involuntary) | Refunds issued / required | 100% |

→ [Trust Metrics](../../product/success-metrics-overview.md#trust-metrics)

---

## Post-Incident / Retro

**Required retro when:**

- Suspension overturned on appeal with customer harm
- Creator with significant following — public dispute
- Wrong creator suspended (identity mix-up)
- Payout hold exceeded policy without resolution
- System failed to propagate `creator.suspended`

**Outputs:** Process fix, Trust Service monitoring alert, template update, training for operators.

---

## Related Documents

### Mechanics & flows
- [Marketplace Mechanics — Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder)
- [Trust Verification Flow — Reject reason codes](../../pages/flows/trust-verification-flow.md#reject)
- [Order Fulfillment Flow](../../pages/flows/order-fulfillment-flow.md)
- [Creator Onboarding Flow — Suspended state](../../pages/flows/creator-onboarding-flow.md#onboarding-states-summary)

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
- [Food Safety Incident](food-safety-incident.md)
- [Fraud Response](fraud-response.md)
- [Launching a Creator](launching-a-creator.md)

### Future SOPs
- [`operations/trust-and-safety/enforcement/`](../../operations/) *(Phase 4)*
