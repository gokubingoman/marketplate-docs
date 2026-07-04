# Payments & Fees

> Help Center · Payments  
> Route: `/help/payments`  
> Last updated: 2026-07-03

## Overview

Marketplate shows your full order total before you pay — item prices set by the creator, platform service fee, tax, and any deposits or custom-order terms. There are no hidden fees at checkout. The creator is the merchant of record; Marketplate facilitates payment and trust verification.

This article explains what you pay, when you are charged, receipts, and common payment issues. For refunds, see [Refunds & cancellations](refunds.md).

---

## Step-by-step guidance

### Step 1: Review your cart total

1. Open [Cart](../../pages/customer/cart.md) before checkout.
2. Review line items: product subtotal, platform service fee, estimated tax, and **Order total**.
3. Select the fee info icon to read what the service fee covers — verification, payments infrastructure, and customer support.

[Screenshot: Cart summary panel with itemized subtotal, service fee with info icon, tax estimate, and bold total]

### Step 2: Understand fees

| Line item | Description |
|-----------|-------------|
| **Item subtotal** | Sum of menu prices set by the creator |
| **Platform service fee** | Supports verification, payments, and support — shown explicitly, not embedded in item price |
| **Tax** | Calculated by jurisdiction and fulfillment type (pickup vs. delivery) |
| **Deposit** (if applicable) | Custom orders, catering — balance due date shown at checkout |
| **Order total** | Full amount charged (or deposit amount for split-payment orders) |

Fees support the trust infrastructure described in [Marketplace Mechanics](../../product/marketplace-mechanics.md) — verification, audit trails, and dispute mediation.

[Screenshot: Checkout fee breakdown expanded with tooltip explaining service fee purpose]

### Step 3: Enter payment and confirm

1. On [Checkout](../../pages/customer/checkout.md), select or enter your payment method.
2. Review fulfillment details, cancellation policy acknowledgment, and allergen acknowledgment if required.
3. Select **Place order**. Payment is authorized at confirmation; capture timing aligns to fulfillment model.
4. Receive confirmation on-screen and via email with receipt.

[Screenshot: Checkout payment section with card fields, saved payment method option, and "Place order" button]

### Step 4: Access receipts

1. Open [Order history](../../pages/customer/order-history.md) or the order confirmation email.
2. Select **View receipt** on [Order Detail](../../pages/customer/order-detail.md).
3. Receipts include itemized charges, fees, tax, payment method (last four digits), and order number for expense reporting.

[Screenshot: Order receipt view with itemized lines, fee, tax, payment method last four digits, and download PDF option]

---

## Common issues

| Issue | Likely cause | What to do |
|-------|--------------|------------|
| Payment declined | Insufficient funds, expired card, bank block | Verify card details; contact bank; try another method |
| Charged but no confirmation | Network interruption during submit | Check Order history before retrying; contact support if duplicate charge |
| Tax higher than expected | Jurisdiction rules for delivery address | Tax calculated on fulfillment location — shown before payment |
| Deposit charged, balance unclear | Custom or catering order | Balance due date on Order Detail and confirmation email |
| Fee different from last order | Different creator, fulfillment type, or tax jurisdiction | Each order calculates independently — review cart before paying |

---

## FAQs

### What payment methods are accepted?

Major credit and debit cards (Visa, Mastercard, American Express, Discover). Additional methods may roll out by market. Payment details are tokenized — Marketplate does not store full card numbers.

### When am I charged?

Standard orders: payment authorized at checkout and captured per fulfillment model. Custom orders may charge a deposit at booking with balance before the event date — always disclosed pre-payment.

### Why is there a platform service fee?

The fee supports identity and kitchen verification, secure payments, customer support, and platform integrity. It is shown separately so item prices reflect what the creator sets.

### Can I pay with cash?

Marketplate orders require electronic payment at checkout. Creators cannot accept cash through the platform for tracked orders.

### How do tips work?

If tipping is enabled for a creator, it appears as an optional line at checkout. Tips go to the creator per their payout settings.

---

## Related articles

- [Refunds & cancellations](refunds.md) — Refund timing and partial refunds
- [Orders](orders.md) — Order confirmation and status
- [Cart page spec](../../pages/customer/cart.md) — Fee explainer entry point (`#fees`)
- [Checkout page spec](../../pages/customer/checkout.md)
- [Marketplace Mechanics — Transactions](../../product/marketplace-mechanics.md#transactions)

---

## Escalation guidance

Contact support for payment issues:

- Duplicate charge or charged without order confirmation
- Refund not received after 10 business days
- Incorrect amount charged vs. checkout total shown
- Unauthorized transaction on your account

**Support category:** Payment & refund  
**Expected response:** Within 24–48 hours  
**Include:** Order number, charge amount, date, last four digits of card, screenshot of checkout total if available

For unauthorized charges, also see [Security](security.md) and use **Account security** if you suspect account compromise.
