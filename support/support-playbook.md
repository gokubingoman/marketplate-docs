# Support Playbook

> End-to-end customer support operations — channels, triage, SLAs, tools, handoffs, and shift procedures.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Customer Support  
**Reports to:** Support Lead → Operations

---

## Purpose

This playbook defines how Marketplate Support reduces uncertainty for **customers (buyers)** and **creators (sellers)** when self-service and creator messaging are not enough. Support triages, informs, mediates, and escalates — but does not approve verification, moderate content, suspend accounts, or issue refunds without following established workflows.

**Governing principles:** [Operations Philosophy](../company/constitution.md#operations-philosophy) · [Voice and Tone — Customer Support](../brand/voice-and-tone.md#customer-support) · [Humans Decide; AI Assists](../company/values.md#7-humans-decide-ai-assists)

**v1 rule:** [Support Assist](../ai/support-assist.md) recommends categories, priorities, macros, and related articles. **Humans send every customer-facing reply.** No autonomous outbound email or chat.

---

## Scope

| In scope | Out of scope (escalate) |
|----------|-------------------------|
| Order status, pickup/delivery timing, quality disputes | Verification approval or rejection |
| Refund mediation within policy | Creator suspension or reinstatement |
| Account access, notification, preference help | Content moderation actions |
| Creator verification status communication (read-only) | Payout adjustments without supervisor approval |
| Policy explanation and Help article guidance | Legal/regulatory responses |
| Trust report intake and routing | Food safety investigation (T&S owns) |

→ Boundaries: [Support Onboarding — Decision Framework](../docs/training/support-onboarding.md#decision-framework)

---

## Support Channels

| Channel | v1 status | Audience | Notes |
|---------|-----------|----------|-------|
| **Help form** | Primary | Customer + creator | [`/help#contact`](../pages/customer/help.md#contact-support) · [Contact Support article](../docs/help-center/contact-support.md) |
| **Email (ticket thread)** | Primary | All | Reply in-thread; preserve case context |
| **Order-scoped help** | Primary | Customer | [Order Detail](../pages/customer/order-detail.md) → `?order=[id]` pre-fills context |
| **In-app messaging** | Creator ↔ customer | Not Support | Direct customers to message creator first for order issues |
| **Phone** | Market-dependent | — | If listed on Help page; otherwise email/form only |
| **Live chat** | Future | — | See [Help future improvements](../pages/customer/help.md#future-improvements) |

### Channel routing rules

1. **Self-service first** — Cite Help articles before opening investigations.
2. **Creator first for order issues** — Late pickup, wrong item, timing: customer messages creator via [Messaging](../docs/help-center/messaging.md). Support enters when creator is unresponsive 24+ hours or parties disagree on resolution.
3. **Support form for platform actions** — Refunds requiring mediation, payment errors, account security, verification status, trust reports.
4. **Never ask for** full card numbers, government ID, or passwords in email.

---

## Ticket Intake & Classification

### Customer-submitted categories

Maps to Help form and [Support Assist](../ai/support-assist.md) routing queues:

| Category | Routing queue | Default priority | First response SLA |
|----------|---------------|------------------|-------------------|
| General inquiry | `general` | Standard | 24 hours |
| Order issue | `orders` | Standard | 24 hours |
| Payment & refund | `payments` | Standard → Elevated if 5+ days unresolved | 24–48 hours |
| Food safety | `trust` | **Urgent** | 4 hours |
| Allergic reaction | `trust` | **Critical** | 1 hour |
| Account security | `trust` | **Priority** | 4 hours |
| Creator verification | `verification` | Standard | 2 business days |
| Trust & safety report | `trust` | Elevated | 24 hours |

→ Public SLAs: [Help Center README — Escalation Paths](../docs/help-center/README.md#escalation-paths) · [Contact Support](../docs/help-center/contact-support.md#response-timelines)

### AI-assisted triage (Support Assist)

On ticket creation, Support Assist may suggest:

- Category and routing queue
- Priority (`standard` · `elevated` · `urgent`)
- Top 3 macros from [Macro Library](macro-library.md)
- Related Help articles

**Operator actions:**

1. Confirm or override AI suggestions — never auto-send.
2. Validate `urgent`/`critical` items at shift start (food safety keyword rules may over-trigger).
3. Attach order context from admin lookup when customer omitted order ID.

→ Full spec: [Support Assist](../ai/support-assist.md)

---

## Triage Workflow

### Standard triage (every ticket)

```
1. Read ticket + AI assist panel
2. Pull order/creator/account context (admin read-only)
3. Classify: customer issue | creator issue | platform issue | trust issue
4. Check Help center for applicable article
5. Respond (macro + personalization) OR escalate
6. Tag resolution category; log actions in ticket
7. Close when resolved + 48h no reply, or hand off with owner
```

### Priority queue handling

| Priority | Acknowledge within | Investigation start | Escalate if unresolved |
|----------|-------------------|---------------------|------------------------|
| **Critical** (allergic reaction) | 15 minutes | Immediate | T&S on-call immediately — [Escalation Guide](escalation-guide.md) |
| **Urgent** (food safety, account security) | 30 minutes | 1 hour | T&S if safety confirmed or account compromised |
| **Elevated** (payment dispute aging, trust report) | 4 hours | Same business day | Ops or T&S per matrix |
| **Standard** | Per SLA above | Next available agent | Support Lead at SLA breach |

**Critical path — allergic reaction:**

1. Do **not** use a macro as the full response.
2. Acknowledge receipt; confirm medical care if not already stated.
3. Page T&S on-call immediately — tag `food-safety` + `P0-candidate`.
4. Pull order snapshot; preserve evidence per [Food Safety Incident](../docs/playbooks/food-safety-incident.md).
5. Follow [Escalation Guide — Food Safety](escalation-guide.md#food-safety-and-allergen-incidents).

---

## Customer vs. Creator Issues

Marketplate serves two sides of the marketplace. Route and frame responses accordingly.

### Customer (buyer) issues

| Issue type | First action | Support role |
|------------|--------------|--------------|
| Order status / not ready | Confirm creator contacted; check order state in admin | Explain status; mediate if creator unresponsive 24h+ |
| Wrong / missing items | Verify messaging thread | Mediate refund/replacement per [Refunds](../docs/help-center/refunds.md) |
| Pickup / delivery problem | Check fulfillment type and window | Cite [Pickup](../docs/help-center/pickup.md) or [Delivery](../docs/help-center/delivery.md) |
| Refund disagreement | Review checkout policy acknowledgment | Mediate; escalate to [Dispute Resolution](../operations/README.md) SOP if deadlocked |
| Allergen / illness | **Stop macro workflow** | Escalate T&S — [Food Safety](../docs/help-center/food-safety.md) |
| Account / login | Troubleshoot per [Account](../docs/help-center/account.md) | Security escalation if compromise suspected |
| Verification education | Link [Trust](../docs/help-center/trust.md) | Explain badges; do not promise verification outcomes |

**Tone:** Empathetic, accountable, resolution-focused. Lead with creator name when discussing orders.

### Creator (seller) issues

| Issue type | First action | Support role |
|------------|--------------|--------------|
| Verification status / delay | Read verification state in [Creator Admin Detail](../pages/admin/creator-admin-detail.md) | Communicate status only — no approval promises |
| Verification resubmission help | Link [Verification](../docs/help-center/verification.md) | Explain "Needs action" items; escalate doc questions to T&S queue |
| Payout timing | Check payment state | Explain timeline; escalate missing payout > SLA to Ops |
| Order / customer dispute | Review order + messages | Coach on policy; mediate when customer escalates |
| Catalog / listing help | Link [Menus](../docs/help-center/menus.md), [Storefronts](../docs/help-center/storefronts.md) | Product guidance; compliance questions → T&S |
| Account / dashboard access | Troubleshoot | Escalate security issues |

**Tone:** Respectful of livelihood; precise on timelines. Creators are partners, not ticket numbers.

**Handoff to Creator Success:** Repeat buyer disputes, high-GMV creator at-risk signals, or churn-risk patterns → tag `cs-handoff` per [Customer Lifecycle — Internal Handoffs](../docs/customer-success/customer-lifecycle.md#internal-handoffs). CS responds within 24 hours on eligible tickets.

---

## Food Safety Escalation

Food safety incidents override normal support workflows. **When in doubt, escalate up.**

### Mandatory immediate escalation (no macro-only reply)

| Trigger | Action |
|---------|--------|
| Allergic reaction reported | T&S on-call + [Food Safety Incident](../docs/playbooks/food-safety-incident.md) |
| Illness after consumption | T&S — severity P0/P1 per symptoms |
| Suspected allergen mislabeling | T&S — creator may be suspended pending review |
| Multiple reports same creator/item (72h) | T&S — pattern escalation |
| Customer mentions hospital / emergency room | P0 — [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md) |

### Support role during food safety incidents

1. **Triage** — Log order ID, creator ID, items, timeline, symptoms.
2. **Acknowledge** — Human-written empathy + next steps; never blame customer or creator in initial reply.
3. **Hand off** — Assign T&S owner; Support Lead notified for P0/P1.
4. **Customer comms** — Use T&S-approved templates only after IC review.
5. **Do not** — Promise investigation outcomes, assign fault, or discuss creator enforcement with customer before T&S guidance.

→ Matrix: [Escalation Guide](escalation-guide.md) · SOP: [Food Safety Incident](../operations/README.md) *(Phase 4)*

---

## Service Level Agreements (SLAs)

### Response SLAs (first human reply)

| Tier | Target | Business hours |
|------|--------|----------------|
| Critical | 1 hour | 24/7 on-call rotation for food safety |
| Urgent | 4 hours | 24/7 for safety/security; else next business day start |
| Elevated | 24 hours | Business days |
| Standard | 24 hours | Business days |
| Creator verification status | 2 business days | Business days |

**Resolution SLAs** vary by issue — set explicit next-update time in every reply.

### SLA breach procedure

1. Reply to customer with status and revised timeline.
2. Notify Support Lead in `#support`.
3. If trust-impacting or > 2× SLA, open escalation per [Escalation Guide](escalation-guide.md).
4. Log breach reason: volume, complexity, handoff delay, system outage.

### Business hours

TODO(decision): Official support hours by market and holiday coverage. Until defined, SLAs apply to **next business day** for standard tickets submitted outside Mon–Fri 9 AM–6 PM local primary market time.

---

## Tools & Systems

| System | Access | Use |
|--------|--------|-----|
| **Support ticket platform** | Agent | Primary workspace — respond, tag, escalate |
| **Support Assist panel** | View | AI classification, macro suggestions, related articles |
| **Admin — Order lookup** | Read-only | [Order states](../engineering/services/order-service.md) |
| **Admin — Creator profile** | Read-only | [Creator Admin Detail](../pages/admin/creator-admin-detail.md) |
| **Admin — Disputes** | Read-only → write via SOP | [Dispute Detail](../pages/admin/dispute-detail.md) |
| **Help center CMS** | Read | Verify FAQ accuracy before citing |
| **Macro library** | Read | [Macro Library](macro-library.md) — in ticket tool when integrated |
| **Slack** `#support` · `#trust-safety` · `#incidents` | Member | Coordination and escalation |

**Not granted to Tier 1:** Verification queue write, moderation actions, platform settings, payout adjustments without approval.

→ Access request: [Support Onboarding — Systems](../docs/training/support-onboarding.md#systems-access)

---

## Handoffs

### To Trust & Safety

| Trigger | Required context | Playbook |
|---------|------------------|----------|
| Food safety / allergen / illness | Order, creator, items, symptoms, photos | [Food Safety Incident](../docs/playbooks/food-safety-incident.md) |
| Fraud suspicion | Timeline, evidence, user IDs | [Fraud Response](../docs/playbooks/fraud-response.md) |
| Harassment, threats, illegal content | Screenshots, message IDs | [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md) |
| Verification dispute / appeal | Case ID, rejection reason | [Trust Verification Flow](../pages/flows/trust-verification-flow.md) |

**Escalation quality bar:** Ticket ID, user IDs, order IDs, timeline, what you told the customer, recommended next action.

### To Operations / Payments

| Trigger | Destination |
|---------|-------------|
| Refund over policy threshold | [Refund Processing](../operations/README.md) SOP |
| Payout missing > SLA | Ops lead + dispute tools |
| Platform outage affecting orders | `#incidents` + Engineering on-call |

### To Customer Success

| Trigger | Context |
|---------|---------|
| Repeat buyer dispute | [Customer Lifecycle handoffs](../docs/customer-success/customer-lifecycle.md#internal-handoffs) |
| High-GMV creator support pattern | Creator health signal |
| Trust incident affecting creator base | Incident severity summary |

### From T&S back to Support

After containment, T&S may request Support to:

- Send surge customer communications (IC-approved copy)
- Update Help articles for incident-related FAQs
- Handle refund status inquiries on force-cancelled orders

---

## Dispute & Refund Mediation

Support mediates; Ops executes refunds per SOP.

### Workflow

1. Confirm customer contacted creator and waited reasonable window (48h post-fulfillment for quality issues).
2. Review order policy acknowledgment and message thread.
3. Apply [Refunds & Cancellations](../docs/help-center/refunds.md) — creator-initiated cancel = full refund automatic.
4. If deadlocked, open dispute in [Dispute Detail](../pages/admin/dispute-detail.md) or escalate to Ops.
5. Communicate outcome with specific amounts and 5–10 business day refund timing.

**Do not** override checkout-acknowledged policies without investigation findings.

→ Mechanics: [Marketplace Mechanics — Cancellations and refunds](../product/marketplace-mechanics.md)

---

## Shift Procedures

### Shift start (all agents)

| Step | Action |
|------|--------|
| 1 | Check `#support` and `#incidents` for active incidents |
| 2 | Review **priority queue** — validate AI-flagged urgent/critical tickets |
| 3 | Acknowledge any ticket approaching SLA breach |
| 4 | Confirm Support Assist / ticket platform operational — note fallback mode if degraded |
| 5 | Read handoff notes from prior shift (pinned thread or ticket tag `shift-handoff`) |

### During shift

- Work priority queue before standard queue unless SLA breach imminent on standard ticket.
- Personalize every macro — see [Macro Library — Usage rules](macro-library.md#usage-rules).
- Tag `escalated` + owner when handing off; do not close until owner accepts.
- Flag Help gaps: `#support-content` or doc PR for recurring unanswered questions.

### Shift end

| Step | Action |
|------|--------|
| 1 | Post handoff note: open escalations, SLA-at-risk tickets, incident status |
| 2 | Reassign unowned urgent tickets if going off-shift |
| 3 | Log volume summary if Support Lead requested |

### On-call (food safety / P0)

- PagerDuty rotation — Support Lead or designated senior agent.
- 15-minute ack for P0 triggers from Support Assist keyword rules or manual report.
- Immediately invoke [Escalation Guide](escalation-guide.md) and notify T&S.

---

## Metrics & Reporting

### Support-owned KPIs

| Metric | Definition | Target direction | Cadence |
|--------|------------|-------------------|---------|
| **First response time** | Ticket created → first human reply | Within SLA tier | Daily |
| **First contact resolution (FCR)** | Resolved without escalation or reopen | ↑ | Weekly |
| **CSAT** | Post-resolution survey (1–5) | ≥ 4.2 avg | Weekly |
| **SLA adherence** | % tickets first response within SLA | ≥ 95% | Weekly |
| **Escalation rate** | Escalated / total tickets | Monitor by category | Weekly |
| **Reopen rate** | Reopened within 14 days / closed | ↓ | Weekly |
| **Macro edit distance** | Sent vs. suggested macro diff | ↓ over time = better templates | Monthly |
| **Help deflection** (product) | FAQ expand without ticket | ↑ | Weekly |

→ CS context: [Success Metrics — Buyer satisfaction](../docs/customer-success/success-metrics.md#buyer-satisfaction-cs-primary-ownership) · [Support contact rate](../product/success-metrics-overview.md)

### AI assist quality

| Metric | Source |
|--------|--------|
| Ticket category accuracy | Support Assist dashboard |
| Urgent priority recall | Weekly audit sample |
| Macro acceptance rate | Sent without major edit |
| Zero-result Help searches | Content ops backlog |

→ Targets: [Support Assist — Evaluation](../ai/support-assist.md#evaluation)

### Weekly Support review (Support Lead)

| Section | Review |
|---------|--------|
| Volume | By category, queue, creator vs customer |
| SLA | Breaches, root causes |
| Escalations | T&S, Ops, CS handoffs |
| Quality | CSAT, reopen rate, spot-check replies |
| Content | Top ticket themes → Help FAQ candidates |
| Incidents | Any P0/P1 involvement |

---

## Quality Standards

Every customer-facing reply must pass the [Voice Checklist](../brand/voice-and-tone.md#voice-checklist):

- Most important information first
- Verifiable statements only
- Specific timing, money, or safety information
- One clear next action
- Human tone — not robotic or overly casual

**Avoid:** "We apologize for any inconvenience" without action; blame shifting; verification promises; internal jargon (Tier 1, queue names in customer copy).

### Spot-check cadence

- New hires: 100% reviewed first 2 weeks
- All agents: 5% random weekly + 100% of escalated trust tickets

---

## Incident & Surge Mode

When `#incidents` declares active incident (outage, food safety P0, fraud at scale):

1. Support Lead activates surge roster or pauses non-urgent queue.
2. Use IC-approved macros only — no improvisation on legal/safety copy.
3. Pause SLA clock for affected category if Engineering confirms platform issue.
4. Post-incident: contribute to retro; update Help articles and macros as needed.

→ [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md)

---

## Related Documents

### Support team
- [Escalation Guide](escalation-guide.md)
- [Macro Library](macro-library.md)
- [Support Onboarding](../docs/training/support-onboarding.md)

### Customer-facing
- [Help Page Spec](../pages/customer/help.md)
- [Help Center](../docs/help-center/README.md)
- [Contact Support](../docs/help-center/contact-support.md)

### AI & engineering
- [Support Assist](../ai/support-assist.md)
- [Order Service](../engineering/services/order-service.md)
- [Payment Service](../engineering/services/payment-service.md)
- [Notification Service](../engineering/services/notification-service.md)

### Operations & trust
- [Operations SOPs](../operations/README.md)
- [Trust & Safety Escalation](../docs/playbooks/trust-safety-escalation.md)
- [Food Safety Incident](../docs/playbooks/food-safety-incident.md)
- [Fraud Response](../docs/playbooks/fraud-response.md)
- [Dispute Resolution](../operations/README.md) *(Phase 4 SOP)*

### Admin surfaces
- [Admin Dashboard](../pages/admin/admin-dashboard.md)
- [Dispute Detail](../pages/admin/dispute-detail.md)
- [Moderation Queue](../pages/admin/moderation-queue.md)
- [Verification Queue](../pages/admin/verification-queue.md)

### Customer Success
- [Customer Success README](../docs/customer-success/README.md)
- [Customer Lifecycle](../docs/customer-success/customer-lifecycle.md)
- [Success Metrics](../docs/customer-success/success-metrics.md)

### Brand & governance
- [Voice and Tone](../brand/voice-and-tone.md)
- [Founding Constitution](../company/constitution.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
