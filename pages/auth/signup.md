# Signup (Customer)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Auth  
**Route:** `/signup`

---

## Purpose

The Customer Signup page creates new buyer accounts for people who want to discover, purchase from, and track orders with verified local food creators. It is the demand-side authentication entry — distinct from creator onboarding, which requires verification before selling.

This page exists to establish identity for repeat purchase, order tracking, reviews, and favorites while keeping the flow minimal and trust-forward.

---

## Goals

**User goals:**
- Create an account in under 60 seconds
- Understand what a Marketplate customer account enables (orders, favorites, reviews)
- Confirm email and proceed to discovery or checkout

**Business goals:**
- Convert discovery visitors to registered customers without dark patterns
- Collect minimum PII required for commerce and support
- Route food entrepreneurs accidentally on customer signup to [Creator Signup](creator-signup.md)
- Maintain clear separation: customer accounts cannot sell without creator verification

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | First-time buyer creating account at checkout or from marketing |
| **Secondary:** Returning visitor who previously browsed as guest | Converting to save order history |
| **Anti-persona:** Independent food entrepreneurs intending to sell — redirect to [Creator Signup](creator-signup.md) |
| **Anti-persona:** Restaurant chain procurement managers — not v1 target |

---

## Navigation

**Arrival paths:**
- Global nav "Create account"
- Checkout gate: "Create account to complete order" with cart preserved
- Post-purchase prompt to save account details
- Marketing landing pages
- [Login](login.md) → "New here? Create account"

**Exit paths:**
- Success → email verification prompt OR immediate session if email verification deferred to first order — `TODO(decision):` email verification timing
- Post-verification → intended redirect (checkout, discovery, order confirmation)
- "Sign in" → [Login](login.md)
- "Want to sell on Marketplate?" → [Creator Signup](creator-signup.md)

---

## Layout

Centered auth card matching [Login](login.md) shell for visual consistency.

```
┌─────────────────────────────────────────────────────────────┐
│                      [Marketplate logo]                     │
│              ┌─────────────────────────────┐                │
│              │  Create your account        │                │
│              │  Buy from verified local    │                │
│              │  food creators.             │                │
│              │                             │                │
│              │  First name    Last name    │                │
│              │  [________]    [________]   │                │
│              │  Email                      │                │
│              │  [________________________] │                │
│              │  Password                   │                │
│              │  [________________________] │                │
│              │  □ I agree to Terms & Privacy│               │
│              │                             │                │
│              │  [     Create account     ] │                │
│              │                             │                │
│              │  Already have an account?   │                │
│              │  Sign in                    │                │
│              │                             │                │
│              │  Selling food? Creator      │                │
│              │  signup →                   │                │
│              └─────────────────────────────┘                │
└─────────────────────────────────────────────────────────────┘
```

**Hierarchy:** Value prop line → form fields → legal consent → primary CTA → secondary links.

---

## Components

| Component | Usage |
|-----------|-------|
| **Text input** | First name, last name, email, password |
| **Checkbox** | Terms of Service and Privacy Policy acceptance (required) |
| **Primary button** | "Create account" |
| **Ghost / text links** | Sign in, Creator signup |
| **Toast** | Success confirmation, resend verification |

Password strength indicator: optional inline helper text — not gamified meter per calm design principles.

---

## Interactions

| Action | Behavior |
|--------|----------|
| Submit | Validate all fields; POST signup; disable CTA during request |
| Terms links | Open Terms/Privacy in new tab; signup checkbox still required |
| Password field | Optional show/hide toggle; inline requirements on blur if unmet |
| Duplicate email | Error: "An account with this email already exists. Sign in instead." with link |
| Creator pivot link | Navigates to [Creator Signup](creator-signup.md); preserve email if entered — `TODO(decision):` |

---

## Animations

| Element | Motion |
|---------|--------|
| Submit loading | Button spinner, 150ms |
| Field validation errors | Inline appearance, 200ms ease-out |
| Success | Transition to verification confirmation view (crossfade 300ms) or redirect |

Respect `prefers-reduced-motion`.

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Stacked name fields (first / last on separate rows if <360px); full-width CTA |
| **Tablet/Desktop** | Name fields side-by-side; card max-width 440px centered |

All legal copy and creator pivot link visible on mobile — no hidden consent.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Submit | Disabled form + button spinner |
| Post-success | "Check your email" confirmation state with resend option |
| Resend verification | Button loading on resend action |

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Invalid email | "Enter a valid email address." | Fix field |
| Weak password | "Password must be at least 8 characters and include a number." | Fix field |
| Email taken | "An account with this email exists. Sign in or reset your password." | Links to login/reset |
| Terms not accepted | "Accept the Terms of Service to continue." | Check box |
| Network/server | Same patterns as [Login](login.md) | Retry |

Voice: [Precise and calm](../../brand/voice-and-tone.md#voice-attributes).

---

## Empty States

Not applicable — fixed registration form.

Post-signup "Check your email" is a **confirmation state**, not empty:

```
We've sent a confirmation link to you@example.com.
Didn't receive it? Resend email.
```

---

## Permissions

| Role | Access |
|------|--------|
| Unauthenticated | Full signup access |
| Authenticated customer | Redirect to account home |
| Authenticated creator | Redirect to creator dashboard |
| Guest checkout user | May upgrade guest order to account post-purchase — separate flow |

Customer signup does **not** grant creator privileges or verification status.

---

## Analytics

| Event | Properties |
|-------|------------|
| `auth.signup.page_view` | `referrer`, `has_cart`, `redirect_url` |
| `auth.signup.submit` | — |
| `auth.signup.success` | `verification_required` |
| `auth.signup.failure` | `error_code` |
| `auth.signup.creator_pivot_click` | — |
| `auth.signup.verification_resend` | — |

Funnel: page view → submit → success → email verified → first order.

---

## Accessibility

- All inputs labeled; consent checkbox has linked legal text readable by screen readers
- Error announcements via `role="alert"`
- Password requirements available in `aria-describedby` before submit
- Focus management on success state moves to confirmation heading
- Legal links meet contrast requirements

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Create account — Marketplate |
| `meta robots` | `noindex, nofollow` |
| Meta description | "Create a Marketplate account to order from verified local food creators." |

---

## Future Improvements

- Social sign-in (Apple, Google) for customers with same trust bar as password
- Progressive profiling — defer name collection to checkout if reduces friction without harming support
- Guest-to-account merge UX improvements
- Referral code field at signup

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/auth/signup` | POST | Create customer account |
| `/api/v1/auth/verify-email` | POST | Confirm email token |
| `/api/v1/auth/resend-verification` | POST | Resend confirmation email |

**Request:** `{ first_name, last_name, email, password, terms_accepted: true, account_type: "customer" }`  
**Response:** `{ user_id, session?, verification_email_sent }`

---

## Related Pages

- [Login](login.md)
- [Creator Signup](creator-signup.md)
- [Password Reset](password-reset.md)
- Customer checkout and order pages (Phase 2 `customer/` specs)
