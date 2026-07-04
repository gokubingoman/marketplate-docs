# ADR-006: Stripe Connect Account Model

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Finance · Engineering · Legal

---

## Decision

**Pending founder approval.**

Select Stripe Connect account type (**Express**, **Standard**, or **Custom**) and onboarding flow for creator payouts.

---

## Background

[Payment Service](../engineering/services/payment-service.md) implements creator-as-merchant-of-record with Marketplate as marketplace facilitator. Connect model affects:

- Creator onboarding UX (Stripe-hosted vs embedded)
- Platform control over payout timing and holds
- Compliance burden (KYC, 1099 reporting)
- Integration with [ADR-003 Commission Structure](adr-003-commission-structure.md)

Stripe Identity overlap: see [ADR-005 Identity Verification Vendor](adr-005-identity-verification-vendor.md).

---

## Options

| Option | Connect type | Creator experience | Platform control |
|--------|--------------|-------------------|------------------|
| **A — Express** | Stripe-hosted onboarding + Express Dashboard | Fastest creator setup | Good — application fees, payout schedule |
| **B — Standard** | Creator has full Stripe account | Most creator autonomy | Less platform control; weaker marketplace UX |
| **C — Custom** | Fully embedded; platform owns UI | Best branded UX | Highest build + compliance burden |

---

## Reasoning (recommended direction)

**Recommend Option A — Stripe Connect Express:**

1. Industry standard for marketplaces at Phase 1 scale.
2. Stripe handles KYC/tax onboarding — reduces legal surface for Marketplate.
3. Supports `application_fee_amount` for commission ([ADR-003](adr-003-commission-structure.md)).
4. Express Dashboard sufficient for creator payout visibility until Chef OS matures.
5. Custom (Option C) deferred until Phase 4 Chef OS when embedded finance is strategic.

**Payout schedule:** weekly per ADR-003. **Instant payout** gated to Trusted Chef tier only (future).

---

## Alternatives considered

- **Standard accounts** — rejected; creators manage separate Stripe relationship — weakens OS narrative.
- **Custom from launch** — rejected; 3–6 month compliance overhead not justified pre-liquidity.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Fast creator payment onboarding | Stripe-branded Express Dashboard elements |
| Platform fee collection native | Stripe fees + platform commission visible separately |
| Proven marketplace pattern | Less UX control than Custom |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| Creator signup flow | Connect onboarding step |
| Payment Service | Connect account creation webhooks |
| Creator payouts page | Express Dashboard deep links |
| Payout Processing SOP | Stripe-specific runbooks |
| Legal | Stripe terms incorporation in Creator Agreement |

---

## Interim implementation

- Payment Service: `connect_account_type: express` in config (assumption)
- Staging: Stripe test mode Connect accounts
- Do not enable live Connect until ADR **Accepted** + legal counsel sign-off

---

## Related Documents

- [ADR-003 Commission Structure](adr-003-commission-structure.md)
- [Payment Service](../engineering/services/payment-service.md)
- [Payout Processing SOP](../operations/payout-processing-sop.md)
- [Creator Agreement — Payouts](../legal/creator-agreement.md)
