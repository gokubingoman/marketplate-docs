# Chef Onboarding Checklist

> Step-by-step pre-launch checklist for independent food creators — every item with what, why, where, and done criteria.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Audience:** Creators preparing to go live on Marketplate

---

## Purpose

This checklist translates [Creator Onboarding Flow](../../pages/flows/creator-onboarding-flow.md) into actionable tasks. Complete every section before sharing your storefront publicly. Items are ordered by dependency — verification gates must clear before publish.

For narrative context and best practices, see [Chef Welcome Package](chef-welcome-package.md). For post-launch growth, see [Chef Success Guide](chef-success-guide.md).

---

## How to Use This Checklist

| Column | Meaning |
|--------|---------|
| **What** | The task to complete |
| **Why** | Business or trust rationale |
| **Where** | Product location (route and page spec) |
| **Done when** | Objective completion criteria |

Check items off as you complete them. Dashboard activation checklist mirrors items 9–15 after verification.

---

## 1. Account

### 1.1 Create creator account

| | |
|---|---|
| **What** | Sign up with email, legal name, business type, storefront slug, jurisdiction, and creator category |
| **Why** | Initializes your profile, compliance checklist, and public URL (`marketplate.com/creators/your-slug`) |
| **Where** | `/creator/signup` — [Creator Signup flow](../../pages/flows/creator-onboarding-flow.md#phase-1--creator-signup) |
| **Done when** | Account created; redirected to Identity Verification; slug reserved and preview visible |

### 1.2 Confirm business type and jurisdiction

| | |
|---|---|
| **What** | Select sole proprietor, LLC, or partnership; confirm state/locality |
| **Why** | Drives compliance document requirements and cottage food category rules |
| **Where** | Signup form; editable in [Compliance](../../pages/creator/compliance.md) if correction needed pre-approval |
| **Done when** | Business type and jurisdiction saved; compliance checklist reflects correct rules |

### 1.3 Select creator category

| | |
|---|---|
| **What** | Choose chef, baker, meal prep, food truck, cottage food, caterer, pop-up, or other |
| **Why** | Persona-specific onboarding prompts (lead times, commissary linkage, category restrictions) |
| **Where** | Signup form |
| **Done when** | Category selected; persona-appropriate checklist items visible in compliance center |

---

## 2. Verification (Identity)

### 2.1 Submit government ID and liveness check

| | |
|---|---|
| **What** | Upload government-issued photo ID; complete selfie/liveness verification |
| **Why** | Confirms you are a real, accountable operator — foundation of "Verified Creator" status |
| **Where** | `/creator/verify/identity` — [Identity Verification](../../pages/flows/creator-onboarding-flow.md#phase-2--identity-verification) |
| **Done when** | Documents submitted; status = `identity_in_review` or `approved` |

### 2.2 Submit business registration (if applicable)

| | |
|---|---|
| **What** | Upload business registration for LLC or partnership |
| **Why** | Entity verification for non-sole-proprietor operators |
| **Where** | `/creator/verify/identity` |
| **Done when** | Registration document uploaded and accepted by quality check (no blur/glare rejections) |

### 2.3 Complete tax identity and phone verification

| | |
|---|---|
| **What** | Provide EIN or tax identity where applicable; verify phone number |
| **Why** | Required for payouts, 1099 reporting, and account recovery |
| **Where** | `/creator/verify/identity` |
| **Done when** | Tax identity on file; phone verified via SMS or call |

### 2.4 Identity approval

| | |
|---|---|
| **What** | Wait for human review (typically 2 business days); address any action-required items |
| **Why** | Unapproved identity blocks kitchen verification and paid listings |
| **Where** | `/creator/verify/identity` · [Compliance](../../pages/creator/compliance.md) status panel |
| **Done when** | Status = `approved`; Kitchen Verification unlocked |

---

## 3. Kitchen

### 3.1 Select kitchen type

| | |
|---|---|
| **What** | Choose home/cottage, commercial shared, dedicated facility, commissary, or multi-tenant bay |
| **Why** | Determines required artifacts and verification path |
| **Where** | `/creator/verify/kitchen` — [Kitchen Verification](../../pages/flows/creator-onboarding-flow.md#phase-3--kitchen-verification) |
| **Done when** | Kitchen type selected; type-specific upload fields displayed |

### 3.2 Submit production address and facility photos

| | |
|---|---|
| **What** | Provide validated production address; upload photos of prep area, storage, and handwashing station |
| **Why** | Customers trust food from known, verified environments; every SKU must link to a verified location |
| **Where** | `/creator/verify/kitchen` |
| **Done when** | Address validated; minimum photo set uploaded (clear, well-lit, current) |

### 3.3 Submit facility documentation

| | |
|---|---|
| **What** | Upload inspection records (where available), facility registration/license; for food trucks: commissary agreement and unit ID |
| **Why** | Documentation consistency check; mobile operators must link to approved commissary |
| **Where** | `/creator/verify/kitchen` · [Compliance](../../pages/creator/compliance.md) |
| **Done when** | All type-required documents submitted |

### 3.4 Kitchen approval (or tenant link)

| | |
|---|---|
| **What** | Complete review, or link to pre-verified commercial kitchen via facility invite code |
| **Why** | Kitchen verification gates catalog publish |
| **Where** | `/creator/verify/kitchen` · [Compliance](../../pages/creator/compliance.md) |
| **Done when** | Status = `approved`; at least one verified production location available in Menu Item Editor |

---

## 4. Identity (Ongoing Profile)

### 4.1 Complete public creator identity

| | |
|---|---|
| **What** | Add profile photo, cover image, and creator story |
| **Why** | Storefront conversion depends on human connection; incomplete profiles underperform in discovery |
| **Where** | `/dashboard/storefront` — [Storefront Settings](../../pages/creator/storefront-settings.md) |
| **Done when** | Profile photo uploaded; story ≥ 2 paragraphs; cover image set; preview looks professional on mobile |

### 4.2 Confirm public slug and brand name

| | |
|---|---|
| **What** | Verify storefront slug and display name match your brand |
| **Why** | Slug change triggers redirect policy; early correction avoids broken links |
| **Where** | `/dashboard/storefront` |
| **Done when** | Slug and brand name finalized; shareable URL tested |

---

## 5. Tax

### 5.1 Provide tax identity for reporting

| | |
|---|---|
| **What** | Ensure EIN or SSN on file matches your business entity type |
| **Why** | Required for year-end tax reporting and Stripe compliance |
| **Where** | Identity verification · Stripe onboarding |
| **Done when** | Tax identity verified; no outstanding tax info requests in dashboard |

### 5.2 Understand sales tax responsibility

| | |
|---|---|
| **What** | Review how tax is calculated and displayed at checkout for your jurisdiction |
| **Why** | You are merchant of record; tax handling varies by location |
| **Where** | Checkout preview · [Marketplace Mechanics — Transactions](../../product/marketplace-mechanics.md#transactions) |
| **Done when** | You understand whether tax is collected at checkout and your remittance obligations |

---

## 6. Stripe

### 6.1 Connect payout account

| | |
|---|---|
| **What** | Complete Stripe Express onboarding — bank account, identity confirmation |
| **Why** | No connected account = no payouts; required before first paid order settles |
| **Where** | `/creator/payouts` — [Payouts](../../pages/creator/payouts.md) · onboarding prompt on [Dashboard](../../pages/creator/dashboard.md) |
| **Done when** | Stripe status = connected; payout schedule visible; test deposit path confirmed |

### 6.2 Review fee structure

| | |
|---|---|
| **What** | Understand platform fee deduction and net payout calculation |
| **Why** | Transparent economics prevent "where's my money?" support issues |
| **Where** | `/creator/payouts` · order confirmation in test checkout |
| **Done when** | You can articulate gross → fees → net for a sample order |

---

## 7. Photos

### 7.1 Prepare listing photography

| | |
|---|---|
| **What** | Shoot real food photos: primary + optional angles; min 1200px longest edge; JPG/PNG |
| **Why** | Photography drives discovery conversion; stock imagery rejected |
| **Where** | Local shoot → upload in [Menu Item Editor](../../pages/creator/menu-item-editor.md) |
| **Done when** | At least one photo per planned launch item; accurate representation of portion and plating |

### 7.2 Upload storefront imagery

| | |
|---|---|
| **What** | Profile photo, cover image, and optional gallery |
| **Why** | Storefront is primary conversion surface before catalog browse |
| **Where** | `/dashboard/storefront` |
| **Done when** | Profile and cover live; preview reviewed on mobile |

---

## 8. Menu

### 8.1 Create catalog structure

| | |
|---|---|
| **What** | Add menu sections (e.g., Weekly Mains, Bakes, Add-ons) |
| **Why** | Organized catalog improves browse and sets customer expectations |
| **Where** | `/dashboard/catalog` — [Catalog](../../pages/creator/catalog.md) |
| **Done when** | At least one section created |

### 8.2 Create and publish first menu item

| | |
|---|---|
| **What** | Complete all required fields: name, description, price, photo, ingredients, allergens, production location, fulfillment, lead time |
| **Why** | Incomplete allergen data blocks publish; listing transparency is trust-critical |
| **Where** | `/dashboard/catalog/items/:itemId/edit` — [Menu Item Editor](../../pages/creator/menu-item-editor.md) |
| **Done when** | Item status = published; visible on storefront preview |

### 8.3 Validate cottage food / category restrictions

| | |
|---|---|
| **What** | Confirm items comply with jurisdiction category limits (if cottage food) |
| **Why** | Platform blocks prohibited SKUs; violations risk suspension |
| **Where** | Menu Item Editor · [Compliance](../../pages/creator/compliance.md) |
| **Done when** | No category violation warnings; all items pass save validation |

### 8.4 Publish minimum viable catalog

| | |
|---|---|
| **What** | Publish 3–5 items (recommended) or at least 1 for soft launch |
| **Why** | Single-item storefronts convert poorly; breadth signals operational readiness |
| **Where** | `/dashboard/catalog` |
| **Done when** | Target item count live; each with photo, allergens, and pricing |

---

## 9. Storefront

### 9.1 Complete storefront profile

| | |
|---|---|
| **What** | Finalize bio, photos, fulfillment summary, social links (optional) |
| **Why** | Profile completeness score affects activation benchmarks and discovery |
| **Where** | `/dashboard/storefront` — [Storefront Settings](../../pages/creator/storefront-settings.md) |
| **Done when** | Dashboard profile checklist item marked complete |

### 9.2 Preview customer experience

| | |
|---|---|
| **What** | Open live storefront preview on mobile and desktop |
| **Why** | Catch formatting issues, missing badges, or broken images before public share |
| **Where** | Storefront Settings → Preview · public URL `/creators/:slug` |
| **Done when** | Storefront renders correctly; verification badges visible; catalog accessible |

---

## 10. Policies

### 10.1 Configure cancellation policy

| | |
|---|---|
| **What** | Set rules for customer-initiated cancellations within policy window |
| **Why** | Policies displayed pre-checkout; ambiguity drives disputes |
| **Where** | Storefront Settings · item-level overrides in Menu Item Editor where supported |
| **Done when** | Cancellation policy saved and visible on storefront/checkout preview |

### 10.2 Configure refund policy

| | |
|---|---|
| **What** | Define refund terms for quality issues, no-shows, and creator-initiated cancellations |
| **Why** | Creator-initiated cancel = full refund + reliability metric impact |
| **Where** | Storefront Settings · [Marketplace Mechanics — Cancellations](../../product/marketplace-mechanics.md#cancellations-and-refunds) |
| **Done when** | Refund policy published; you understand platform-mediated dispute path |

### 10.3 Set lead time and deposit terms (if applicable)

| | |
|---|---|
| **What** | Configure lead times per item; deposit rules for custom/catering items |
| **Why** | Lead time enforcement prevents overselling batch production |
| **Where** | Menu Item Editor · [Availability](../../pages/creator/availability.md) |
| **Done when** | Lead times match your production capacity; deposit terms disclosed pre-payment |

---

## 11. Availability

### 11.1 Set operating schedule

| | |
|---|---|
| **What** | Define weekly hours, operating days, and blackout dates |
| **Why** | Accurate availability prevents orders you cannot fulfill; feeds discovery signals |
| **Where** | `/dashboard/availability` — [Availability](../../pages/creator/availability.md) |
| **Done when** | Recurring schedule saved; closures blocked |

### 11.2 Configure order cut-offs

| | |
|---|---|
| **What** | Set cut-off times before each pickup window (e.g., order by Thursday 6 PM for Saturday pickup) |
| **Why** | Aligns customer expectations with batch production rhythm |
| **Where** | `/dashboard/availability` |
| **Done when** | Cut-offs saved; test checkout shows correct last-order time |

### 11.3 Set capacity limits

| | |
|---|---|
| **What** | Cap max orders per window/day; item-level max per day where needed |
| **Why** | Prevents overload; system enforces at checkout |
| **Where** | `/dashboard/availability` · Menu Item Editor |
| **Done when** | Capacity limits reflect realistic production volume |

---

## 12. Pickup

### 12.1 Configure pickup location

| | |
|---|---|
| **What** | Set pickup address or location description; handoff instructions |
| **Why** | Reduces missed pickups and customer confusion |
| **Where** | `/dashboard/storefront` · `/dashboard/availability` |
| **Done when** | Pickup location matches verified kitchen or approved pickup point; instructions clear |

### 12.2 Define pickup windows

| | |
|---|---|
| **What** | Create time windows customers select at checkout |
| **Why** | No valid window = checkout blocked; windows batch your production |
| **Where** | `/dashboard/availability` |
| **Done when** | At least one pickup window available in next 7 days on test checkout |

### 12.3 Prepare handoff process

| | |
|---|---|
| **What** | Define how you identify orders (name, order number, pickup code) |
| **Why** | Smooth handoff reduces wait time and wrong-order incidents |
| **Where** | Operational prep · [Order Detail](../../pages/creator/order-detail.md) |
| **Done when** | Written handoff procedure ready; labels or bags prepared |

---

## 13. Delivery

### 13.1 Enable delivery (if offered)

| | |
|---|---|
| **What** | Toggle delivery fulfillment; define service zone (radius or defined areas) |
| **Why** | Delivery expands reach but adds operational complexity — only enable if sustainable |
| **Where** | Menu Item Editor (fulfillment types) · `/dashboard/availability` · Storefront Settings |
| **Done when** | Delivery zone saved; delivery-specific lead times configured |

### 13.2 Set delivery minimums and pricing

| | |
|---|---|
| **What** | Configure minimum order value and/or delivery fee for zone |
| **Why** | Protects margin on low-ticket delivery runs |
| **Where** | Menu Item Editor · Storefront Settings |
| **Done when** | Minimums visible at checkout; pricing covers transport cost |

### 13.3 Confirm packaging for transit

| | |
|---|---|
| **What** | Insulated bags, leak-proof containers, tamper-evident seals |
| **Why** | Delivery quality issues drive refunds and negative reviews |
| **Where** | Operational prep — [Chef Welcome Package — Packaging](chef-welcome-package.md#packaging-guide) |
| **Done when** | Packaging supplies stocked for first delivery orders |

*Skip this section if pickup-only.*

---

## 14. Payments

### 14.1 Verify checkout flow

| | |
|---|---|
| **What** | Place test order through customer checkout; confirm total, fees, tax display |
| **Why** | Validates end-to-end payment before real customers |
| **Where** | Public storefront · customer checkout flow |
| **Done when** | Test order payment succeeds; order appears in [Orders](../../pages/creator/orders.md) |

### 14.2 Confirm payout path

| | |
|---|---|
| **What** | Verify Stripe connected; review payout schedule after test order completes |
| **Why** | Ensures first real earnings settle correctly |
| **Where** | `/creator/payouts` |
| **Done when** | Test order completed; net earnings visible in payout summary |

---

## 15. Preview

### 15.1 Customer journey walkthrough

| | |
|---|---|
| **What** | Walk full path: discovery → storefront → item detail → cart → checkout → confirmation |
| **Why** | Catches trust surface gaps (missing allergens, unclear pickup, wrong photos) |
| **Where** | Public storefront · [Customer Purchase Flow](../../pages/flows/customer-purchase-flow.md) |
| **Done when** | Journey completes without confusion; all trust badges and disclosures visible |

### 15.2 Creator fulfillment walkthrough

| | |
|---|---|
| **What** | Fulfill test order: Confirm → In production → Ready → Complete |
| **Why** | First real order should not be your first time using the production queue |
| **Where** | `/dashboard/orders/:orderId` — [Order Detail](../../pages/creator/order-detail.md) · [Order Fulfillment Flow](../../pages/flows/order-fulfillment-flow.md) |
| **Done when** | Test order status = completed; review prompt triggered on customer side |

### 15.3 Mobile verification

| | |
|---|---|
| **What** | Repeat preview on mobile device — most customers browse on phone |
| **Why** | Layout and photo crops differ on mobile |
| **Where** | Public storefront on mobile browser |
| **Done when** | Storefront, catalog, and checkout usable on mobile without horizontal scroll or broken images |

---

## 16. Publish

### 16.1 Complete compliance center

| | |
|---|---|
| **What** | Upload all jurisdiction-required documents; confirm all verification layers approved |
| **Why** | Verified Creator status required for paid orders |
| **Where** | `/creator/compliance` · `/dashboard/compliance` — [Compliance](../../pages/creator/compliance.md) |
| **Done when** | All checklist items green; "Verified Creator" badge active |

### 16.2 Publish catalog and go live

| | |
|---|---|
| **What** | Confirm all launch items published; storefront accepting orders |
| **Why** | Draft items are invisible to customers |
| **Where** | `/dashboard/catalog` · `/dashboard` activation checklist |
| **Done when** | Live items visible on public storefront; checkout enabled |

### 16.3 Share storefront link

| | |
|---|---|
| **What** | Copy link from dashboard; share via social, email, word of mouth |
| **Why** | Creator-attributed acquisition is highest-quality early traffic |
| **Where** | `/dashboard` — share action · `marketplate.com/creators/:slug` |
| **Done when** | Link shared to at least one channel; order notifications confirmed |

### 16.4 Monitor first orders closely

| | |
|---|---|
| **What** | Respond to first 5–10 orders with extra attention to timing, packaging, and communication |
| **Why** | Early reviews and reliability metrics compound into Trust Score |
| **Where** | `/dashboard/orders` · [Messages](../../pages/creator/messages.md) |
| **Done when** | First order fulfilled and completed; activation checklist marked done on dashboard |

---

## Quick Reference — Verification Gates

| State | Can publish | Can accept orders |
|-------|-------------|-------------------|
| Signed up | Draft only | No |
| Identity in review | Draft only | No |
| Kitchen in review | Draft only | No |
| Compliance pending | Draft only | No |
| Verified, no listings | Yes | Yes (nothing to buy) |
| Verified, published | Yes | Yes |
| Suspended | No | No |

→ Full state table: [Creator Onboarding Flow — Onboarding States](../../pages/flows/creator-onboarding-flow.md#onboarding-states-summary)

---

## Related Documents

- [Chef Welcome Package](chef-welcome-package.md)
- [Chef Success Guide](chef-success-guide.md)
- [Creator Onboarding Flow](../../pages/flows/creator-onboarding-flow.md)
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Mission](../../company/mission.md)
- [Value Propositions](../../product/value-props.md)
- [Marketplate Standards](../standards/marketplate-standards.md)
- [Chef Quality Standards](../standards/chef-quality-standards.md)
