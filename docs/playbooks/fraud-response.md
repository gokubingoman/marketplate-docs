# Fraud Response

> End-to-end operational playbook for fraud investigation, containment, recovery, and platform hardening.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Trust & Safety  
**Playbook type:** Cross-functional orchestration — **P0 when active fraud confirmed**

---

## Purpose

This playbook orchestrates Marketplate's response to **fraud** — fraudulent identity, stolen payment methods, document manipulation, multi-account abuse, review fraud, payout fraud, and coordinated bad-actor networks. Fraud directly violates the trust thesis and may intersect with [Food Safety Incident](food-safety-incident.md) and [Creator Suspension](creator-suspension-offboarding.md) playbooks.

**Governing principles:** [Human approval on high stakes](../../product/marketplace-mechanics.md#marketplace-model-overview) · [Verification Assist fraud flags](../../ai/verification-assist.md) · Permanent removal for confirmed fraudulent identity per [Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder).

AI detects and flags; humans investigate and enforce — [Humans Decide; AI Assists](../company/values.md#7-humans-decide-ai-assists).

---

## Trigger

| Trigger | Source | Priority |
|---------|--------|----------|
| **Verification Assist fraud flag** | Tampered document, duplicate doc across accounts, font inconsistency | High — 4h SLA |
| **Payment fraud alert** | Chargebacks, stolen card patterns, Payment Service risk score | High |
| **Customer report** | Suspected fake creator, scam listing | Medium |
| **Review fraud cluster** | Moderation Assist duplicate/spam cluster ID | Medium |
| **Operator suspicion** | Manual review during verification | High |
| **Law enforcement inquiry** | Subpoena, fraud referral | P0 |
| **Internal audit** | QA sampling false approve with fraud characteristics | High |
| **Creator report** | Account takeover, impersonation | High |

---

## Stakeholders

| Role | Team | Responsibility |
|------|------|----------------|
| **Fraud Investigation Lead** | Trust & Safety | Case ownership, containment decisions |
| **Trust & Safety Supervisor** | Trust & Safety | Suspension, permanent removal approval |
| **Trust Lead** | Trust & Safety | Network-level decisions, policy exceptions |
| **Legal Counsel** | Legal | Law enforcement response, preservation notices |
| **Engineering On-Call** | Engineering | Account locks, payment blocks, data export |
| **Finance** | Finance | Chargeback handling, payout clawback |
| **AI Platform** | Engineering | Model review if fraud evaded detection |
| **Customer Support** | Support | Customer communication for payment fraud |
| **Security** | Security | Account takeover remediation, credential reset |

**War room:** `#incident-fraud` for P0/active network fraud.

---

## Prerequisites

| Prerequisite | Verification |
|--------------|--------------|
| Fraud reason codes configured in Trust Service | `fraud_suspected` on reject/suspend |
| Verification Assist fraud flag pipeline operational | [Verification Assist — fraud flags](../../ai/verification-assist.md) |
| Payment risk rules active | Payment Service monitoring |
| Document hash cross-account duplicate detection | Trust Service |
| Law enforcement contact protocol documented | Legal ops |
| Audit log export capability | Admin Console |
| Junior operators cannot approve fraud-flagged cases | RBAC enforced |

**Future SOPs:** Identity fraud investigation, payout fraud → [`operations/trust-and-safety/fraud/`](../../operations/) *(Phase 4)*

---

## Phase-by-Phase Execution

### Phase 1 — Detection & Triage (0–4 hours)

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 1.1 | System or Operator | Fraud signal enters queue or alert fires | Verification Queue priority `Fraud suspect` · Payment alert |
| 1.2 | Trust Operator | Claim case; do not approve pending fraud review | Optimistic lock on case |
| 1.3 | Trust Operator | Gather: all accounts linked by document hash, IP, device fingerprint, payment method | Creator Admin Detail · internal tools |
| 1.4 | Fraud Investigation Lead | Classify: **Active** · **Suspected** · **Historical review** | Case tracker |
| 1.5 | Lead (Active) | Open `#incident-fraud`; notify Legal if LE contact or > $5k exposure | War room |

**Active fraud indicators:**

- Fraudulent verification approved and accepting orders
- Stolen payment method checkout in progress
- Payout directed to suspected mule account
- Coordinated review manipulation affecting discovery ranking

---

### Phase 2 — Containment (Active fraud: immediate)

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 2.1 | Trust Supervisor | **Suspend all linked accounts** | `creator.suspended` / account lock |
| 2.2 | Engineering | Block payment capture on pending orders | Payment Service |
| 2.3 | Finance | **Hold payouts** on linked accounts | Payment Service payout hold |
| 2.4 | Trust Operator | Hide listings; remove from Discovery index | Catalog + Discovery |
| 2.5 | Support | Cancel/refund customer orders from fraudulent creator with full refund | Order + Payment |
| 2.6 | Security | Force password reset if account takeover suspected | Identity Service |
| 2.7 | Trust Operator | Preserve evidence: documents, audit logs, payment records, AI flags | Immutable export — Legal hold if needed |

**Containment checklist:**

- [ ] All linked accounts identified and suspended
- [ ] Payouts held
- [ ] Customer orders refunded or cancelled
- [ ] Evidence preserved with chain of custody note
- [ ] No junior operator unilateral approval occurred

---

### Phase 3 — Investigation (4 hours – 10 business days)

| Step | Actor | Action |
|------|-------|--------|
| 3.1 | Fraud Investigation Lead | Build account graph: creators, customers, payment methods, documents |
| 3.2 | Trust Operator | Document comparison — side-by-side viewer, prior submissions | [Verification Queue](../../pages/admin/verification-queue.md) |
| 3.3 | Trust Operator | Review AI fraud flags — which signals fired, which missed | `ai_flags_json` + model version |
| 3.4 | Finance | Chargeback analysis, payout history, refund patterns |
| 3.5 | Support | Customer impact assessment — affected orders, contact list |
| 3.6 | Legal | LE protocol if subpoena; preservation notice if litigation risk |
| 3.7 | Lead | Investigation summary: confirmed fraud · inconclusive · false positive |

**Investigation evidence standards:**

| Evidence type | Source |
|---------------|--------|
| Document forensics | Verification Assist + manual operator notes |
| Account linkage | Document hash, device ID, payment fingerprint |
| Behavioral signals | Order patterns, messaging, review timing |
| Audit trail | All Trust Service actions with operator IDs |
| AI run metadata | Model version, confidence, flags dismissed (if any) |

---

### Phase 4 — Enforcement & Recovery

| Step | Actor | Action |
|------|-------|--------|
| 4.1 | Trust Supervisor | Final enforcement per finding | See decision matrix below |
| 4.2 | Trust Operator | Apply enforcement with required rationale and reason code | Audit log |
| 4.3 | Finance | Execute payout clawback if funds recoverable |
| 4.4 | Support | Customer remediation: refunds, credits, notification |
| 4.5 | Creator Success | **Do not outreach** to confirmed fraud accounts — Trust-only comms |
| 4.6 | Engineering | Close account registration vectors if systemic (disposable email block, etc.) |
| 4.7 | AI Platform | Update fraud detection benchmarks; reprocess hold queue if model improved |

**Enforcement matrix:**

| Finding | Enforcement |
|---------|-------------|
| Confirmed fraudulent identity | Permanent removal — all linked accounts |
| Document manipulation (single account) | Reject + permanent removal |
| Review fraud ring | Remove fraudulent reviews; suspend creators involved; reset ratings |
| Payment fraud (customer-side) | Account lock; refund legitimate creators |
| Account takeover | Restore legitimate owner; suspend attacker |
| False positive | Reinstate with apology; document for QA |
| Operator false approve | QA review; retraining; case re-opened |

→ [Creator Suspension & Offboarding](creator-suspension-offboarding.md)

---

### Phase 5 — Hardening & Close

| Step | Actor | Action |
|------|-------|--------|
| 5.1 | Fraud Lead | File hardening recommendations: rules, AI thresholds, UX friction |
| 5.2 | Engineering | Implement approved controls (e.g., enhanced liveness, velocity limits) |
| 5.3 | Trust Ops | Update verification checklist if gap identified |
| 5.4 | AI Platform | Eval pipeline run before model threshold changes |
| 5.5 | Fraud Lead | Close case; schedule retro |

---

## Decision Points

| Decision | Owner | Options | Default |
|----------|-------|---------|---------|
| Suspend before investigation complete | Fraud Lead | Immediate suspend · Monitor | Immediate on Active fraud |
| Permanent removal vs. appeal path | Trust Lead | Permanent · Suspension with appeal | Permanent on confirmed identity fraud |
| Customer refund scope | Fraud Lead + Finance | All orders · Post-fraud-only | All orders from fraudulent creator |
| Law enforcement cooperation | Legal | Respond · Challenge · Monitor | Legal decides |
| Reprocess queue with new model | AI Platform + Trust Lead | Reprocess · Forward only | Reprocess if false approve pattern |
| Public disclosure | Legal + Comms | Required · Not required | Legal decides |

---

## Communication Templates

### Template: Customer — Fraudulent Creator Refund

**Owner:** Support  
**Channel:** Email

```
Subject: Important update on your order — full refund issued

Hi [Customer first name],

We've identified activity on [Creator name]'s account that violates our trust policies. Out of caution, we've refunded your order #[ORDER_ID] in full.

Refund amount: [AMOUNT]
Expected timeline: 5–10 business days

You do not need to take action. If you have concerns about your experience, reply with reference [CASE_ID].

We're sorry for the disruption.

— Marketplate Trust & Safety
```

### Template: Creator — Fraud Rejection (pre-approval)

**Owner:** Trust & Safety  
**Channel:** Email + in-app

```
Subject: Your verification could not be approved

Hi [Name],

We were unable to approve your verification submission.

Case ID: [CASE_ID]

If you believe this is an error, you may contact Help with your case ID. Please note that fraudulent submissions may result in permanent account removal.

— Marketplate Trust & Safety
```

*(Intentionally vague on fraud specifics to avoid educating bad actors — detailed rationale in internal audit only.)*

### Template: Internal — Active Fraud Containment

**Channel:** Slack `#incident-fraud`

```
🚨 ACTIVE FRAUD — Lead: @[name]

Case: [CASE_ID]
Type: [Identity / Payment / Review ring]
Exposure: [N accounts] · [N orders] · $[amount]
Actions:
• [x] Accounts suspended: [ids]
• [x] Payouts held
• [ ] Customer refunds in progress
• [x] Evidence preserved

Next update: [time]
Legal notified: [Y/N]
```

---

## Metrics

| Metric | Target direction |
|--------|------------------|
| Fraud flag review SLA (4h) | ≥ 95% compliance |
| Time to containment (active fraud) | ≤ 1 hour |
| False approve rate (fraud cases in QA sample) | ↓ 0 |
| Fraud loss ($) per month | ↓ |
| Chargeback rate | ↓ vs. industry baseline |
| Duplicate document detection rate | ↑ |
| Linked account identification completeness | 100% at close |
| Customer refund completion time | ≤ 72 hours |

→ [Trust Metrics](../../product/success-metrics-overview.md#trust-metrics)

---

## Post-Incident / Retro

**Required for:** All P0 fraud incidents; any false approve that reached live orders; any fraud network > 5 accounts.

**Retro agenda:**

1. Detection timeline — when could we have caught this earlier?
2. Containment effectiveness — customer/creator impact minimized?
3. AI assist performance — flags fired/missed; dismissed inappropriately?
4. Operator process — checklist gap, senior review bypass?
5. Hardening actions — rules, UX, staffing

**Outputs:** Updates to [Verification Assist](../../ai/verification-assist.md), Platform Settings thresholds, verification SOPs, this playbook.

---

## Related Documents

### AI & engineering
- [Verification Assist — Fraud flags](../../ai/verification-assist.md)
- [Moderation Assist — Spam clusters](../../ai/moderation-assist.md)
- [Trust Service](../../engineering/services/trust-service.md)
- [Trust Verification Flow — Fraud flag SLA](../../pages/flows/trust-verification-flow.md#sla--escalation)

### Flows & pages
- [Trust Verification Flow](../../pages/flows/trust-verification-flow.md)
- [Creator Admin Detail](../../pages/admin/creator-admin-detail.md)
- [Verification Queue](../../pages/admin/verification-queue.md)
- [Moderation Queue](../../pages/admin/moderation-queue.md)

### Policy
- [Marketplace Mechanics — Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder)
- [Company Values](../../company/values.md)

### Related playbooks
- [Creator Suspension & Offboarding](creator-suspension-offboarding.md)
- [Trust & Safety Escalation](trust-safety-escalation.md)
- [Food Safety Incident](food-safety-incident.md)
- [Launching a Creator](launching-a-creator.md)
