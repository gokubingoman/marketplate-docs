# ADR-005: Identity Verification Vendor

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Trust & Safety · Engineering · Legal

---

## Decision

**Pending founder approval.**

Select the third-party vendor for **government ID verification** and liveness checks in creator identity verification — or manual-only review for Phase 1 soft launch.

---

## Background

Creator identity verification is a hard gate ([Marketplace Mechanics](../product/marketplace-mechanics.md#trust-model)). [Verification Assist](../ai/verification-assist.md) extracts document fields and flags tampering — but **humans approve** per [Verification Review SOP](../operations/verification-review-sop.md).

Vendor handles: ID capture, OCR, liveness, document authenticity signals. Trust Service stores verification records and audit trail.

Launch market ([ADR-001](adr-001-geographic-launch-market.md)) affects supported ID types and jurisdictions.

---

## Options

| Option | Vendor / approach | Pros | Cons |
|--------|-------------------|------|------|
| **A — Persona** | ID + liveness API | Food/regulated industry experience; good UX | Cost per verification |
| **B — Stripe Identity** | Integrated with Connect onboarding | Single vendor with payments | Less flexible outside Stripe flow |
| **C — Onfido / Jumio** | Enterprise IDV | Global coverage | Higher cost; enterprise sales cycle |
| **D — Manual only (Phase 1)** | Operators review uploaded docs; no vendor API | Lowest cost; full human control | Slower SLA; higher fraud exposure at scale |

---

## Reasoning (recommended direction)

**Recommend Option D for soft launch** (first 50 creators), **Option A (Persona) for public launch**:

1. Founding cohort size allows manual review with Trust & Safety staffing.
2. Validates verification SOP and AI assist pipeline before vendor spend.
3. Persona (or Stripe Identity if ADR-006 chooses deep Stripe integration) before scaling beyond 100 verifications/month.
4. Vendor signals feed Verification Assist flags — never auto-approve.

Migration trigger: verification queue exceeds 48h SLA for 2 consecutive weeks OR >100 applications/month.

---

## Alternatives considered

- **Vendor from day one** — acceptable if founder prioritizes speed over cost; increases soft launch spend.
- **Stripe Identity only** — tie-break with ADR-006; prefer Persona if Connect onboarding stays separate from identity flow.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Manual phase validates ops before vendor lock-in | Higher operator load early |
| Persona at scale improves fraud detection | Per-check cost |
| Human approval preserved either way | Integration work before public launch |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| Identity verification page | Vendor SDK embed vs upload-only |
| Trust Service | Webhook handlers for vendor results |
| Verification Review SOP | Vendor flag interpretation |
| Data Protection | Vendor DPA, data residency |
| Legal / Privacy Policy | Subprocessor disclosure |

---

## Interim implementation

- Phase 1 soft launch: document upload + Verification Assist + human review only
- Trust Service: `verification.vendor` nullable; `verification.method = manual`
- Feature flag `identity_vendor_enabled` default false

---

## Related Documents

- [Verification Review SOP](../operations/verification-review-sop.md)
- [Verification Assist](../ai/verification-assist.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Identity Verification page](../pages/auth/identity-verification.md)
- [ADR-001 Geographic Launch Market](adr-001-geographic-launch-market.md)
