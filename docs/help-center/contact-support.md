# Contact Support

> Help Center · Contact support  
> Route: `/help/contact-support`  
> Last updated: 2026-07-03

## Overview

Contact support when self-service articles and creator messaging do not resolve your issue. Support specialists investigate order, payment, account, verification, and trust concerns with clear response timelines. Food safety and account security issues receive priority routing.

This article explains how to reach support, what to include, expected response times, and escalation paths. In-app form lives on the [Help page](../../pages/customer/help.md) — anchor `#contact`.

---

## Step-by-step guidance

### Step 1: Try self-service first

1. Search Help articles — start with [Troubleshooting](troubleshooting.md) for technical issues.
2. For active orders, message the creator via [Messaging](messaging.md) before escalating.
3. Review policy articles: [Refunds](refunds.md), [Payments](payments.md), [Food safety](food-safety.md).

[Screenshot: Help page search bar with suggested articles dropdown as user types "refund"]

Self-service deflects preventable volume and often resolves issues faster.

### Step 2: Open the support form

1. Go to **Help** → scroll to **Contact support** or visit `/help/contact-support`.
2. From [Order Detail](../../pages/customer/order-detail.md), select **Get help with this order** — pre-fills order context (`?order=[id]`).
3. Unauthenticated users may submit — email required.

[Screenshot: Contact support section with category dropdown, name, email, message fields, and order attach checkbox]

### Step 3: Select the right category

| Category | Use for |
|----------|---------|
| **General inquiry** | Account questions, how-to, accessibility barriers |
| **Order issue** | Late order, wrong item, pickup/delivery problem |
| **Payment & refund** | Charges, refunds after 10 days, dispute mediation |
| **Food safety** | Illness, allergic reaction, mislabeling — **priority** |
| **Account security** | Unauthorized access, suspicious activity — **priority** |
| **Creator verification** | Verification status, document review (creators) |
| **Trust & safety** | Fraud, harassment, policy violations, fake reviews |

[Screenshot: Category dropdown expanded showing all categories with Food safety and Account security marked Priority]

### Step 4: Write an effective message

Include:

1. **Order number** (if applicable) — auto-attached when using order help link
2. **Creator name**
3. **What happened** — specific dates and times
4. **What you need** — refund, status update, investigation
5. **What you tried** — creator messages, troubleshooting steps
6. **Evidence** — photos for quality or safety issues

[Screenshot: Example well-formed support message with labeled sections highlighted as best practice]

Do not include: full payment card numbers, government ID numbers, passwords.

### Step 5: Submit and track response

1. Select **Submit** → confirmation toast: "We typically respond within 24 hours."
2. Priority categories: Food safety (4 hours target); Account security (4 hours); allergic reaction critical (1 hour target).
3. Reply arrives via email — respond in thread to keep case context.
4. Duplicate submission guard: button disabled 30 seconds after success.

[Screenshot: Success confirmation card replacing form with case reference number and expected response window]

---

## Response timelines

| Category | Target response | Notes |
|----------|-----------------|-------|
| General inquiry | 24 hours | Business days |
| Order issue | 24 hours | Creator contact attempts noted |
| Payment & refund | 24–48 hours | Complex disputes may extend |
| Food safety | 4 hours | Seek medical care first for emergencies |
| Allergic reaction | 1 hour | **Call emergency services first** |
| Account security | 4 hours | May temporarily lock account |
| Creator verification | 2 business days | Include submission date |
| Trust & safety | 24 hours | Elevated for active fraud |

Timelines are targets, not guarantees — per [operations philosophy](../../company/constitution.md#operations-philosophy).

---

## Escalation paths

```
Self-service article → Creator message (orders) → Support form → Specialist investigation → Trust & Safety / Payments ops
```

| Situation | Escalation |
|-----------|------------|
| Support no response past SLA | Reply to case email requesting escalation |
| Dispute outcome disputed | Appeal within window in resolution email — [Platform policies](platform-policies.md) |
| Safety emergency | Medical care first → Food safety category → local authorities if criminal |
| Legal request | Attorney correspondence via legal contact in terms (Phase 5) |

Support cannot override checkout-acknowledged policies without investigation findings.

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| Submit support form | ✓ (email required) | ✓ (pre-filled) |
| Attach order to ticket | Manual order # entry | ✓ own orders via picker or `?order=` |
| View order context banner | ✗ | ✓ own order only |

---

## Common issues

| Issue | Likely cause | What to do |
|-------|--------------|------------|
| Submit failed | Network error | Retry; check connection |
| Rate limited | Multiple rapid submissions | Wait 1 hour |
| Order not attaching | Not signed in; wrong order | Sign in; enter order # manually |
| No reply after 48 hours | Spam filter; wrong email | Check spam; verify account email |
| Wrong category selected | Misrouted ticket | Reply to email with correct category request |

---

## FAQs

### Can I call Marketplate?

Phone support availability varies by market and phase. Email/form is primary channel — check Help page for current phone hours if listed.

### Can creators contact support?

Yes. Use **Creator verification** for onboarding; **General inquiry** for dashboard issues. Creator OS help expands in future phases.

### Will support share my message with the creator?

Order and dispute investigations may require creator contact with relevant facts. Safety investigations may proceed with limited disclosure.

### How do I reopen a closed case?

Reply to the case email within 14 days with new information. New issues: submit fresh form with prior case number referenced.

---

## Related articles

- [Troubleshooting](troubleshooting.md) — Before contacting support
- [Orders](orders.md) — Order-specific help entry
- [Refunds & cancellations](refunds.md) — Refund disputes
- [Food safety & allergens](food-safety.md) — Priority safety routing
- [Security](security.md) — Account compromise
- [Platform policies](platform-policies.md) — Appeals
- [Help page spec — Contact support section](../../pages/customer/help.md#contact-support)
- [Help Center README](README.md) — Architecture and SLAs

---

## Escalation guidance

**This is the escalation endpoint.** For issues requiring immediate emergency services, call local emergency number first — do not wait for support.

After submitting:

- **Food safety / allergic reaction:** Monitor email and phone if provided; keep affected product per safe storage guidance in case follow-up questions arise.
- **Account security:** Change password if you retain access; watch for confirmation of account lock.
- **Unresolved after SLA:** Reply to ticket email with "Escalation requested" and original submission time.

**API reference:** `POST /api/v1/support/tickets` — payload: `category`, `name`, `email`, `message`, optional `order_id`, `referrer_page`.

We are accountable for resolution — per brand voice: empathetic, specific timelines, no blame shifting.
