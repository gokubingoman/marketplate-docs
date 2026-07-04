# Troubleshooting

> Help Center · Troubleshooting  
> Route: `/help/troubleshooting`  
> Last updated: 2026-07-03

## Overview

Most Marketplate issues resolve with a few targeted checks — refresh, update, verify settings, or retry checkout. This article collects common technical problems for customers and creators with step-by-step fixes before contacting support.

For policy or order disputes, see topic-specific articles. For unresolved technical issues, see [Contact support](contact-support.md).

---

## Step-by-step guidance

### Step 1: General fixes (try first)

1. **Refresh** the page or force-quit and reopen the mobile app.
2. **Update** to the latest app version or use a current browser (Chrome, Safari, Firefox, Edge — last two major versions).
3. **Sign out and sign in** to refresh your session.
4. **Check connection** — switch Wi‑Fi/mobile data if pages load partially.
5. **Clear cache** only if other steps fail — you may need to sign in again.

[Screenshot: Mobile app Settings → About showing app version number and "Check for updates" link]

### Step 2: Checkout and payment issues

| Symptom | Fix |
|---------|-----|
| Checkout button disabled | Select valid pickup window or delivery address in zone |
| Payment declined | Verify card details; try different card; contact bank |
| Cart empty after login | Items are per-creator — return to storefront and re-add |
| Total looks wrong | Review fee breakdown — see [Payments & fees](payments.md) |
| Stuck on "Processing" | Wait 60 seconds; check Order history before retrying |

[Screenshot: Checkout error state with "Payment couldn't be processed" message and Retry button]

Detailed payment help: [Payments & fees](payments.md). Duplicate charge: contact support with order number.

### Step 3: Order and notification issues

| Symptom | Fix |
|---------|-----|
| Status not updating | Pull to refresh Order Detail; check [Notifications](notifications.md) settings |
| No Ready notification | Verify push/email enabled; check spam folder |
| Cannot cancel | Window may have closed — see [Refunds](refunds.md) |
| Message not sending | Confirm active order thread; refresh app |

[Screenshot: Order detail pull-to-refresh gesture with loading indicator on status timeline]

Order help: [Orders](orders.md). Pickup: [Pickup](pickup.md). Delivery: [Delivery](delivery.md).

### Step 4: Account and sign-in issues

| Symptom | Fix |
|---------|-----|
| Forgot password | [Password reset](../../pages/auth/password-reset.md) |
| Email not verified | Resend from login page; check spam |
| 2FA code fails | Sync device clock; use backup code — [Security](security.md) |
| Account locked | Wait 30 minutes after failed attempts |

[Screenshot: Login page with "Forgot password" and "Resend verification email" links]

### Step 5: Creator dashboard issues

| Symptom | Fix |
|---------|-----|
| Cannot publish item | Complete [Verification](verification.md); link verified kitchen |
| Orders not appearing | Refresh dashboard; check notification settings |
| Payout missing | Compare [Analytics](analytics.md) date range to payout schedule — [Payouts](../../pages/creator/payouts.md) |
| Photo upload fails | File under 10 MB; JPG/PNG; stable connection |
| Analytics empty | 24-hour delay normal for new data |

[Screenshot: Creator dashboard error banner with "Try again" and support link]

Creator help: [Storefronts](storefronts.md), [Menus](menus.md), [Analytics](analytics.md).

### Step 6: Search and discovery issues

| Symptom | Fix |
|---------|-----|
| No search results | Widen radius; remove filters; try Browse |
| Creator not appearing | New listings index within 24 hours; verification required |
| Wrong location results | Update search area or enable location permission |

[Screenshot: Search empty state with "Clear filters" and "Browse all creators" buttons]

---

## Browser and device support

| Platform | Supported |
|----------|-----------|
| iOS app | Current and previous major version |
| Android app | Current and previous major version |
| Desktop web | Chrome, Safari, Firefox, Edge (latest 2 versions) |
| Mobile web | Safari iOS, Chrome Android |

JavaScript required. Private/incognito mode supported but may limit saved login.

---

## Common issues

| Issue | Likely cause | What to do |
|-------|--------------|------------|
| Blank white screen | Cache corruption; outdated browser | Update browser; clear cache; try incognito |
| Images not loading | Slow connection; content blocker | Disable blockers for marketplate.com; retry |
| Help page unavailable | Temporary outage | Retry in 5 minutes; contact support if 30+ minutes |
| "Something went wrong" generic | Server error | Retry; note time for support |
| Rate limited on support form | Multiple rapid submissions | Wait 1 hour — see [Contact support](contact-support.md) |

---

## FAQs

### Why did my cart expire?

Carts may release held inventory after inactivity — especially same-day limited items. Re-add items and complete checkout promptly.

### The app crashes on launch

Update app; reinstall if needed (order history preserved when signed in). Report persistent crashes to support with device model and OS version.

### Help search returns no results

Try different keywords or browse categories on [Help](../../pages/customer/help.md). Clear search filter with × button.

### Is Marketplate down?

Check status page when available, or contact support if widespread issues suspected. Individual connection issues usually local.

---

## Related articles

- [Contact support](contact-support.md) — When self-service fails
- [Payments & fees](payments.md) — Payment errors
- [Orders](orders.md) — Order status issues
- [Account](account.md) — Profile problems
- [Security](security.md) — Sign-in and 2FA
- [Accessibility](accessibility.md) — Assistive technology issues
- [Help page spec](../../pages/customer/help.md)

---

## Escalation guidance

Contact support when troubleshooting steps fail:

- Payment charged without order confirmation after 15 minutes
- Persistent errors 24+ hours across devices
- Data loss (missing orders, reviews) after confirmed completion
- Creator dashboard blocking revenue-critical actions after verification complete

**Support category:** Match issue type — Order issue, Payment & refund, Account, General inquiry  
**Expected response:** Within 24 hours  
**Include:** Device, OS, app version or browser, steps already tried, screenshots, time of error, order/account email

Technical reports help engineering — specific error messages and timestamps accelerate resolution.
