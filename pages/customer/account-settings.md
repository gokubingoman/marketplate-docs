# Account Settings

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/account/settings`  
**Surface:** Customer marketplace (web + mobile)  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

Account Settings is where customers manage their **profile, saved addresses, dietary preferences, and notification choices** — data that pre-fills [Checkout](checkout.md), improves [Search](search.md) and [Browse](browse.md) relevance, and controls how Marketplate communicates about orders.

This page exists so customers configure once and order confidently. Dietary preferences surface as filters and badges across discovery; addresses speed delivery checkout; notification toggles respect communication preferences without blocking critical order updates.

---

## Goals

### User goals

- Update name, email, and phone used for orders
- Manage saved delivery addresses with a default
- Set dietary preferences and allergen filters for discovery
- Control email, push, and SMS notification categories
- Sign out or delete account (with confirmation)
- Access [Order History](order-history.md) from account context

### Business goals

- Reduce checkout friction via saved profile and address data
- Improve discovery relevance through dietary preference signals
- Maintain compliant communication opt-in/opt-out records
- Reduce address-related delivery failures and support tickets
- Measure profile completeness and preference adoption

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Managing account between orders |
| **Secondary** | First-time buyer post-signup | May arrive from checkout "Add address" link |
| **Anti-persona** | Creator managing business profile | Creator settings live in [Storefront Settings](../creator/storefront-settings.md) |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| Top nav account menu | "Account settings" |
| Tab bar "Account" (mobile) | Direct to settings |
| [Checkout](checkout.md) | "Add address" / "Manage addresses" link |
| [Search](search.md) | Location prompt → account settings |
| [Home](home.md) | "Set location in account" near-you module |
| Direct URL | Bookmark or email link |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Order History](order-history.md) | Account menu or settings nav link |
| [Help](help.md) | "Privacy & data" / support links |
| [Home](home.md) | Logo tap, cancel unsaved changes |
| [Checkout](checkout.md) | Return after address add (if `?redirect=` present) |
| [Login](../auth/login.md) | Sign out |
| External | Password change via auth provider flow |

### Global chrome

- **Top nav bar:** Logo, search, cart, account menu (active)
- **Tab bar (mobile):** Account tab active
- Settings sub-nav (desktop): Profile · Addresses · Dietary · Notifications

---

## Layout

### Content hierarchy (top to bottom)

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — logo, search, cart, account (active)         │
├─────────────────────────────────────────────────────────────┤
│  Page header — "Account settings" (h1)                      │
├──────────────────┬──────────────────────────────────────────┤
│  Settings nav    │  Profile section (default)               │
│  · Profile       │  ┌────────────────────────────────────┐  │
│  · Addresses     │  │  First name *    [___________]     │  │
│  · Dietary       │  │  Last name *     [___________]     │  │
│  · Notifications │  │  Email *         [___________]     │  │
│  · Order history │  │  Phone *         [___________]     │  │
│  · Sign out      │  │  (for order SMS updates)           │  │
│                  │  │  [ Save changes ]                  │  │
│                  │  └────────────────────────────────────┘  │
│                  │  Addresses section                       │
│                  │  ┌─ Address card ──────────────────────┐ │
│                  │  │  Home · Default                     │ │
│                  │  │  123 Main St, Brooklyn NY 11201     │ │
│                  │  │  [ Edit ] [ Remove ]                │ │
│                  │  └─────────────────────────────────────┘ │
│                  │  [ + Add address ]                       │
│                  │  Dietary preferences                     │
│                  │  [ Vegan ] [ GF ] [ Nut-free ] ...       │
│                  │  Allergen alerts (multi-select)          │
│                  │  Notifications                           │
│                  │  Order updates — Email ✓ Push ✓ SMS ✓    │
│                  │  Marketing — Email ☐                     │
│                  │  [ Save preferences ]                    │
└──────────────────┴──────────────────────────────────────────┘
```

### Grid

| Breakpoint | Layout |
|------------|--------|
| Mobile (320–767px) | Single column; section accordion or vertical scroll; sticky save on section edit |
| Tablet (768–1023px) | Single column; horizontal section tabs |
| Desktop (1024px+) | Left settings nav (~240px) + content area; max-width 960px centered |

---

## Components

| Component | Usage on this page |
|-----------|-------------------|
| **Top nav bar** | Global navigation; account menu active |
| **Tab bar (mobile)** | Account tab active |
| **Text input** | Name, email, phone |
| **Address input** | Add/edit address with autocomplete |
| **Address card** | Saved address row with default badge |
| **Chip / toggle group** | Dietary preference multi-select |
| **Checkbox** | Notification category toggles |
| **Select** | Default address picker when multiple |
| **Primary button** | Save changes per section |
| **Secondary button** | Add address |
| **Ghost button** | Edit/remove address; section nav links |
| **Destructive button** | Remove address; delete account |
| **Confirmation modal** | Remove address; delete account; unsaved changes |
| **Toast** (Success) | Settings saved |
| **Toast** (Error) | Save failure |
| **Warning banner** | Email verification pending |

---

## Interactions

### Profile section

- Pre-fill from `/api/v1/customers/me`
- Email change may require verification flow — show **Warning banner** until confirmed
- Phone required for SMS order notifications; validated E.164 format
- **Primary button** "Save changes" → PATCH profile; **Success toast**
- Password managed via external auth — **Ghost button** "Change password" opens auth flow

### Addresses section

- List saved addresses; one **Default** badge per customer
- **Secondary button** "+ Add address" → inline form or modal with **Address input** autocomplete
- **Ghost button** "Edit" → same form pre-filled
- **Ghost button** "Remove" → **Confirmation modal** if default or only address
- Set default → radio or "Make default" action; updates checkout pre-fill
- Max 10 addresses in v1
- Zone hint on save: "Delivery available" or "Outside delivery zones — pickup only" (informational)

### Dietary preferences section

- Multi-select chips: Vegan, Vegetarian, Gluten-free, Dairy-free, Nut-free, Halal, Kosher, etc. per platform taxonomy
- Allergen alerts: separate multi-select for peanuts, tree nuts, shellfish, etc.
- Preferences sync to discovery filters on [Search](search.md) and [Browse](browse.md)
- **Dietary badge** highlighting on [Menu Item Detail](menu-item-detail.md) and [Cart](cart.md) when preferences match
- Does not replace per-order allergen acknowledgment at [Checkout](checkout.md)

### Notifications section

- Toggles by category:

| Category | Channels | Default | Notes |
|----------|----------|---------|-------|
| Order status updates | Email, Push, SMS | All on | Critical — SMS requires verified phone |
| Pickup reminders | Push, SMS | On | 1h before window |
| Review prompts | Email, Push | On | Post-completion |
| Marketing & discovery | Email | Off | Explicit opt-in |

- Order-critical notifications cannot be fully disabled — inline helper explains minimum channel requirement
- **Primary button** "Save preferences" → PATCH; audit log for compliance

### Account actions

- **Ghost button** "Order history" → [Order History](order-history.md)
- **Ghost button** "Sign out" → session clear → [Home](home.md)
- **Destructive button** "Delete account" → **Confirmation modal** with policy summary → soft delete request

### Unsaved changes

- Dirty state tracking per section
- Navigate away → **Confirmation modal** if unsaved
- Mobile: sticky save bar when section dirty

### Keyboard

- Tab order: nav → section fields → save → next section
- Enter in form submits current section save
- Escape closes address modal

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Section switch | Content crossfade 150ms |
| Address add | Card slide-down 200ms |
| Address remove | Collapse height 200ms |
| Save success | Brief checkmark on button 200ms |
| Chip toggle | Scale 100ms |

Respect `prefers-reduced-motion`: instant section swap.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Vertical sections; settings nav as horizontal scroll tabs or accordion |
| **Tablet** | Section tabs below header |
| **Desktop** | Persistent left nav; content scrolls independently |

**Content parity:** All sections reachable on mobile without desktop-only nav.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Initial page | Skeleton for profile fields + 2 address card skeletons |
| Section switch | Inline skeleton if lazy-loaded |
| Address autocomplete | Spinner in input trailing icon |
| Save | Button loading state |
| Delete account | Modal button loading |

Never show empty form during load — shimmer placeholders only.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Profile load failure | "Account settings couldn't load." | **Primary button** "Try again" |
| Save failure | **Error toast**: "Changes couldn't save. Try again." | Retry |
| Invalid phone | Inline field error | Fix format |
| Address validation fail | Inline: "Enter a valid address" | Correct input |
| Email in use | Inline: "This email is already registered" | Use different email |
| Auth expired | Redirect to [Login](../auth/login.md) | Re-authenticate |
| Delete account blocked | Modal: "Complete or cancel active orders first." | Link to [Order History](order-history.md) |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| No saved addresses | "Add an address for faster checkout." | **Primary button** "+ Add address" |
| No dietary prefs selected | "Select preferences to personalize discovery." | Chip group ready — no blocker |
| New account | Profile pre-filled from signup where available | Complete phone field |

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| View settings | ✗ | ✓ |
| Edit profile | ✗ | ✓ |
| Manage addresses | ✗ | ✓ |
| Set dietary prefs | ✗ | ✓ |
| Manage notifications | ✗ | ✓ |
| Delete account | ✗ | ✓ (no active orders) |

Unauthenticated access redirects to login with return URL.

---

## Analytics

### Page events

| Event | Properties |
|-------|------------|
| `page_view` | `page: account_settings`, `section` (default profile) |
| `account_settings_section_viewed` | `section: profile\|addresses\|dietary\|notifications` |
| `account_settings_profile_saved` | `fields_changed[]` |
| `account_settings_address_added` | — |
| `account_settings_address_removed` | `was_default` |
| `account_settings_dietary_updated` | `preferences[]`, `allergen_alerts[]` |
| `account_settings_notifications_saved` | `categories_changed[]` |
| `account_settings_sign_out` | — |
| `account_settings_delete_started` | — |

### Funnel metrics

- Profile completeness rate (phone + default address)
- Dietary preference adoption
- Address book size vs. delivery order rate
- Marketing opt-in rate

→ [Customer Metrics](../../product/success-metrics-overview.md#customer-metrics)

---

## Accessibility

- **Landmark regions:** `banner` (nav), `navigation` (settings sub-nav), `main` (settings content)
- **Skip link:** "Skip to settings content"
- **Page title (document):** `Account settings — Marketplate`
- **Form sections:** `<fieldset>` + `<legend>` for Profile, Addresses, Dietary, Notifications
- **Required fields:** `aria-required="true"`; error summary on save failure with focus first error
- **Address cards:** `article` with `aria-label="Address: [label], [street]"`; default announced
- **Notification toggles:** Each toggle labeled with category and channel
- **Delete account:** Destructive action with `aria-describedby` linking to consequences
- **Unsaved changes modal:** Focus trap per [modals spec](../../design-system/components/modals.md)

→ [Accessibility Standards](../../design-system/accessibility-standards.md)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Account Settings \| Marketplate |
| `<meta name="description">` | Manage your Marketplate profile, addresses, and preferences. |
| Canonical | `https://marketplate.com/account/settings` |
| `robots` | `noindex, nofollow` — authenticated content |

Account settings is not indexable.

---

## Future Improvements

- Payment methods management (saved cards)
- Creator follow list and favorites
- Family/household profiles with shared addresses
- Export personal data (GDPR/CCPA)
- Two-factor authentication
- Language preference
- Gift credit balance display

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/customers/me` | GET | Full profile, preferences, notification settings |
| `/api/v1/customers/me` | PATCH | Update profile fields |
| `/api/v1/customers/me/addresses` | GET | List saved addresses |
| `/api/v1/customers/me/addresses` | POST | Add address |
| `/api/v1/customers/me/addresses/:id` | PATCH | Update address |
| `/api/v1/customers/me/addresses/:id` | DELETE | Remove address |
| `/api/v1/customers/me/addresses/:id/default` | POST | Set default |
| `/api/v1/customers/me/preferences/dietary` | PATCH | Dietary chips + allergen alerts |
| `/api/v1/customers/me/preferences/notifications` | PATCH | Notification toggles by category/channel |
| `/api/v1/customers/me/delete` | POST | Account deletion request |

Address autocomplete via platform geocoding service — debounced 300ms.

---

## Related Pages

- [Order History](order-history.md) — Linked from account menu
- [Checkout](checkout.md) — Consumes saved addresses and contact defaults
- [Search](search.md) — Location and dietary filter source
- [Browse](browse.md) — Dietary collection personalization
- [Home](home.md) — Near-you uses saved location
- [Cart](cart.md) — Dietary badge highlighting
- [Help](help.md) — Privacy, data, and account support
- [Login](../auth/login.md) — Sign out destination inverse
