# Privacy Policy

> **DRAFT — FRAMEWORK ONLY.** Requires review and approval by qualified legal counsel before publication. Do not present to users until counsel-approved.

**Status:** Draft — Framework  
**Version:** 1.0.0  
**Effective date:** `TODO(decision):` Set upon legal approval  
**Last updated:** 2026-07-03  
**Owner:** Legal

**Plain-language summary:** [Help — Privacy](../docs/help-center/privacy.md)

---

## 1. Introduction

This Privacy Policy describes how `TODO(decision):` Marketplate legal entity name ("**Marketplate**," "**we**," "**us**," or "**our**") collects, uses, discloses, retains, and protects personal information when you use the Marketplate platform (the "**Platform**").

This Policy applies to customers, creators, visitors, and other users. Creator-specific obligations regarding customer data appear in the [Creator Agreement](creator-agreement.md).

By using the Platform, you acknowledge this Policy. Where required by law, we obtain consent for specific processing activities.

---

## 2. Roles & Scope

| Role | Relationship |
|------|--------------|
| **Marketplate** | Platform operator; data controller (or equivalent) for account, platform, and verification data |
| **Creator (seller)** | Independent merchant of record; receives customer order data necessary to fulfill transactions |
| **Payment processor** | Processes payments under its own privacy terms; Marketplate does not store full card numbers |
| **Service providers** | Process data on Marketplate's behalf under contract |

Creators must use customer data only for order fulfillment and related communication — not for unrelated marketing without consent. [Creator Agreement — Customer data](creator-agreement.md#8-customer-data--privacy)

---

## 3. Information We Collect

### 3.1 Information you provide

| Category | Examples | Primary purpose |
|----------|----------|-----------------|
| **Account** | Name, email, phone, password hash | Authentication, communication |
| **Profile** | Photo, preferences, dietary flags | Personalization, safety highlighting |
| **Orders** | Items, fulfillment details, notes, allergen acknowledgments | Transaction processing |
| **Payment** | Billing address, payment method token (via processor) | Payment processing |
| **Creator verification** | Government ID, business registration, tax ID, kitchen docs, compliance certificates, insurance | Trust verification — restricted access |
| **Communications** | Messages, support tickets, reviews | Service delivery, dispute resolution |
| **Creator business** | Storefront content, menus, photos, fulfillment settings | Marketplace operation |

### 3.2 Information collected automatically

| Category | Examples | Primary purpose |
|----------|----------|-----------------|
| **Device & usage** | IP address, browser type, pages viewed, search queries, referral source | Security, analytics, product improvement |
| **Location** | Approximate location from IP; precise location if you grant permission | Discovery, delivery, fraud prevention |
| **Cookies & similar tech** | Session, authentication, analytics cookies | Platform operation — see Section 10 |

Engineering context: [Identity Service](../engineering/services/identity-service.md) · [Trust Service](../engineering/services/trust-service.md)

### 3.3 Information from third parties

| Source | Data |
|--------|------|
| **Payment processor** | Transaction status, chargeback notifications |
| **Identity verification vendors** | Document verification signals (if used) |
| **Legal/regulatory requests** | As required by valid process |

---

## 4. How We Use Information

We use personal information to:

| Purpose | Legal basis (framework — `TODO(decision):` counsel to map per jurisdiction) |
|---------|-------------------------------------------------------------------------------|
| Operate the Platform and process orders | Contract performance |
| Verify creators and enforce trust standards | Legitimate interest / legal obligation |
| Facilitate payments and payouts | Contract performance |
| Provide customer support and resolve disputes | Contract / legitimate interest |
| Send transactional notifications | Contract performance |
| Improve products, security, and fraud detection | Legitimate interest |
| Comply with legal obligations | Legal obligation |
| Marketing (where permitted) | Consent or legitimate interest with opt-out |

We **do not sell** personal information. We do not use customer health information for advertising.

Trust operations: [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)

---

## 5. AI & Automated Processing Disclosure

Marketplate uses artificial intelligence and automated systems to assist platform operations. **AI recommends; humans approve** on high-stakes decisions.

### 5.1 AI systems in use (framework)

| System | Input | Output | Human gate |
|--------|-------|--------|------------|
| **Verification Assist** | Identity, kitchen, compliance documents | Field extraction, mismatch flags, fraud signals | Human operator approves/rejects verification |
| **Moderation Assist** | Listings, reviews, messages, storefront content | Policy violation scores, severity suggestions | Human moderator decides enforcement |
| **Discovery ranking** | Creator trust signals, relevance, location | Search/browse ordering | Documented, auditable algorithm |
| **Support assist** (internal) | Ticket content | Suggested responses | Human support agent sends |
| **Fraud detection** | Transaction patterns, document hashes | Risk signals | Human review for enforcement |

AI governance: [AI Philosophy](../company/constitution.md#ai-philosophy) · [Verification Assist](../ai/verification-assist.md) · [Moderation Assist](../ai/moderation-assist.md)

### 5.2 What AI does not do

AI systems on Marketplate **do not autonomously**:

- Approve or reject creator verification
- Suspend accounts or remove content
- Authorize refunds or select dispute outcomes
- Make legally binding decisions about users without human review

### 5.3 Automated decision-making rights

`TODO(decision):` Include jurisdiction-specific rights regarding automated decision-making (GDPR Art. 22, etc.) per launch market counsel guidance.

Users may contact us to request human review of decisions significantly affecting them where required by law.

---

## 6. How We Share Information

| Recipient | What | Why |
|-----------|------|-----|
| **Creators** | Customer name, contact, order details, notes, dietary/allergen info | Order fulfillment |
| **Customers** | Creator name, verification badges, appropriate location transparency | Informed purchase |
| **Payment processor** | Tokenized payment data, transaction amounts | Payment processing |
| **Service providers** | Data necessary for hosting, email, analytics, support tools | Platform operation — under DPA |
| **Legal authorities** | As required by law, subpoena, or to protect rights and safety | Legal compliance |
| **Business transfers** | In merger, acquisition, or asset sale — with notice where required | Corporate transaction |

Creator verification documents are **not** shared with customers beyond badge status and policy-appropriate location disclosure.

We require service providers to protect data consistent with this Policy.

---

## 7. Data Retention

We retain personal information only as long as necessary for the purposes described, unless a longer period is required by law.

| Data category | Retention framework |
|---------------|---------------------|
| **Account data** | Duration of account + grace period after deletion request |
| **Order & transaction records** | Minimum period for tax, accounting, and dispute resolution — typically 7 years `TODO(decision):` per jurisdiction |
| **Verification documents** | Active account + period after offboarding; case-linked for investigations |
| **Messages** | Active dispute period + defined retention; then delete or anonymize |
| **Reviews** | Associated with completed orders; may persist in anonymized form after account deletion |
| **Audit logs (trust, payment, moderation)** | Immutable; retained per [Trust & Safety Standards — Evidence preservation](../docs/standards/trust-and-safety-standards.md#evidence-preservation) |
| **Support tickets** | Defined schedule based on category and legal hold |
| **Analytics** | Aggregated/anonymized data may be retained indefinitely |

Deletion requests are subject to legal retention requirements (tax, ongoing disputes, trust investigations).

---

## 8. Your Rights & Choices

Depending on your jurisdiction, you may have rights to:

| Right | Description |
|-------|-------------|
| **Access** | Request a copy of personal information we hold |
| **Correction** | Update inaccurate information via account settings or request |
| **Deletion** | Request account deletion — subject to legal retention |
| **Portability** | Receive data in machine-readable format |
| **Opt-out of marketing** | Unsubscribe via account settings or email links |
| **Restrict processing** | Where applicable under local law |
| **Object** | To certain processing based on legitimate interest |
| **Withdraw consent** | Where processing is consent-based |

### 8.1 Exercising rights

- **Account settings:** Profile, preferences, data export, deletion — [Help — Privacy](../docs/help-center/privacy.md)
- **Privacy requests:** `TODO(decision):` Privacy request form URL or dedicated email
- **Response timeline:** `TODO(decision):` Per applicable law (e.g., 30 days GDPR, 45 days CCPA)

We may verify identity before fulfilling requests.

### 8.2 Jurisdiction-specific notices

`TODO(decision):` Add annexes as required:

- **California (CCPA/CPRA):** Do-not-sell/share, sensitive PI, authorized agent
- **EU/UK (GDPR):** DPO contact, legal bases table, cross-border transfers, SCCs
- **Other US states:** Colorado, Virginia, etc. — per expansion counsel
- **Canada (PIPEDA), Australia, etc.:** Per international expansion

---

## 9. Security

We implement administrative, technical, and organizational measures to protect personal information, including:

- Encryption in transit and at rest for sensitive categories
- Access controls and role-based permissions for verification documents
- MFA for administrative accounts
- Audit logging on trust and payment actions
- Vendor security assessments

No system is perfectly secure. Report suspected unauthorized access: [Help — Security](../docs/help-center/security.md)

Engineering: [Architecture Overview — Security](../engineering/architecture-overview.md)

---

## 10. Cookies & Tracking

| Cookie type | Purpose | Control |
|-------------|---------|---------|
| **Essential** | Authentication, cart, security | Required for Platform operation |
| **Analytics** | Usage measurement, product improvement | Consent banner where required |
| **Marketing** | Attribution (if used) | Opt-out where required |

`TODO(decision):` Publish separate Cookie Policy if counsel recommends; link from consent banner.

---

## 11. International Transfers

`TODO(decision):` Disclose data storage locations and cross-border transfer mechanisms (SCCs, adequacy decisions) per launch market and infrastructure choices.

---

## 12. Children's Privacy

The Platform is not directed to children under 13 (or 16 where applicable). We do not knowingly collect information from children. Contact us to request deletion if you believe a child has provided information.

---

## 13. Changes to This Policy

We may update this Policy. Material changes will be communicated via email or Platform notice before the effective date. The "Last updated" date reflects the current version.

---

## 14. Contact Us

| Purpose | Contact |
|---------|---------|
| **Privacy inquiries** | `TODO(decision):` privacy@marketplate.com |
| **Data rights requests** | `TODO(decision):` Privacy request form |
| **Data Protection Officer** | `TODO(decision):` If required by GDPR |
| **Postal address** | `TODO(decision):` Registered legal address |

---

## Related Documents

- [Legal README](README.md)
- [Terms of Service](terms-of-service.md)
- [Creator Agreement](creator-agreement.md)
- [Help — Privacy](../docs/help-center/privacy.md)
- [Help — Security](../docs/help-center/security.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
