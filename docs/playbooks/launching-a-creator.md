# Launching a Creator

> End-to-end operational playbook from creator signup through verified status, first listing, and first fulfilled order.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Creator Operations  
**Playbook type:** Cross-functional orchestration

---

## Purpose

This playbook orchestrates the **supply-side activation funnel** — the journey from a creator expressing interest to a verified operator receiving and fulfilling their first order. It is not a single verification SOP; it coordinates Product, Trust & Safety, Creator Success, Engineering, and Marketing across product surfaces, backend services, and operational workflows.

**Governing thesis:** [Trust is our product](../company/values.md#1-trust-is-the-product). Unverified creators cannot accept paid orders — [Marketplace Mechanics — Verified to sell](../product/marketplace-mechanics.md#marketplace-model-overview).

**Primary flow reference:** [Creator Onboarding Flow](../../pages/flows/creator-onboarding-flow.md)

---

## Trigger

| Trigger type | Example |
|--------------|---------|
| **Inbound application** | Creator completes signup at `/creator/signup` |
| **Referral / partner** | Commercial kitchen partner sends tenant with pre-linked facility ID |
| **Outbound recruitment** | Creator Success identifies target creator and sends invite link |
| **Customer conversion** | Existing customer selects "Become a creator" in account menu |

**Entry criteria:** Valid email, jurisdiction selection, and business type declared. No pre-approval required to begin signup.

---

## Stakeholders

| Role | Team | Responsibility in this playbook |
|------|------|--------------------------------|
| **Creator Success Lead** | Creator Ops | Activation monitoring, outreach on stalled onboarding |
| **Trust & Safety Operator** | Trust & Safety | Identity, kitchen, compliance review |
| **Trust & Safety Supervisor** | Trust & Safety | SLA breach escalation, fraud-flag cases |
| **Engineering On-Call** | Engineering | Trust Service, Catalog, Notification incidents |
| **AI Platform** | Engineering | Verification Assist pipeline health |
| **Marketing** | Growth | Acquisition campaigns, welcome email sequences |
| **Legal / Compliance** | Legal | Jurisdiction template validation (new markets) |
| **Support** | Customer Support | Creator help tickets during onboarding |

**RACI summary:** Creator Success is **Accountable** for time-to-first-order; Trust & Safety is **Accountable** for verification decisions; Engineering is **Responsible** for system availability.

---

## Prerequisites

Before a creator can go live, the following must be in place:

| Prerequisite | Owner | Verification |
|--------------|-------|--------------|
| Jurisdiction compliance template loaded | Legal + Trust Ops | [Platform Settings](../../pages/admin/platform-settings.md) → jurisdiction library |
| Trust Service operational | Engineering | Verification queue accepting submissions |
| Verification Assist pipeline healthy | AI Platform | Fallback rate within SLO; no P1 alerts |
| Operator staffing for queue SLAs | Trust & Safety | Coverage for identity (2 BD), kitchen (3 BD), compliance (2 BD) |
| Creator-facing docs published | Creator Ops | [Chef Welcome Package](../onboarding/chef-welcome-package.md) live |
| Notification templates configured | Product + Ops | Approve/reject/request-info emails in Notification Service |

**Future SOPs:** Detailed verification checklists → [`operations/trust-and-safety/verification/`](../../operations/) *(Phase 4)*

---

## Phase-by-Phase Execution

### Phase 0 — Acquisition & Signup

**Duration target:** Same session  
**Pages:** `/creator/signup` → [Creator Signup](../../pages/auth/creator-signup.md)

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 0.1 | Marketing | Creator lands via campaign, referral, or organic | Analytics: `creator_signup_start` |
| 0.2 | Creator | Completes signup: email, legal name, business type, slug, jurisdiction, category | Identity Service creates account; Trust Service initializes compliance checklist |
| 0.3 | System | Sets `verification_status: identity_not_started` | Redirect → `/creator/verify/identity` |
| 0.4 | Creator Success | Monitor signup → identity submit conversion daily | Dashboard: creator funnel metrics |

**Exit criteria:** Creator account created with jurisdiction and category captured.

---

### Phase 1 — Identity Verification

**Duration target:** ≤ 2 business days (review SLA)  
**Pages:** `/creator/verify/identity` · Admin: [Verification Queue](../../pages/admin/verification-queue.md)

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 1.1 | Creator | Uploads government ID, selfie/liveness, business registration (if applicable), tax identity | Trust Service: `VerificationRecord` created, status `in_review` |
| 1.2 | System | Verification Assist extracts fields, flags mismatches | `ai_flags_json` attached; case enters queue |
| 1.3 | Trust Operator | Claims case, completes identity checklist, decides approve/reject/request info | [Trust Verification Flow — Phase 4–5](../../pages/flows/trust-verification-flow.md#phase-4--case-review) |
| 1.4 | System | On approve: unlock kitchen submission; emit `verification.approved` | Notification Service emails creator |
| 1.5 | Creator Success | If no identity submit within 48h of signup, send nudge email | CRM / lifecycle email |

**Exit criteria:** Identity status `approved`.

**Blocked path:** Reject or request info → creator revises → resubmission with priority bump (see [Trust Verification Flow — Resubmission](../../pages/flows/trust-verification-flow.md#resubmission-flow)).

---

### Phase 2 — Kitchen Verification

**Duration target:** ≤ 3 business days (review SLA)  
**Pages:** `/creator/verify/kitchen` · Admin: Verification Queue

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 2.1 | Creator | Selects kitchen type; uploads address, photos, inspection/registration docs | Trust Service: kitchen `VerificationRecord` |
| 2.2 | Trust Operator | Validates facility type, photos, multi-tenant linkage (if applicable) | Checklist per [Trust Verification Flow](../../pages/flows/trust-verification-flow.md#operator-checklist--kitchen) |
| 2.3 | System | On approve: unlock compliance + paid listing eligibility | Catalog Service notified via creator cache update |

**Persona variations:**

| Persona | Difference |
|---------|------------|
| Cottage Food Operator | Home kitchen path; cottage registration required in Phase 3 |
| Commercial Kitchen tenant | Facility link — skip redundant facility upload |
| Food Truck Operator | Commissary linkage + unit ID required |

**Exit criteria:** Kitchen status `approved`.

---

### Phase 3 — Compliance Verification

**Duration target:** ≤ 2 business days per document batch  
**Pages:** `/creator/compliance` · `/dashboard/compliance` · Admin: Verification Queue

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 3.1 | Creator | Uploads jurisdiction-required docs: food handler cert, business license, cottage food reg, insurance | Compliance Engine validates against jurisdiction template |
| 3.2 | Trust Operator | Reviews each document; captures expiration dates | Expiration tracking scheduled |
| 3.3 | System | All required docs approved → **Verified Creator** status granted | `verification.approved` (compliance); Notification: "You are verified" |
| 3.4 | Creator Success | Trigger welcome-to-verified email with first-listing guide | Link to [Chef Onboarding Checklist](../onboarding/chef-onboarding-checklist.md) |

**Exit criteria:** Verified Creator status; all three trust layers approved.

---

### Phase 4 — Activation (First Listing & Availability)

**Duration target:** ≤ 7 days post-verification  
**Pages:** `/dashboard` · `/dashboard/catalog` · `/dashboard/availability` · `/dashboard/storefront`

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 4.1 | Creator | Completes activation checklist: profile photo, story, first listing, availability | Dashboard tracks checklist completion |
| 4.2 | Creator | Publishes first menu item with allergens, ingredients, production location, fulfillment method | Catalog Service: listing live; Discovery index updated |
| 4.3 | Creator | Configures pickup windows / delivery zones / capacity limits | Order Service enforces capacity at checkout |
| 4.4 | Creator Success | If no listing within 5 days of verification, personal outreach | Phone or email with setup assistance offer |
| 4.5 | Marketing | Creator shares storefront link (`marketplate.com/creators/:slug`) | Analytics: `storefront_share` |

**Exit criteria:** At least one published listing with valid fulfillment configuration.

---

### Phase 5 — First Order & Fulfillment

**Duration target:** Creator-dependent (goal: within 14 days of first listing)  
**Pages:** Customer: [Checkout](../../pages/customer/checkout.md) · Creator: [Orders](../../pages/creator/orders.md)  
**Flow reference:** [Order Fulfillment Flow](../../pages/flows/order-fulfillment-flow.md)

| Step | Actor | Action | System |
|------|-------|--------|--------|
| 5.1 | Customer | Discovers creator, purchases via [Customer Purchase Flow](../../pages/flows/customer-purchase-flow.md) | Order Service: payment authorized, status `New` |
| 5.2 | Creator | Receives push + email; confirms order within SLA (default 2h) | Status → `Confirmed` |
| 5.3 | Creator | Produces → marks Ready → completes handoff | Status → `Completed`; review window opens |
| 5.4 | Creator Success | First-order congratulations + [Chef Success Guide](../onboarding/chef-success-guide.md) | Lifecycle email at completion |
| 5.5 | Trust & Safety | Monitor first-order disputes or safety flags | No action unless triggered |

**Exit criteria:** First order completed; activation checklist fully done.

---

## Decision Points

| Decision | Owner | Options | Default |
|----------|-------|---------|---------|
| Approve vs. reject identity | Trust Operator | Approve · Reject · Request info | Request info when ambiguous — never rubber-stamp |
| Fraud flag on submission | Trust Supervisor | Escalated review · Account hold · Reject with fraud code | Immediate supervisor claim; no junior approval |
| Creator stalled > 7 days at any verification step | Creator Success | Automated nudge · Personal outreach · Archive lead | Nudge at 3d, outreach at 7d |
| Verified but no listing > 14 days | Creator Success | Outreach · Pause marketing spend on acquisition in region | Outreach + offer setup call |
| First order dispute or allergen report | Trust & Safety | Mediate · Suspend pending investigation | See [Food Safety Incident](food-safety-incident.md) if safety-related |
| Commercial kitchen tenant linkage dispute | Trust Operator | Verify facility admin approval · Reject linkage | Require facility admin confirmation |

**Escalation path:** Operator → Supervisor (SLA breach) → Trust Lead (fraud/safety) → Founder (`TODO(decision):` for policy exceptions)

---

## Communication Templates

### Template: Identity Approved

**Channel:** Email + in-app  
**Trigger:** Trust Operator approves identity  
**Owner:** System (Notification Service)

```
Subject: Your identity verification is approved

Hi [Creator first name],

Your identity verification is approved. You're one step closer to going live.

Next step: Complete your kitchen verification so customers know where your food is made.

[Continue to kitchen verification →]

Questions? Reply to this email or visit Help — include case ID [CASE_ID] if referencing this review.

— The Marketplate team
```

### Template: Verification Action Required

**Channel:** Email + in-app  
**Trigger:** Request info decision

```
Subject: Action needed on your verification

Hi [Creator first name],

We reviewed your [identity/kitchen/compliance] submission and need a few items before we can approve:

• [Specific item 1]
• [Specific item 2]

Upload the requested items in your verification dashboard. We'll re-review within [1/2] business day(s) of resubmission.

[Update my submission →]

Case ID: [CASE_ID]
```

### Template: Verified — Publish Your First Listing

**Channel:** Email  
**Trigger:** All verification layers approved  
**Owner:** Creator Success (lifecycle)

```
Subject: You're verified — let's publish your first item

Hi [Creator first name],

Congratulations — you're a Verified Creator on Marketplate.

Your storefront: marketplate.com/creators/[slug]

Three steps to your first order:
1. Add your first menu item (include allergens and ingredients)
2. Set your pickup windows or delivery schedule
3. Share your storefront link with customers

[Go to dashboard →]

We're here if you need help getting set up.
```

### Template: First Order Received

**Channel:** Push + email  
**Trigger:** New order placed  
**Owner:** System

```
Subject: New order #[ORDER_ID] — pickup [DAY] [TIME]

You have a new order from [Customer first name].

Items: [Summary]
Pickup: [Window]
Total: [Amount]

[View order →]

Confirm within 2 hours to keep your reliability score strong.
```

---

## Metrics

| Metric | Definition | Target | Owner |
|--------|------------|--------|-------|
| Signup → identity submit | % completing identity upload within 7d | ↑ Baseline TBD | Creator Ops |
| Time to verified | Signup → Verified Creator status | ↓ ≤ 10 business days median | Trust & Safety |
| Verification SLA compliance | % cases decided within SLA | ≥ 95% | Trust & Safety |
| Verified → first listing | Days from verified to publish | ↓ ≤ 5 days median | Creator Ops |
| First listing → first order | Days from publish to first order | ↓ ≤ 14 days median | Creator Ops |
| First order completion rate | First orders completed / placed | ≥ 95% | Creator Ops |
| Verification abandonment | Drop-off by onboarding step | ↓ | Product + Creator Ops |
| False approve rate (QA sample) | Incorrect approvals / sample | ↓ | Trust & Safety |

→ [Creator Metrics](../../product/success-metrics-overview.md#creator-metrics) · [Trust Metrics](../../product/success-metrics-overview.md#trust-metrics)

---

## Post-Incident / Retro

Run a retro when any of the following occur during a creator launch:

| Trigger | Retro focus |
|---------|-------------|
| False approval discovered post-order | Verification checklist gap; AI flag handling |
| Creator abandoned after 3+ resubmissions | Creator guidance clarity; doc requirements |
| First order cancelled due to platform defect | Capacity/availability system fix |
| SLA breach affecting > 10 creators in a week | Staffing, queue tooling, AI fallback impact |
| Fraudulent creator reached verified status | Fraud detection pipeline; escalation timing |

**Retro template:**

1. Timeline of creator journey (signup → incident)
2. Systems involved (Trust Service events, queue actions, notifications)
3. Root cause — process, tooling, or policy gap
4. Corrective actions with owners and due dates
5. Documentation updates (this playbook, SOPs, creator-facing guides)
6. Whether affected customers require outreach

**Output:** Action items in ops tracker; updates to [`operations/`](../../operations/) SOPs when Phase 4 artifacts exist.

---

## Related Documents

### Flows & pages
- [Creator Onboarding Flow](../../pages/flows/creator-onboarding-flow.md)
- [Trust Verification Flow](../../pages/flows/trust-verification-flow.md)
- [Order Fulfillment Flow](../../pages/flows/order-fulfillment-flow.md)
- [Customer Purchase Flow](../../pages/flows/customer-purchase-flow.md)

### Engineering & AI
- [Trust Service](../../engineering/services/trust-service.md)
- [Verification Assist](../../ai/verification-assist.md)
- [Verification Queue](../../pages/admin/verification-queue.md)

### Creator-facing docs
- [Chef Welcome Package](../onboarding/chef-welcome-package.md)
- [Chef Onboarding Checklist](../onboarding/chef-onboarding-checklist.md)
- [Chef Success Guide](../onboarding/chef-success-guide.md)

### Policy & values
- [Marketplace Mechanics — Trust Model](../../product/marketplace-mechanics.md#trust-model)
- [Company Values](../../company/values.md)
- [Trust & Safety Standards](../standards/trust-and-safety-standards.md) *(when published)*

### Related playbooks
- [Trust & Safety Escalation](trust-safety-escalation.md)
- [Food Safety Incident](food-safety-incident.md)
- [Creator Suspension & Offboarding](creator-suspension-offboarding.md)
- [Fraud Response](fraud-response.md)
