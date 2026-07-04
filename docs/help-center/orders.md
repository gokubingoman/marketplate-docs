# Orders: Tracking, Status, and Changes

> Help Center · Orders  
> Route: `/help/orders`  
> Last updated: 2026-07-03

## Overview

After you place an order, Marketplate tracks it through a clear lifecycle: Confirmed → In production → Ready → In fulfillment → Completed. Status updates appear on [Order Detail](../../pages/customer/order-detail.md) and via [Notifications](notifications.md). The creator prepares your food; Marketplate facilitates payment and trust.

This article explains order statuses, how to track progress, when you can make changes, and what to do when something goes wrong. For cancellations and refunds, see [Refunds & cancellations](refunds.md). For fulfillment specifics, see [Pickup](pickup.md) or [Delivery](delivery.md).

---

## Step-by-step guidance

### Step 1: Find your order

1. Select your account icon → **Order history**, or open the confirmation email link.
2. Select the order to open [Order Detail](../../pages/customer/order-detail.md).
3. From Help, use **Get help with this order** — this attaches order context automatically (`?order=[id]`).

[Screenshot: Order history list with order number, creator name, date, status badge, and total]

### Step 2: Understand order status

| Status | What it means | Your action |
|--------|---------------|-------------|
| **Confirmed** | Payment authorized; creator notified | Note pickup window or delivery ETA |
| **In production** | Creator is preparing your order | Wait for Ready notification; message creator if urgent |
| **Ready** | Order prepared for pickup or dispatch | Proceed to pickup location or await delivery |
| **In fulfillment** | Out for delivery or service in progress | Track per creator instructions |
| **Completed** | Handoff confirmed | Leave a review; contact creator for quality issues |
| **Cancelled / Refunded** | Order did not complete | Refund processes in 5–10 business days |

[Screenshot: Order detail status timeline with current step highlighted and timestamps]

### Step 3: Communicate with the creator

1. On Order Detail, select **Message creator** for order-scoped conversation.
2. Use messaging for pickup questions, dietary clarifications, or timing updates — not for payment disputes.
3. If the creator does not respond within 24 hours, see [Escalation guidance](#escalation-guidance) below.

[Screenshot: Order-scoped messaging thread with creator name, order number header, and text input]

### Step 4: Cancel or modify (when eligible)

1. On Order Detail, look for **Cancel order** — visible only within the creator's cancellation window and before production starts.
2. Custom orders, catering deposits, and batch items may have different rules disclosed at checkout.
3. To change pickup window or items, message the creator before production starts. They may ask you to cancel and re-order if changes are not possible.

[Screenshot: Cancel order button with policy summary tooltip showing cancellation window deadline]

### Step 5: Complete your order

1. Pick up within your scheduled window or receive delivery per instructions.
2. Confirm receipt if prompted, or the order auto-completes after the fulfillment window.
3. You will receive a review prompt after completion — reviews require verified purchase.

[Screenshot: Ready-for-pickup state with address, pickup code, and window time prominently displayed]

---

## Common issues

| Issue | Likely cause | What to do |
|-------|--------------|------------|
| Status stuck on "In production" past window | Creator delay or missed status update | Message creator; escalate if no response 24+ hours |
| Order not ready at pickup time | Production backlog or miscommunication | Message creator; wait on-site if reasonable; see [Pickup](pickup.md) |
| Wrong items received | Fulfillment error | Message creator immediately with photo; request correction or refund |
| Cannot find cancel button | Window closed or production started | See [Refunds & cancellations](refunds.md); contact support if creator agrees |
| Duplicate charge | Payment retry or system error | See [Payments & fees](payments.md); contact support with order number |

---

## FAQs

### How long until my order is ready?

Lead time depends on the creator and item type. Checkout shows the pickup window or delivery estimate before you pay. Batch items and custom orders may require days of lead time — always shown pre-checkout.

### Can I change my order after paying?

Contact the creator via messaging immediately. Changes are at the creator's discretion and may not be possible once production starts. Some changes require cancel-and-reorder.

### What happens if I miss my pickup window?

Creators set their own no-show policies, disclosed at checkout. Food not picked up within the window may be discarded without refund. See [Pickup](pickup.md).

### Who is responsible for my order quality?

The creator is the merchant of record and prepares your food. Marketplate verifies identity and kitchen documentation but does not prepare food. Quality issues: contact the creator first, then support if unresolved.

---

## Related articles

- [Refunds & cancellations](refunds.md) — Cancellation windows and refund timing
- [Pickup](pickup.md) — Pickup windows, codes, and missed pickup
- [Delivery](delivery.md) — Delivery zones and tracking
- [Messaging](messaging.md) — Order-scoped communication rules
- [Payments & fees](payments.md) — Charges, receipts, and fee breakdown
- [Reviews](reviews.md) — Post-order feedback
- [Order detail page spec](../../pages/customer/order-detail.md)
- [Order fulfillment flow](../../pages/flows/order-fulfillment-flow.md)

---

## Escalation guidance

**Contact the creator first** for timing, wrong items, or quality concerns on active orders.

Contact support when:

- Creator is unresponsive for 24+ hours on an active order
- You believe a food safety issue occurred — use **Food safety** category (4-hour response)
- Payment charged incorrectly or refund not received after stated timeline
- You need platform mediation on a dispute after creator contact

**Support category:** Order issue  
**Expected response:** Within 24 hours  
**Include:** Order number, creator name, status, photos if quality issue, summary of creator contact attempts

From Order Detail, select **Get help with this order** to pre-fill context. Critical allergic reactions: **Food safety** category immediately — see [Contact support](contact-support.md).
