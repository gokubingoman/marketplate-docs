# Creator Signup

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Auth / Onboarding  
**Route:** `/creator/signup`

---

## Purpose

Creator Signup is the dedicated entry point for independent food entrepreneurs who want to sell on Marketplate. It creates a creator account, captures business intent, and routes new sellers into the verification onboarding pipeline — identity, kitchen, and compliance — before they can accept paid orders.

This page exists because creators are not customers who happen to list items. They require a distinct signup path, expectations setting, and immediate orientation toward [Identity Verification](identity-verification.md).

Per [Marketplace Mechanics](../../product/marketplace-mechanics.md#trust-model): **Verified to sell** — unverified creators cannot accept paid orders.

---

## Goals

**User goals:**
- Understand what Marketplate offers creators (marketplace + operating system)
- Create an account with clear next steps toward verification
- Select business type context to personalize onboarding (chef, baker, cottage food, etc.)
- Know timeline and requirements before investing time in document uploads

**Business goals:**
- Qualify supply-side signups without blocking legitimate cottage operators
- Set accurate expectations: human review required, no instant "verified" status
- Reduce incomplete verification submissions via upfront checklist
- Track creator acquisition funnel from signup through first verification submission

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** All creator personas — [Independent Chef](../../product/personas.md#independent-chef), [Baker](../../product/personas.md#baker), [Cottage Food Operator](../../product/personas.md#cottage-food-operator), [Meal Prep Business](../../product/personas.md#meal-prep-business), etc. | New sellers evaluating or committing to Marketplate |
| **Secondary:** Existing customer upgrading to creator account | Account type conversion — `TODO(decision):` unified vs. separate accounts |
| **Anti-persona:** Restaurant chains seeking delivery-aggregator model | Out of product scope per [Product Overview](../../product/overview.md#what-marketplate-is-not) |
| **Anti-persona:** Customers who only want to buy | Route to [Signup](signup.md) |

---

## Navigation

**Arrival paths:**
- Marketing "Start selling" / "Become a creator" CTAs
- [Login](login.md) → "Selling food? Creator signup"
- [Signup](signup.md) → creator pivot link
- Referral / partner links (commercial kitchens, local food orgs)

**Exit paths:**
- Account created → [Identity Verification](identity-verification.md) (step 1 of onboarding wizard)
- Already have account → [Login](login.md)
- "Just browsing?" → marketing creator page (optional)
- Abandon → save draft account; email nurture for incomplete verification — ops policy

**Onboarding sequence after signup:**
1. [Identity Verification](identity-verification.md)
2. [Kitchen Verification](kitchen-verification.md)
3. [Compliance Center](compliance-center.md)
4. Creator dashboard (catalog setup) — Phase 2 `creator/` specs

---

## Layout

Auth shell with expanded content — value prop + form + verification preview.

```
┌──────────────────────────────────────────────────────────────────┐
│  [Logo]                    Start selling on Marketplate          │
│                                                                  │
│  ┌────────────────────────────┐  ┌────────────────────────────┐  │
│  │  Create creator account    │  │  What happens next         │  │
│  │                            │  │  ① Identity verification   │  │
│  │  Business / display name   │  │  ② Kitchen verification    │  │
│  │  [____________________]    │  │  ③ Permits & compliance    │  │
│  │                            │  │                            │  │
│  │  Your name                 │  │  Our team reviews each     │  │
│  │  [____________________]    │  │  submission. Most complete   │  │
│  │                            │  │  within 2 business days.   │  │
│  │  Email                     │  │                            │  │
│  │  [____________________]    │  │  You can draft your menu     │  │
│  │                            │  │  while verification is       │  │
│  │  Password                  │  │  in progress. Paid orders    │  │
│  │  [____________________]    │  │  require full verification.  │  │
│  │                            │  └────────────────────────────┘  │
│  │  Business type             │                                  │
│  │  [Select: Chef, Baker… ▼]  │                                  │
│  │                            │                                  │
│  │  □ Terms, Seller Agreement │                                  │
│  │                            │                                  │
│  │  [   Create creator account ]                                │
│  │                            │                                  │
│  │  Sign in · Customer signup │                                  │
│  └────────────────────────────┘                                  │
└──────────────────────────────────────────────────────────────────┘
```

**Mobile:** Single column — "What happens next" accordion above form or below CTA.

---

## Components

| Component | Usage |
|-----------|-------|
| **Text input** | Business name, legal name, email, password |
| **Select / dropdown** | Business type (maps to persona-specific onboarding hints) |
| **Checkbox** | Terms of Service + Seller Agreement acceptance |
| **Primary button** | "Create creator account" |
| **Verification badge** (preview) | Static examples in sidebar — "Verified Creator" explainer tooltip |
| **Step indicator** (preview) | Onboarding steps 1–3 in sidebar — not interactive yet |
| **Cards** | "What happens next" checklist card |

---

## Interactions

| Action | Behavior |
|--------|----------|
| Business type select | Updates sidebar hints (e.g., cottage food → jurisdiction note) |
| Submit | Create account; auto-login; redirect to identity verification |
| Seller Agreement link | Opens legal doc in new tab |
| Tooltip on verification preview | Explains human review — "AI assists; our team approves" per [Values](../../company/values.md#7-humans-decide-ai-assists) |
| Duplicate email | Offer sign in or password reset |

---

## Animations

| Element | Motion |
|---------|--------|
| Business type change | Sidebar hint text crossfade 200ms |
| Submit success | Redirect to verification — no confetti |
| Accordion (mobile) | Expand/collapse 300ms ease-out |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Stacked; onboarding preview as collapsible section |
| **Tablet** | Single column centered, preview below form |
| **Desktop** | Two-column: form 55%, preview 45% |

Critical verification expectations visible without scrolling on desktop; one tap on mobile accordion.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Submit | Button spinner; form disabled |
| Post-create redirect | "Setting up your creator account…" brief overlay |
| Business type options | Static enum — no async load |

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Business name empty | "Enter the name customers will see." | Fix field |
| Terms not accepted | "Accept the Terms and Seller Agreement to continue." | Check boxes |
| Email taken | "This email is already registered. Sign in or reset your password." | Links |
| Weak password | Password policy message | Fix field |
| Region unsupported | "Marketplate isn't available in your area yet. Join the waitlist." — `TODO(decision):` launch geography | Waitlist |

Copy remains calm and actionable per [Clarity Creates Confidence](../../company/values.md#3-clarity-creates-confidence).

---

## Empty States

Not applicable on signup form.

Post-signup, creator lands on verification with **progress empty state** handled on [Identity Verification](identity-verification.md).

---

## Permissions

| Role | Access |
|------|--------|
| Unauthenticated | Full creator signup |
| Authenticated customer | Prompt to add creator profile or convert — `TODO(decision):` |
| Authenticated creator | Redirect to dashboard or verification resume |
| Verified creator | Redirect to dashboard |

New creator account status: `unverified` — draft catalog allowed, paid orders blocked.

---

## Analytics

| Event | Properties |
|-------|------------|
| `auth.creator_signup.page_view` | `referrer`, `campaign` |
| `auth.creator_signup.business_type_selected` | `business_type` |
| `auth.creator_signup.submit` | `business_type` |
| `auth.creator_signup.success` | `business_type` |
| `auth.creator_signup.failure` | `error_code` |
| `auth.creator_signup.customer_pivot_click` | — |

Funnel: signup → identity started → identity submitted → kitchen → compliance → verified.

---

## Accessibility

- Sidebar step preview uses ordered list semantics (`<ol>`) for screen readers
- Business type select fully keyboard operable
- Legal consent: checkbox + linked documents with discernible names
- Two-column layout reflows without loss of information
- Page title: "Create creator account — Marketplate"

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Start selling — Create creator account — Marketplate |
| `meta robots` | `index, follow` — acquisition page |
| Meta description | "Join Marketplate to sell food from your verified kitchen. Marketplace and operating system for independent food creators." |
| Structured data | `WebPage` with `potentialAction` RegisterAction — legal review before ship |

---

## Future Improvements

- Waitlist capture for out-of-market signups with geo detection
- Commercial kitchen tenant invitation flow (pre-linked kitchen verification)
- Video overview of verification requirements by business type
- Partner co-branded signup (shared kitchen facilities)
- SSO for kitchen admin inviting tenants

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/auth/signup` | POST | Create account with `account_type: "creator"` |
| `/api/v1/creators/onboarding` | GET | Return onboarding progress after signup |
| `/api/v1/meta/business-types` | GET | List business type enum with persona metadata |

**Request:** `{ business_name, legal_name, email, password, business_type, terms_accepted, seller_agreement_accepted }`  
**Response:** `{ creator_id, onboarding: { current_step: "identity", steps: [...] }, session }`

Creates audit trail entry: `creator.account.created`.

---

## Related Pages

- [Login](login.md)
- [Signup](signup.md) — customer account
- [Identity Verification](identity-verification.md) — onboarding step 1
- [Kitchen Verification](kitchen-verification.md) — onboarding step 2
- [Compliance Center](compliance-center.md) — onboarding step 3
- [Verification Queue](../admin/verification-queue.md) — admin review of submissions
- [Creator Admin Detail](../admin/creator-admin-detail.md) — internal creator view
