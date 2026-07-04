# Password Reset

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Auth  
**Routes:** `/password-reset`, `/password-reset/confirm/:token`

---

## Purpose

The Password Reset flow restores account access for creators and customers who forgot their credentials. It operates in two steps: request a reset link via email, then set a new password via secure token.

This page exists to reduce support burden while preventing account enumeration and token abuse — security and clarity are equally important.

---

## Goals

**User goals:**
- Regain account access without contacting support
- Understand whether an email was sent without exposing whether the account exists
- Set a new password confidently and return to sign in

**Business goals:**
- Minimize locked-out user drop-off
- Enforce secure token expiry and single-use semantics
- Audit reset requests for fraud detection
- Maintain calm, precise communication during a stressful moment

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** All creator personas | Dashboard-dependent operators who forgot password |
| **Primary:** [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Buyers locked out before reorder |
| **Secondary:** [Platform Operations (Internal)](../../product/personas.md#platform-operations-internal) | Operators with standard password auth — admin may use separate IdP |

---

## Navigation

**Arrival paths:**
- [Login](login.md) → "Forgot password?"
- Account settings → "Change password" uses authenticated flow (different page in `customer/` or `creator/` — not this spec)
- Support article link

**Exit paths:**
- Request submitted → confirmation state (same page)
- Token confirmed → success message → [Login](login.md)
- Invalid/expired token → error with "Request a new link" → step 1
- "Back to sign in" → [Login](login.md)

---

## Layout

**Step 1 — Request reset** (same auth shell as login):

```
┌─────────────────────────────────────┐
│  Reset your password                │
│  Enter your email. We'll send a     │
│  link to reset your password.       │
│                                     │
│  Email                              │
│  [____________________________]     │
│                                     │
│  [      Send reset link       ]     │
│                                     │
│  Back to sign in                    │
└─────────────────────────────────────┘
```

**Step 2 — Set new password** (token landing):

```
┌─────────────────────────────────────┐
│  Choose a new password              │
│                                     │
│  New password                       │
│  [____________________________]     │
│  Confirm password                   │
│  [____________________________]     │
│                                     │
│  [      Update password       ]     │
└─────────────────────────────────────┘
```

**Step 3 — Confirmation** (inline or redirect to login with banner).

---

## Components

| Component | Usage |
|-----------|-------|
| **Text input** | Email; new password; confirm password |
| **Primary button** | "Send reset link" / "Update password" |
| **Ghost link** | "Back to sign in" |
| **Toast** | Success on password update (if redirecting to login) |

---

## Interactions

| Action | Behavior |
|--------|----------|
| Send reset link | Always show same confirmation UI regardless of email existence |
| Email link click | Opens step 2 with token validated server-side on page load |
| Update password | Validate match and strength; invalidate token on success; invalidate other sessions — `TODO(decision):` session invalidation scope |
| Resend link | Available from confirmation state; rate limited |
| Token expired | Show error + link to request new reset |

---

## Animations

| Element | Motion |
|---------|--------|
| Step transition | Crossfade 300ms between request → confirmation |
| Submit loading | Button spinner |
| Success | Optional checkmark 200ms; then redirect to login |

No celebratory motion — user is recovering from friction.

---

## Responsive Behaviour

Identical auth card layout to [Login](login.md) across breakpoints. Full-width primary button on mobile.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Send link | Button spinner; email field disabled |
| Token validation on load | Brief spinner while verifying token before showing password form |
| Update password | Button spinner |

If token invalid, skip password form — show error immediately after validation completes.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Invalid email format | "Enter a valid email address." | Fix field |
| Rate limited | "Too many reset requests. Try again in 15 minutes." | Wait |
| Token invalid/expired | "This reset link has expired. Request a new one." | Link to step 1 |
| Passwords don't match | "Passwords must match." | Fix confirm field |
| Weak password | Strength requirements message | Fix field |
| Network/server | Standard retry messaging | Retry |

**Security:** Request step always shows: "If an account exists for that email, we've sent a reset link." — never confirms account existence.

---

## Empty States

Not applicable.

Confirmation state after email send is intentional non-empty feedback — not an empty state.

---

## Permissions

| Role | Access |
|------|--------|
| Unauthenticated | Full reset flow |
| Authenticated | Should use in-account password change; `/password-reset` may redirect with notice |
| Invalid token | Step 2 blocked |

All account types (customer, creator, operator) share reset flow unless admin uses SSO-only — `TODO(decision):`.

---

## Analytics

| Event | Properties |
|-------|------------|
| `auth.password_reset.request_view` | — |
| `auth.password_reset.request_submit` | — |
| `auth.password_reset.request_success` | — (no email logged) |
| `auth.password_reset.confirm_view` | `token_valid` |
| `auth.password_reset.confirm_success` | — |
| `auth.password_reset.confirm_failure` | `error_code` |

Monitor: request volume spikes (potential abuse), completion rate token → new password.

---

## Accessibility

- Clear headings per step announced on route change
- Token error uses `role="alert"`
- Password fields with show/hide and requirements in `aria-describedby`
- Focus moves to first field on each step
- Confirmation message readable by screen readers without timed dismissal

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Reset password — Marketplate |
| `meta robots` | `noindex, nofollow` |

Token URLs must not be indexed.

---

## Future Improvements

- Passkey recovery as alternative to email token
- In-app reset from logged-in settings with re-auth challenge
- Admin-initiated reset for creator success team (logged in [Creator Admin Detail](../admin/creator-admin-detail.md) audit trail)
- Localization of email templates

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/auth/password-reset/request` | POST | Queue reset email |
| `/api/v1/auth/password-reset/validate-token` | GET | Validate token before showing form |
| `/api/v1/auth/password-reset/confirm` | POST | Set new password, consume token |

**Request (request):** `{ email }`  
**Request (confirm):** `{ token, new_password }`  
**Response:** Generic success; audit log with IP hash and timestamp.

Rate limits: per email, per IP. Tokens: single-use, 1-hour expiry (configurable in [Platform Settings](../admin/platform-settings.md)).

---

## Related Pages

- [Login](login.md)
- [Signup](signup.md)
- [Creator Signup](creator-signup.md)
- [Creator Admin Detail](../admin/creator-admin-detail.md) — operator-assisted recovery actions
