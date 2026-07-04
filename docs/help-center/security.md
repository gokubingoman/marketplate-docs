# Security

> Help Center · Security  
> Route: `/help/security`  
> Last updated: 2026-07-03

## Overview

Your Marketplate account protects order history, payment methods, and personal information. Use a strong unique password, enable available security features, and report suspicious activity promptly. Marketplate never asks for your password via email or message.

This article covers sign-in security, password management, suspicious activity, and creator account protection.

---

## Step-by-step guidance

### Step 1: Secure your password

1. Use a unique password not reused on other sites — 12+ characters recommended.
2. Reset via [Password reset](../../pages/auth/password-reset.md) if forgotten or after suspected compromise.
3. Change password periodically and immediately if you receive unauthorized login alerts.

[Screenshot: Password reset page with email entry and security notice "We never ask for your password by email"]

### Step 2: Enable two-factor authentication (2FA)

1. Account settings → **Security** → **Two-factor authentication**.
2. Choose authenticator app or SMS (where available).
3. Save backup codes in a secure location — required if you lose device access.

[Screenshot: 2FA setup wizard with QR code for authenticator app and backup codes display]

### Step 3: Review active sessions

1. Security settings → **Active sessions**.
2. Review devices and locations signed into your account.
3. Select **Sign out** on unrecognized sessions; change password if suspicious.

[Screenshot: Active sessions list with device type, location approximation, last active time, and sign out buttons]

### Step 4: Recognize phishing and fraud

**Marketplate will never:**
- Ask for your password in email or chat
- Request payment outside the checkout flow
- Ask you to send verification documents to a personal email

**Report immediately:**
- Emails impersonating Marketplate with suspicious links
- Creators requesting off-platform payment — see [Messaging](messaging.md)
- Unauthorized orders on your account

[Screenshot: Example phishing email with red flags annotated — mismatched sender domain, urgency language, fake login link]

### Step 5: Secure creator accounts

Creators handle customer data and payouts — higher stakes:

1. Enable 2FA on Creator OS.
2. Limit dashboard access to trusted team members (team features by tier).
3. Do not share verification document uploads outside platform channels.
4. Review [Payouts](../../pages/creator/payouts.md) bank details changes — confirm via verified email.

[Screenshot: Creator security dashboard with 2FA enabled badge and payout change confirmation email notice]

---

## Common issues

| Issue | Likely cause | What to do |
|-------|--------------|------------|
| Locked out after failed logins | Brute-force protection | Wait 30 minutes; reset password |
| 2FA code not working | Clock drift on authenticator | Sync device time; use backup code |
| Unauthorized order | Compromised account or guest checkout typo | Contact support immediately — Account security |
| Password reset email missing | Spam or wrong email | Check spam; verify email on file |
| Creator payout destination changed | Account compromise | Contact support immediately; freeze payouts |

---

## FAQs

### Is my payment information secure?

Payment data is tokenized via PCI-compliant processors. Marketplate does not store full card numbers. See [Payments & fees](payments.md).

### What if I lost my 2FA device?

Use backup codes from setup. Without codes, identity verification with support required — may take 24–48 hours.

### Should creators use a business email?

Recommended. Separates personal and business account recovery. Use email you control for verification correspondence.

### How does Marketplate detect fraud?

Automated fraud signals plus human review on verification and high-risk transactions. Details internal — report concerns via support.

---

## Related articles

- [Account](account.md) — Profile and email management
- [Privacy](privacy.md) — Data collection and rights
- [Payments & fees](payments.md) — Secure checkout
- [Messaging](messaging.md) — Off-platform payment scams
- [Contact support](contact-support.md) — Security incident reporting
- [Login page spec](../../pages/auth/login.md)
- [Password reset page spec](../../pages/auth/password-reset.md)

---

## Escalation guidance

Contact support **immediately** for:

- Unauthorized account access or orders
- Suspected creator account compromise affecting payouts
- Phishing campaign impersonating Marketplate
- Password/email changed without your action

**Support category:** Account security  
**Expected response:** Within 4 hours  
**Include:** Account email, incident time, unauthorized activity description, screenshots of suspicious emails

Change password before contacting support if you still have access. Support may temporarily lock account during investigation.
