# Login

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Auth  
**Route:** `/login`

---

## Purpose

The Login page is the primary entry point for returning creators, customers, and internal operators to access their Marketplate accounts. It establishes authenticated sessions securely while reinforcing that Marketplate is a trusted platform — not an anonymous marketplace.

This page exists to reduce friction for known users without compromising account security or obscuring the distinction between creator and customer account types.

---

## Goals

**User goals:**
- Sign in quickly with email and password or supported SSO
- Recover access if credentials are forgotten
- Understand which account type they are signing into

**Business goals:**
- Maximize successful authentication rate with minimal support tickets
- Route creators and customers to appropriate post-login destinations
- Capture login analytics for funnel and security monitoring
- Prevent credential stuffing and brute-force attacks

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Returning buyers accessing order history, favorites, and checkout |
| **Primary:** All creator personas (shared baseline) | Returning creators accessing dashboard, orders, and verification status |
| **Secondary:** [Platform Operations (Internal)](../../product/personas.md#platform-operations-internal) | Operators signing into admin console via separate auth path |
| **Anti-persona:** Unauthenticated users seeking to browse discovery — they should not be forced through login |

---

## Navigation

**Arrival paths:**
- Global nav "Sign in" link (customer and marketing surfaces)
- Creator marketing CTAs ("Sign in to your dashboard")
- Redirect from protected routes when session expired (`?redirect=/orders/123`)
- Email deep links that require re-authentication (password reset completion, verification reminders)
- `/admin` redirect for operators (may use separate SSO entry — `TODO(decision):` admin auth provider)

**Exit paths:**
- Successful login → intended redirect URL or role-default home:
  - Customer → `/` or `/orders`
  - Creator → `/creator/dashboard` (or verification onboarding if incomplete)
  - Operator → `/admin`
- "Create account" → [Signup](signup.md) or [Creator Signup](creator-signup.md)
- "Forgot password?" → [Password Reset](password-reset.md)
- "Continue as guest" → discovery (customer context only, if shown)

**Breadcrumbs:** None — auth shell is outside main IA tree.

---

## Layout

Centered auth card on neutral background. Minimal chrome — logo, form, supporting links only.

```
┌─────────────────────────────────────────────────────────────┐
│                      [Marketplate logo]                     │
│                                                             │
│              ┌─────────────────────────────┐                │
│              │  Sign in                    │                │
│              │                             │                │
│              │  Email                      │                │
│              │  [________________________] │                │
│              │                             │                │
│              │  Password                   │                │
│              │  [________________________] │                │
│              │                             │                │
│              │  [        Sign in        ]  │  ← primary     │
│              │                             │                │
│              │  Forgot password?           │                │
│              │  New here? Create account   │                │
│              └─────────────────────────────┘                │
│                                                             │
│         Trust strip: "Verified creators. Real kitchens."    │
└─────────────────────────────────────────────────────────────┘
```

**Content hierarchy:**
1. Logo (home link for marketing context)
2. Page title: "Sign in"
3. Email and password fields
4. Primary CTA: "Sign in"
5. Secondary links: password reset, signup
6. Optional trust reassurance line (subtle, not banner-heavy)

**Grid:** Single column, max-width 400px card, vertically centered on desktop; top-aligned with safe-area padding on mobile.

---

## Components

| Component | Usage |
|-----------|-------|
| **Text input** | Email, password (with show/hide toggle) |
| **Primary button** | "Sign in" — single primary action |
| **Ghost / text button** | "Forgot password?", "Create account" links |
| **Toast** | Post-login session warnings (e.g., "Signed in on a new device") |
| **Verification badge** (inline) | Not on login — reserved for post-auth surfaces |

Design tokens per [Design Principles](../../design-system/principles.md). One primary action per [component philosophy](../../design-system/components-overview.md).

---

## Interactions

| Action | Behavior |
|--------|----------|
| Submit form | Validate client-side; POST credentials; disable button + show loading state |
| Enter key | Submits form when focus in any field |
| Show/hide password | Toggles input type; icon button with `aria-pressed` |
| Invalid credentials | Inline error below form — no field-level blame without specificity |
| Account locked | Inline message with support contact and cooldown timer if applicable |
| Session expired banner | If arrived via redirect, show info banner: "Your session expired. Sign in to continue." |
| SSO (future) | Secondary button below divider — `TODO(decision):` SSO providers for creators |

**Keyboard:** Tab order — email → password → show/hide → sign in → forgot password → create account.

---

## Animations

| Element | Motion |
|---------|--------|
| Form submit | Primary button loading spinner (150ms fade-in) |
| Error appearance | Error message slides down 200ms ease-out; no shake animation |
| Page enter | Optional 200ms fade-in of auth card; respect `prefers-reduced-motion` |
| Success redirect | No celebration animation — immediate navigation |

Functional motion only per [Motion communicates state](../../design-system/principles.md#3-motion-communicates-state).

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile (320–767px)** | Full-width card with 16px horizontal padding; primary button full-width; logo scaled down |
| **Tablet (768–1023px)** | Centered card, 440px max-width |
| **Desktop (1024px+)** | Centered card; optional subtle background texture or photography — food/creator imagery, low opacity |

Content parity: email, password, and all links visible on all breakpoints.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Initial page load | Static form — no skeleton needed for two fields |
| Submit in progress | Primary button disabled with spinner; fields disabled |
| Redirect after success | Brief loading overlay or button spinner until navigation completes |
| SSO redirect (future) | Full-page loading with "Redirecting to sign in…" |

Never show skeleton that never resolves.

---

## Error States

| Error | Message (voice: precise, calm) | Recovery |
|-------|-------------------------------|----------|
| Invalid email format | "Enter a valid email address." | Fix field |
| Wrong credentials | "Email or password is incorrect." | Retry or [Password Reset](password-reset.md) |
| Account not verified (email) | "Confirm your email before signing in. Resend confirmation?" | Resend link action |
| Account suspended | "This account is suspended. Contact support for details." | Support link |
| Rate limited | "Too many attempts. Try again in 15 minutes." | Wait |
| Network failure | "We couldn't reach Marketplate. Check your connection and try again." | Retry button |
| Server error | "Something went wrong on our end. Try again in a moment." | Retry |

No blame language. Never reveal whether email exists in wrong-credentials case (security).

---

## Empty States

Not applicable — login is a fixed-form page with no data-dependent empty state.

**First-time adjacent:** "New here?" link routes to signup flows rather than an empty state on this page.

---

## Permissions

| Role | Access |
|------|--------|
| Unauthenticated | Full access to login form |
| Authenticated | Redirect away from `/login` to role-appropriate home |
| Suspended account | Login blocked with suspension message |
| Operator | Same form or dedicated `/admin/login` with elevated MFA — `TODO(decision):` |

Post-login routing respects verification state: unverified creators may land on [Identity Verification](identity-verification.md) rather than full dashboard.

---

## Analytics

| Event | Properties |
|-------|------------|
| `auth.login.page_view` | `referrer`, `redirect_url`, `surface` |
| `auth.login.submit` | — |
| `auth.login.success` | `user_type` (customer/creator/operator), `method` (password/sso) |
| `auth.login.failure` | `error_code` (no PII) |
| `auth.login.password_reset_click` | — |
| `auth.login.signup_click` | `destination` (customer/creator) |

Conversion: login success rate, time-to-success, failure reason distribution.

---

## Accessibility

- WCAG 2.2 AA minimum per [accessibility standards](../../design-system/accessibility-standards.md)
- `<form>` with explicit `<label>` for every input; no placeholder-only labels
- Password show/hide: `aria-label="Show password"` / `"Hide password"`
- Error summary: `role="alert"` on submit failure; associate errors with fields via `aria-describedby`
- Focus order logical; focus trapped only in modals (none on this page)
- Touch targets ≥ 44×44px for show/hide and links
- Color not sole error indicator — icon + text
- Screen reader page title: "Sign in — Marketplate"

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Sign in — Marketplate |
| `meta robots` | `noindex, nofollow` — auth pages not indexed |
| Canonical | `https://marketplate.com/login` |
| Structured data | None |

---

## Future Improvements

- Passkey / WebAuthn support for passwordless login
- SSO for commercial kitchen multi-tenant admins
- Device trust and "Remember this device" with risk-based MFA
- Magic link login for customers (lower friction, same security review)
- Inline creator vs. customer account type selector if unified signup converges

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/auth/login` | POST | Authenticate credentials; return session token / set cookie |
| `/api/v1/auth/session` | GET | Validate existing session; redirect if already logged in |
| `/api/v1/auth/logout` | POST | Clear session (linked from account menus, not this page) |
| `/api/v1/auth/resend-verification` | POST | Resend email confirmation from blocked-login state |

**Request (login):** `{ email, password }`  
**Response (success):** `{ user: { id, type, verification_status }, redirect_url }`  
**Response (failure):** `{ error_code, message }`

Rate limiting and audit logging required per [Marketplace Mechanics — Audit everything](../../product/marketplace-mechanics.md#marketplace-model-overview).

---

## Related Pages

- [Signup](signup.md) — new customer account
- [Creator Signup](creator-signup.md) — new creator account and onboarding entry
- [Password Reset](password-reset.md) — credential recovery
- [Identity Verification](identity-verification.md) — post-login creator verification flow
- [Admin Dashboard](../admin/admin-dashboard.md) — operator destination after admin login
