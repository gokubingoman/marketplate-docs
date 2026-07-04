# Creator Agreement

> **DRAFT — FRAMEWORK ONLY.** Requires review and approval by qualified legal counsel before publication. Do not present to creators until counsel-approved.

**Status:** Draft — Framework  
**Version:** 1.0.0  
**Effective date:** `TODO(decision):` Set upon legal approval  
**Last updated:** 2026-07-03  
**Owner:** Legal

**Plain-language summary:** [Help — Platform Policies](../docs/help-center/platform-policies.md) · [Help — Verification](../docs/help-center/verification.md)

---

## 1. Agreement

This Creator Agreement ("**Agreement**") is between `TODO(decision):` Marketplate legal entity name ("**Marketplate**") and you, the food creator or business entity registering to sell on the Platform ("**Creator**," "**you**," or "**your**").

By registering as a creator, completing verification, or accepting paid orders, you agree to this Agreement, the [Terms of Service](terms-of-service.md), [Privacy Policy](privacy-policy.md), [Refund & Cancellation Policy](refund-and-cancellation-policy.md), and [Food Commerce Compliance](food-commerce-compliance.md).

If you represent a business entity, you represent that you have authority to bind that entity.

---

## 2. Marketplace Relationship

### 2.1 Independent merchant

You are an **independent seller** and the **merchant of record** for your transactions. You are not an employee, agent, joint venturer, or franchisee of Marketplate.

You control your menus, pricing, fulfillment, and customer relationships. Marketplate provides marketplace infrastructure, verification, discovery, payment facilitation, and dispute mediation.

[Marketplace Mechanics — Creator as merchant of record](../product/marketplace-mechanics.md#payment-model)

### 2.2 No exclusivity

This Agreement is non-exclusive. You may sell through other channels, subject to Platform policies (e.g., no off-platform payment solicitation for Platform orders).

### 2.3 Tax responsibility

You are solely responsible for determining, collecting, reporting, and remitting all applicable taxes (sales, use, VAT, income, etc.) unless Marketplate is legally required to collect and remit on your behalf in a jurisdiction.

`TODO(decision):` Tax collection obligations per launch market and payment processor capabilities.

---

## 3. Creator Eligibility

To sell on Marketplate you must:

- Be at least 18 years old (or age of majority)
- Operate a legitimate food business eligible under applicable law
- Complete all required verification layers before accepting paid orders
- Maintain current compliance documentation throughout your selling period
- Not be subject to prior permanent removal from the Platform

Onboarding: [Creator Onboarding Ops SOP](../operations/creator-onboarding-ops-sop.md) · [Help — Verification](../docs/help-center/verification.md)

---

## 4. Verification Requirements

Verification is mandatory. **Unverified creators cannot accept paid orders.**

### 4.1 Verification layers

| Layer | Requirement | Failure mode |
|-------|-------------|--------------|
| **Identity** | Government ID, business registration (if applicable), tax identity, contact verification | Draft mode only; no paid listings |
| **Kitchen** | Production location documented with address, photos, facility registration | Listings blocked until verified |
| **Compliance** | Jurisdiction-specific licenses, permits, food handler certs, cottage food registration | Category restrictions; suspension on expiry |
| **Insurance** | General/product liability where required by platform policy or law | Status shown; may block go-live when mandated |

Standards: [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md) · Operations: [Verification Review SOP](../operations/verification-review-sop.md)

### 4.2 Ongoing verification

You must:

- Update verification within stated deadlines when information changes (legal name, entity type, kitchen location)
- Renew compliance documents before expiration
- Respond to re-verification requests triggered by fraud signals or reports
- Link every SKU to a verified production location

Expired compliance enters a grace period (default: 14 days), then listings suspend automatically.

### 4.3 Verification limitations

Marketplate verifies **documentation and consistency** — not food quality or kitchen conditions at time of each order. Kitchen verification is **not** a health inspection substitute. Government authorities retain regulatory authority.

Legal framework: [Food Commerce Compliance](food-commerce-compliance.md)

### 4.4 AI-assisted review

Document review may use AI extraction and flagging. **Humans approve** all verification decisions. You may appeal rejections within 14 days.

[Verification Assist](../ai/verification-assist.md) · [AI Philosophy](../company/constitution.md#ai-philosophy)

---

## 5. Food Safety & Product Obligations

### 5.1 Legal compliance

You represent and warrant that you:

- Hold all licenses, permits, and registrations required for your products and jurisdiction
- Produce food only in verified, approved locations
- Sell only categories eligible under your compliance status (including cottage food restrictions)
- Comply with all applicable food safety, labeling, and consumer protection laws

[Food Commerce Compliance](food-commerce-compliance.md) · [Chef Quality Standards](../docs/standards/chef-quality-standards.md)

### 5.2 Labeling & allergens

You must:

- Accurately disclose ingredients and major allergens on every listing
- Update listings before selling if ingredients or preparation change
- Never claim allergen-free unless you can substantiate and applicable law permits
- Acknowledge that shared kitchens carry cross-contact risk

Confirmed allergen mislabeling triggers immediate suspension pending investigation.

[Help — Food Safety](../docs/help-center/food-safety.md) · [Food Safety Incident SOP](../operations/food-safety-incident-sop.md)

### 5.3 Prohibited products

You may not list products prohibited by Platform policy or applicable law, including (framework):

- Items ineligible under your cottage food or license category
- Unverified or misrepresented production location
- Products requiring permits you do not hold
- `TODO(decision):` Jurisdiction-specific prohibited category list`

### 5.4 Quality & fulfillment

You agree to:

- Honor stated lead times, capacity limits, and fulfillment windows
- Not oversell inventory — system enforces capacity at checkout
- Communicate material delays promptly
- Package food safely per fulfillment model
- Respond to customer messages within reasonable time

Standards: [Marketplace Mechanics — Fulfillment invariants](../product/marketplace-mechanics.md#fulfillment-invariants)

---

## 6. Storefront, Pricing & Policies

### 6.1 Storefront content

You are responsible for storefront accuracy — photos, descriptions, pricing, fulfillment options, and policies. Photography must represent actual products.

### 6.2 Pricing

You set item prices. Marketplate displays platform service fees separately at checkout.

### 6.3 Creator policies

You may set cancellation and refund policies **within Platform minimums**. Stricter creator policies must be disclosed pre-checkout. You may not offer terms less protective than Platform minimums for safety or compliance force-cancels.

Minimums: [Refund & Cancellation Policy](refund-and-cancellation-policy.md)

### 6.4 Reviews

Reviews from verified purchases cannot be suppressed for payment. You may respond publicly and professionally. Incentivized or fake reviews are prohibited.

---

## 7. Fees, Payments & Payouts

### 7.1 Platform fees

Marketplate charges a platform service fee per transaction.

`TODO(decision):` Commission structure, fee calculation, and display at checkout.

Fees are deducted before payout remittance unless otherwise stated.

[Help — Payments](../docs/help-center/payments.md)

### 7.2 Payment processing

Marketplate facilitates payment collection through a third-party payment processor. You authorize Marketplate to:

- Charge customers on your behalf
- Deduct fees, refunds, chargebacks, and adjustments
- Remit net payouts to your designated account

You must maintain valid payout account information.

Engineering: [Payment Service](../engineering/services/payment-service.md)

### 7.3 Payout schedule

Payouts follow a defined, predictable schedule visible in your creator dashboard.

`TODO(decision):` Payout timing (e.g., T+2 business days after order completion), rolling reserve, minimum payout threshold.

### 7.4 Refunds & adjustments

When refunds are issued per policy or dispute outcome:

- Customer receives refund to original payment method (5–10 business days)
- Your payout is adjusted accordingly
- Creator-fault refunds may affect reliability metrics and trigger review

Operations: [Refund Processing SOP](../operations/refund-processing-sop.md)

### 7.5 Payout holds

Marketplate may hold payouts during:

- Trust investigations or fraud review
- Dispute resolution
- Compliance or safety incidents
- Chargeback disputes

Held funds are released or applied per investigation outcome.

### 7.6 Chargebacks

You cooperate with chargeback evidence requests. Excessive chargebacks may trigger account review, payout holds, or suspension.

---

## 8. Customer Data & Privacy

When you receive customer personal information through orders, you are a **separate controller/processor** (per applicable law) limited to:

- Fulfilling the order and related communication
- Complying with law and Platform policies

You must **not**:

- Use customer data for unrelated marketing without consent
- Share customer data with third parties except as needed for fulfillment
- Retain data longer than necessary

Customer privacy rights requests related to your use of their data: cooperate with Marketplate and respond as required by law.

[Privacy Policy](privacy-policy.md)

---

## 9. Platform Tools & License

Marketplate grants you a limited, non-exclusive, revocable license to use creator tools, dashboards, and APIs during the term of this Agreement for Platform purposes.

You grant Marketplate license to display your storefront, listings, and content on the Platform and in marketing (with opt-out for specific campaigns where offered).

---

## 10. Enforcement & Termination

### 10.1 Enforcement ladder

Violations may result in progressive enforcement:

```
Education → Warning → Listing restriction → Order suspension → Account suspension → Permanent removal
```

Operations: [Moderation SOP](../operations/moderation-sop.md) · [Creator Suspension SOP](../operations/creator-suspension-sop.md)

### 10.2 Immediate suspension triggers

Without limiting other remedies, Marketplate may immediately suspend listings or accounts for:

- Confirmed allergen mislabeling or food safety incidents
- Fraudulent identity or documentation
- Operating without required verification or compliance
- Off-platform payment solicitation
- Harassment, discrimination, or illegal activity

### 10.3 Termination by creator

You may stop selling and request account closure. Active orders must be fulfilled or cancelled per policy. Verification documents retained per [Privacy Policy — Retention](privacy-policy.md#7-data-retention).

### 10.4 Termination by Marketplate

Marketplate may suspend or terminate your account for policy violations, legal requirements, or business reasons with notice where required.

### 10.5 Effect of termination

Upon termination:

- Paid listings deactivate
- Payouts for completed orders processed subject to holds, refunds, and chargebacks
- Sections on liability, indemnification, and dispute resolution survive

Offboarding: [Creator Suspension playbook](../docs/playbooks/creator-suspension-offboarding.md)

### 10.6 Appeals

Appeals available within 14 days for enforcement actions and verification rejections. Independent review where possible.

[Trust & Safety Standards — Appeals](../docs/standards/trust-and-safety-standards.md#appeals)

---

## 11. Representations & Warranties

You represent and warrant that:

- Information provided to Marketplate and customers is accurate and current
- You have rights to all content you upload
- Your products comply with applicable law
- You will not infringe third-party intellectual property
- You maintain required insurance when mandated

---

## 12. Indemnification

You agree to indemnify Marketplate against claims arising from your products, food safety incidents, regulatory violations, misrepresentations, content, and breach of this Agreement.

`TODO(decision):` Counsel to review scope and any Marketplate indemnification of creators for Platform defects.

---

## 13. Limitation of Liability

Marketplate's liability to you is limited as set forth in the [Terms of Service — Limitation of Liability](terms-of-service.md#11-limitation-of-liability).

Marketplate is not liable for lost profits, business interruption, or indirect damages arising from Platform use, subject to applicable law.

---

## 14. Modifications

Marketplate may modify this Agreement. Material changes notified before effective date. Continued selling after effective date constitutes acceptance where permitted. Fee changes may require additional notice per `TODO(decision):` counsel guidance.

---

## 15. General

| Topic | Framework |
|-------|-----------|
| **Governing law** | `TODO(decision):` Per launch market |
| **Dispute resolution** | `TODO(decision):` Arbitration vs. courts |
| **Entire agreement** | This Agreement + incorporated policies |
| **Contact** | `TODO(decision):` Creator support and legal contacts |

---

## Related Documents

- [Legal README](README.md)
- [Terms of Service](terms-of-service.md)
- [Privacy Policy](privacy-policy.md)
- [Food Commerce Compliance](food-commerce-compliance.md)
- [Refund & Cancellation Policy](refund-and-cancellation-policy.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
- [Creator Onboarding Ops SOP](../operations/creator-onboarding-ops-sop.md)
