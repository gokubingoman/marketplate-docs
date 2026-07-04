# Macro Library

> Approved response templates for support operators. Calm, precise, human — per [Voice and Tone](../brand/voice-and-tone.md). Support Assist suggests; **humans edit and send every reply.**

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Customer Support  
**Change control:** Support Lead approval required for new or edited macros. AI cannot add macros.

---

## Purpose

Macros reduce handle time and voice drift while preserving accountability. Each template is a **starting point** — personalize with order details, creator name, and specific timelines before sending.

**Governing rule:** [Humans Decide; AI Assists](../company/values.md#7-humans-decide-ai-assists) — [Support Assist](../ai/support-assist.md) retrieves macros by similarity; operators own the final message.

---

## Usage Rules

### Always

1. **Replace all `[brackets]`** with specific facts — order number, dates, amounts, creator name.
2. **Lead with clarity** — status or next step in the first sentence.
3. **Set explicit next update time** — "I'll follow up by [day, time] [timezone]."
4. **Link Help articles** when educating — use stable routes from [Help Center](../docs/help-center/README.md).
5. **Match audience** — customer vs. creator variants below.

### Never

1. Send a macro without reading the full ticket thread.
2. Promise verification approval, refund approval, or investigation outcomes you cannot guarantee.
3. Use macros for **food safety, allergic reaction, or illness** — see [When NOT to use a macro](#when-not-to-use-a-macro).
4. Copy internal queue names, severity codes, or "Tier 1" language into customer copy.
5. Use empty empathy ("We apologize for any inconvenience") without a concrete action.

### Personalization checklist

Before send, confirm:

- [ ] Creator name used (not "the vendor")
- [ ] Order number and status accurate (admin lookup)
- [ ] Timeline specific (not "soon")
- [ ] One clear next action for the customer
- [ ] Tone matches [Customer Support voice](../brand/voice-and-tone.md#customer-support)

---

## When NOT to Use a Macro

| Situation | Why | What to do instead |
|-----------|-----|-------------------|
| **Allergic reaction reported** | Requires immediate human empathy + T&S handoff | Write custom ack; page T&S — [Escalation Guide](escalation-guide.md#food-safety-and-allergen-incidents) |
| **Illness / food poisoning claim** | P0/P1 incident; legal sensitivity | Custom reply; invoke [Food Safety Incident](../docs/playbooks/food-safety-incident.md) |
| **Suspected allergen mislabeling** | Enforcement investigation | Custom reply; escalate T&S — no fault assignment |
| **Hospital / ER mention** | P0 | Custom reply ≤15 min; T&S on-call |
| **Account takeover** | Security containment | Custom reply; escalate T&S + Eng — [Security](../docs/help-center/security.md) |
| **Harassment or threats** | Moderation path | Custom brief ack; escalate T&S |
| **Customer describes medical emergency in progress** | Direct to emergency services first | Custom reply: seek local emergency care; then support |
| **Active P0/P1 incident (surge mode)** | IC-approved copy only | Use incident comms templates from war room |
| **Legal or regulatory correspondence** | Legal review required | Forward to Legal; no macro |

**Rule of thumb:** If the ticket is tagged `food-safety`, `urgent`, or `P0-candidate`, do not send a library macro as your complete response.

→ [Macro Library integration in Support Assist](../ai/support-assist.md#macro-suggestion)

---

## Order Status

### `macro_order_status_update`

**Use when:** Customer asks where their order is; status available in admin.

**Category:** Order issue  
**Help link:** [Orders](../docs/help-center/orders.md)

---

Hi [Customer name],

I'm looking at order #[order_number] from [Creator name]. Current status: **[status]** — [one-line explanation, e.g., "Your order is in production for pickup Saturday, 11:00–11:30 AM at [address]."]

You can track updates on your [order detail page](../pages/customer/order-detail.md). If you need to reach [Creator name] directly, use **Message creator** on that page.

If anything changes before pickup, I'll follow up by **[date/time]**. Reply here if your question isn't answered.

— [Agent name]  
Marketplate Support

---

### `macro_order_late_pickup`

**Use when:** Customer arrived; order not ready; no safety concern.

**Category:** Order issue  
**Help link:** [Pickup](../docs/help-center/pickup.md)

---

Hi [Customer name],

I understand waiting past your pickup window is frustrating. I've confirmed order #[order_number] with [Creator name] — [Creator name] [has updated the status to Ready / expects your order ready by TIME / asked me to share: specific message from creator thread].

**What you can do now:** [Message creator on order detail / wait on site if creator confirmed X minutes / return at TIME per creator].

If [Creator name] doesn't respond within 24 hours, reply here and I'll mediate next steps.

— [Agent name]  
Marketplate Support

---

### `macro_order_creator_unresponsive`

**Use when:** Customer messaged creator 24+ hours ago; no reply.

**Category:** Order issue  
**Help link:** [Messaging](../docs/help-center/messaging.md)

---

Hi [Customer name],

Thanks for waiting. I see you messaged [Creator name] about order #[order_number] on [date] without a reply yet.

I've notified [Creator name] through our creator channel and asked for a response by **[date/time]**. Order status remains **[status]**.

If we don't hear back by then, I'll [propose refund mediation / update you on cancellation options / specific next step].

— [Agent name]  
Marketplate Support

---

### `macro_order_wrong_item`

**Use when:** Quality/fulfillment error; not food safety.

**Category:** Order issue  
**Help link:** [Orders](../docs/help-center/orders.md) · [Refunds](../docs/help-center/refunds.md)

---

Hi [Customer name],

I'm sorry order #[order_number] didn't arrive as expected. I reviewed your message [and photo] — you received [what they got] instead of [what was ordered].

**Recommended next step:** [Creator name] can [remake / offer partial refund / full refund] per their policy. I've asked them to respond by **[date/time]**.

If you'd prefer Marketplate to mediate a refund directly, tell me and I'll begin that review once the creator window passes or if they agree in writing.

— [Agent name]  
Marketplate Support

---

## Refunds & Cancellations

### `macro_refund_eligible_cancel`

**Use when:** Customer cancelled within policy; refund processing.

**Category:** Payment & refund  
**Help link:** [Refunds](../docs/help-center/refunds.md)

---

Hi [Customer name],

Your cancellation for order #[order_number] is confirmed. Refund amount: **$[amount]** to your original payment method.

Refunds typically appear in **5–10 business days** after processing, depending on your bank. Status on your [order detail](../pages/customer/order-detail.md): **[Requested / Approved / Processed]**.

Reply if you don't see the refund after 10 business days from the processed date.

— [Agent name]  
Marketplate Support

---

### `macro_refund_creator_initiated`

**Use when:** Creator cancelled; automatic full refund.

**Category:** Payment & refund

---

Hi [Customer name],

[Creator name] cancelled order #[order_number]. You receive a **full refund of $[amount]** automatically — no action needed.

Funds return to your original payment method in **5–10 business days**. We're sorry this order didn't complete.

If you'd like help finding another creator, visit [Browse](../pages/customer/browse.md) or reply with your preferences.

— [Agent name]  
Marketplate Support

---

### `macro_refund_mediation_started`

**Use when:** Customer and creator disagree; Support investigating.

**Category:** Payment & refund  
**Help link:** [Refunds](../docs/help-center/refunds.md) · [Platform policies](../docs/help-center/platform-policies.md)

---

Hi [Customer name],

I'm reviewing your refund request for order #[order_number]. I've read your conversation with [Creator name] and the checkout policy acknowledged at purchase.

**My next step:** [Specific action — e.g., request photos, confirm production start time, review policy window].

I'll reply with a decision or next question by **[date/time]**. Refunds, if approved, process in **5–10 business days** after approval.

— [Agent name]  
Marketplate Support

---

### `macro_refund_outside_window`

**Use when:** Policy does not allow refund; empathetic decline with options.

**Category:** Payment & refund  
**Do not use if:** Customer alleges misrepresentation or safety issue — escalate.

---

Hi [Customer name],

I reviewed order #[order_number] against the cancellation policy shown at checkout: [brief policy summary — e.g., "Cancellations after production starts are not eligible for refund"].

I can't approve a refund under that policy. If you believe the policy was misrepresented or circumstances were exceptional, reply with details and I'll escalate for a second review.

— [Agent name]  
Marketplate Support

---

## Verification (Creators)

### `macro_verification_in_review`

**Use when:** Creator asks status; submission in queue.

**Category:** Creator verification  
**Help link:** [Verification](../docs/help-center/verification.md)

---

Hi [Creator name],

Your [identity / kitchen / compliance] verification submitted on **[date]** is **In review**. Our team typically completes review within **2 business days** per submission.

You'll receive email and dashboard notification when status changes. No action needed unless we request additional documents.

Expected decision by: **[date — 2 business days from submission]**.

— [Agent name]  
Marketplate Support

---

### `macro_verification_needs_action`

**Use when:** Admin shows "Needs action" with specific deficiency (read admin — do not invent reasons).

**Category:** Creator verification  
**Help link:** [Verification](../docs/help-center/verification.md) · [Kitchen Verification](../pages/auth/kitchen-verification.md)

---

Hi [Creator name],

Your verification needs an update before we can continue review. **Requested item:** [specific deficiency from admin — e.g., "Kitchen photo showing production area" / "Renewed food handler certificate"].

**What to do:** Open your verification dashboard, upload the corrected document, and submit. Review restarts when we receive the update — typically **2 business days**.

If anything in the request is unclear, reply with your question and I'll clarify. I can't approve verification from support; our trust team makes final decisions.

— [Agent name]  
Marketplate Support

---

### `macro_verification_approved`

**Use when:** Admin confirms approved; creator hasn't seen notification.

**Category:** Creator verification  
**Help link:** [Chef Success Guide](../docs/onboarding/chef-success-guide.md)

---

Hi [Creator name],

Your verification is **approved**. You can publish paid listings and accept orders.

**Suggested next steps:**
1. Publish your first menu item — [Menus help](../docs/help-center/menus.md)
2. Complete your storefront profile — [Storefronts](../docs/help-center/storefronts.md)
3. Share your storefront link with your network

Welcome to Marketplate. Reply if you hit a technical issue publishing.

— [Agent name]  
Marketplate Support

---

## Allergens & Dietary (Non-Emergency)

> **Not for reactions or illness.** Education and pre-order questions only.

### `macro_allergen_disclosure_explain`

**Use when:** Customer asks how allergens work; no incident reported.

**Category:** General inquiry  
**Help link:** [Food safety & allergens](../docs/help-center/food-safety.md)

---

Hi [Customer name],

Creators disclose allergens on each menu item — look for **Contains** and **May contain** on the item page before ordering. Marketplate does not prepare food and cannot guarantee allergen-free preparation, even in shared kitchens.

**For severe allergies:** Review item disclosures, add a note at checkout, and message [Creator name] before production starts to ask about cross-contact.

Full guidance: [Food safety & allergens](../docs/help-center/food-safety.md).

— [Agent name]  
Marketplate Support

---

### `macro_allergen_checkout_ack`

**Use when:** Customer confused by checkout acknowledgment checkbox.

**Category:** General inquiry  
**Help link:** [Food safety](../docs/help-center/food-safety.md) · [Checkout](../pages/customer/checkout.md)

---

Hi [Customer name],

The checkout acknowledgment confirms you've reviewed allergen information for your items. It's required when your order includes flagged allergens or saved dietary preferences — it does not replace reading each item's disclosure.

If you need to verify an ingredient, message the creator from your order before production starts.

— [Agent name]  
Marketplate Support

---

### `macro_allergen_non_emergency_report`

**Use when:** Customer reports labeling concern **without** symptoms or consumption of unsafe food.

**Category:** Order issue → may escalate to T&S  
**Caution:** If any symptoms mentioned, stop — use [Escalation Guide](escalation-guide.md).

---

Hi [Customer name],

Thank you for reporting a labeling concern on order #[order_number]. I've documented: [summary of concern].

Our trust team reviews allergen disclosure accuracy. **I won't assign an outcome yet** — you'll hear from us by **[date/time]** after review.

Please retain [packaging / photos] if safe to store. If you experience any symptoms, seek medical care and reply immediately — don't wait for this thread.

— [Agent name]  
Marketplate Support

---

## Delivery

### `macro_delivery_status`

**Use when:** Customer asks about delivery timing; order in fulfillment.

**Category:** Order issue  
**Help link:** [Delivery](../docs/help-center/delivery.md)

---

Hi [Customer name],

Order #[order_number] from [Creator name] is **[status]**. Delivery window: **[start–end time]** to **[address]**.

[Creator name] [provides tracking at / asked to message for updates / confirmed driver dispatched]. Check [order detail](../pages/customer/order-detail.md) for status changes.

If delivery passes the window without update, message [Creator name] first, then reply here after 24 hours.

— [Agent name]  
Marketplate Support

---

### `macro_delivery_outside_zone`

**Use when:** Customer cannot checkout; address outside creator zone.

**Category:** General inquiry  
**Help link:** [Delivery](../docs/help-center/delivery.md)

---

Hi [Customer name],

[Creator name]'s delivery zone doesn't include **[address]** at this time. Checkout validates your address against their zone before payment.

**Options:** Choose pickup if offered, try another creator who delivers to your area via [Search](../pages/customer/search.md), or save the address for when the creator expands their zone.

— [Agent name]  
Marketplate Support

---

### `macro_delivery_missing_items`

**Use when:** Delivery completed; items missing; not safety issue.

**Category:** Order issue  
**Help link:** [Delivery](../docs/help-center/delivery.md)

---

Hi [Customer name],

I'm sorry items were missing from order #[order_number]. Please confirm which items didn't arrive: [list].

I've contacted [Creator name] for [redelivery / partial refund / full refund for missing items] and asked for a response by **[date/time]**. Send photos if you have them.

— [Agent name]  
Marketplate Support

---

## Account

### `macro_account_password_reset`

**Use when:** Customer locked out; standard reset flow.

**Category:** General inquiry  
**Help link:** [Security](../docs/help-center/security.md) · [Account](../docs/help-center/account.md)

---

Hi [Customer name],

Use **Forgot password** on the sign-in page to reset your password via email. The link expires in **[X hours]** — request a new one if needed.

If you don't receive the email within 10 minutes, check spam and confirm you're using **[account email on file]**.

If you suspect unauthorized access, reply immediately — we'll secure your account.

— [Agent name]  
Marketplate Support

---

### `macro_account_email_change`

**Use when:** Customer requests email update.

**Category:** General inquiry  
**Help link:** [Account](../docs/help-center/account.md)

---

Hi [Customer name],

Update your email in [Account settings](../pages/customer/account-settings.md) → **Profile**. You may need to verify the new address before it becomes primary.

If you no longer have access to your old email, reply from an address you can access and include [verification steps per security policy — e.g., last order number, last 4 of payment method if applicable]. We'll verify identity before making changes.

— [Agent name]  
Marketplate Support

---

### `macro_account_delete_request`

**Use when:** Customer requests account deletion.

**Category:** General inquiry  
**Help link:** [Account](../docs/help-center/account.md) · [Privacy](../docs/help-center/privacy.md)

---

Hi [Customer name],

You can request account deletion in [Account settings](../pages/customer/account-settings.md) → **Privacy**. Deletion is processed within **[X business days]** per our privacy policy.

**Before you delete:** Active orders must be completed or cancelled. Order history required for tax/refund records may be retained as described in [Privacy](../docs/help-center/privacy.md).

Reply if you need help with an open order first.

— [Agent name]  
Marketplate Support

---

### `macro_account_notification_prefs`

**Use when:** Customer wants fewer emails/pushes.

**Category:** General inquiry  
**Help link:** [Notifications](../docs/help-center/notifications.md)

---

Hi [Customer name],

Manage notifications in [Account settings](../pages/customer/account-settings.md) → **Notifications**. Toggle order updates, marketing, and creator messages independently.

Order status updates for active orders remain on by default so you don't miss pickup windows — you can adjust after delivery completes.

— [Agent name]  
Marketplate Support

---

## General & Closing

### `macro_first_response_ack`

**Use when:** Complex ticket; need investigation time.

**Category:** Any (except food safety as sole response)

---

Hi [Customer name],

Thank you for contacting Marketplate about [brief topic]. I'm reviewing [order #[order_number] / your account / your verification submission] now.

I'll reply with a full update by **[date/time] [timezone]**. If you have additional details before then, reply to this email.

— [Agent name]  
Marketplate Support

---

### `macro_resolution_close`

**Use when:** Issue resolved; closing ticket.

---

Hi [Customer name],

I'm glad we could [resolve summary — e.g., "confirm your refund is processed" / "clarify your pickup time"].

If anything else comes up within 14 days, reply to reopen this case. For new issues, submit a fresh request from [Help](../pages/customer/help.md) so we attach the right context.

— [Agent name]  
Marketplate Support

---

### `macro_escalation_handoff`

**Use when:** Transferring to T&S, Ops, or specialist — customer-facing notice only.

---

Hi [Customer name],

I'm escalating your case to our **[trust team / payments team / specialist]** for [reason in plain language — e.g., "allergen disclosure review" / "refund processing"].

**What changes:** A specialist will contact you by **[date/time]**. Your case reference: **[ticket_id]**.

You don't need to resubmit. Reply here if your situation changes urgently.

— [Agent name]  
Marketplate Support

---

## Macro Index

| ID | Category | Use case |
|----|----------|----------|
| `macro_order_status_update` | Order | Status inquiry |
| `macro_order_late_pickup` | Order | Late at pickup |
| `macro_order_creator_unresponsive` | Order | Creator silent 24h+ |
| `macro_order_wrong_item` | Order | Wrong/missing item (non-safety) |
| `macro_refund_eligible_cancel` | Refund | Cancel refund processing |
| `macro_refund_creator_initiated` | Refund | Creator cancelled |
| `macro_refund_mediation_started` | Refund | Dispute investigation |
| `macro_refund_outside_window` | Refund | Policy decline |
| `macro_verification_in_review` | Verification | Queue status |
| `macro_verification_needs_action` | Verification | Resubmission required |
| `macro_verification_approved` | Verification | Approved notification |
| `macro_allergen_disclosure_explain` | Allergen | Education only |
| `macro_allergen_checkout_ack` | Allergen | Checkout checkbox help |
| `macro_allergen_non_emergency_report` | Allergen | Label concern, no symptoms |
| `macro_delivery_status` | Delivery | In-transit inquiry |
| `macro_delivery_outside_zone` | Delivery | Zone validation |
| `macro_delivery_missing_items` | Delivery | Post-delivery missing items |
| `macro_account_password_reset` | Account | Password help |
| `macro_account_email_change` | Account | Email update |
| `macro_account_delete_request` | Account | Deletion request |
| `macro_account_notification_prefs` | Account | Notification settings |
| `macro_first_response_ack` | General | Investigation pending |
| `macro_resolution_close` | General | Ticket close |
| `macro_escalation_handoff` | General | Specialist transfer |

---

## Maintenance

| Trigger | Action |
|---------|--------|
| Policy change in Help or legal | Review affected macros; bump version |
| High macro edit distance in Support Assist | Rewrite template for clarity |
| New recurring ticket theme | Propose new macro — Support Lead approval |
| Food safety language drift | Audit — ensure no macro implies guaranteed safety |
| Quarterly review | Voice checklist on all macros |

Submit changes via internal doc PR tagged `support-macros`.

---

## Related Documents

- [Support Playbook](support-playbook.md)
- [Escalation Guide](escalation-guide.md)
- [Support Assist](../ai/support-assist.md)
- [Voice and Tone — Customer Support](../brand/voice-and-tone.md#customer-support)
- [Help Center](../docs/help-center/README.md)
- [Contact Support](../docs/help-center/contact-support.md)
- [Food Safety & Allergens](../docs/help-center/food-safety.md)
- [Support Onboarding](../docs/training/support-onboarding.md)
