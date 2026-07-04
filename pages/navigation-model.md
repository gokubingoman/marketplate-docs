# Navigation Model

> Global, contextual, and mobile navigation patterns across Customer Marketplace, Creator OS, and Admin surfaces.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** UX & Information Architecture

---

## Purpose

This document defines **how users move through Marketplate** — not what each page contains (see [Information Architecture](information-architecture.md) and individual page specs). Navigation must reinforce the trust thesis: users always know where they are, who they are acting as, and how to reach safety-critical information.

Design implementation follows [Design System Principles](../design-system/principles.md): calm interfaces, one primary action per screen, and content parity across breakpoints.

---

## Navigation Principles

| Principle | Implementation |
|-----------|----------------|
| **Context before chrome** | Navigation adapts to surface (customer, creator, admin) — never one nav for all |
| **Trust is always reachable** | Verification status, compliance state, and order status are never more than two taps/clicks away in their respective contexts |
| **One primary action** | Global nav provides wayfinding; page-level CTAs provide commitment |
| **Predictable back behavior** | Back always returns to the logical parent — not arbitrary history |
| **Role clarity** | Users always see which hat they are wearing (customer vs. creator vs. admin) |
| **Mobile-first customer, desktop-capable creator** | Customer ordering optimized for thumb reach; creator ops scales to multi-column desktop |

→ Voice for nav labels: [Voice and Tone — Product & UI Copy](../brand/voice-and-tone.md#product--ui-copy)

---

## Application Shells

Marketplate renders three distinct application shells. Shell selection is determined at route level — see [Information Architecture — Path Prefixes](information-architecture.md#path-prefixes-by-surface).

```mermaid
flowchart LR
    Route[Route match] --> Shell{Shell type}
    Shell -->|"/", "/search", "/cart", ...| CS[Customer Shell]
    Shell -->|"/dashboard/*"| CrS[Creator Shell]
    Shell -->|"/admin/*"| AS[Admin Shell]
    Shell -->|"/login", "/creator/*"| MS[Minimal Auth Shell]
```

| Shell | Header | Primary nav | Footer | Role indicator |
|-------|--------|-------------|--------|----------------|
| **Customer** | Logo, search, cart, account | Bottom (mobile) / top (desktop) | Help, legal links | Account menu only |
| **Creator** | Logo, verification badge, role switch | Side (desktop) / bottom (mobile) | — | "Creator dashboard" + status pill |
| **Admin** | Logo, environment badge | Side rail (all breakpoints) | — | Admin role + team name |
| **Minimal Auth** | Logo only | None | Help link | None until authenticated |

---

## Global Navigation — Customer Marketplace

### Desktop (≥1024px)

```
┌──────────────────────────────────────────────────────────────────────┐
│ [Logo]    [Search input — expandable]              [Cart] [Account ▾] │
├──────────────────────────────────────────────────────────────────────┤
│ Home · Browse · Orders (auth) · Help                                  │
└──────────────────────────────────────────────────────────────────────┘
```

| Item | Path | Visibility | Notes |
|------|------|------------|-------|
| Logo | `/` | Always | Returns to home; does not clear cart |
| Search | `/search` | Always | Expands inline; submits to search results |
| Cart | `/cart` | Always | Badge shows item count; zero state hidden |
| Account menu | `/account/settings` | Authenticated | Includes order history, settings, logout |
| Sign in | `/login` | Anonymous | Replaces account menu |
| Home | `/` | Always | Secondary text nav |
| Browse | `/browse` | Always | |
| Orders | `/orders` | Authenticated | Hidden when logged out |
| Help | `/help` | Always | Opens help center |

### Mobile (320–767px) — Bottom Navigation

Fixed bottom tab bar with five slots:

| Tab | Icon + label | Path | Always visible |
|-----|--------------|------|----------------|
| **Home** | Home | `/` | ✓ |
| **Browse** | Browse | `/browse` | ✓ |
| **Search** | Search | `/search` | ✓ |
| **Orders** | Orders | `/orders` | Auth only; hidden when logged out |
| **Account** | Account | `/account/settings` or `/login` | ✓ |

**Cart access on mobile:** Floating cart button (bottom-right, above tab bar) when cart is non-empty. Persistent header cart icon when cart is empty. Cart is intentionally **not** a tab — it is a commerce action, not a destination for browsing.

**Checkout and confirmation:** Bottom nav **hidden** during checkout to prevent accidental navigation away from payment. Replaced by minimal header with back-to-cart only.

### Tablet (768–1023px)

Hybrid: top header matches desktop; bottom nav optional based on viewport height. Prefer top secondary nav when vertical space allows.

---

## Global Navigation — Creator OS

Creator navigation prioritizes **operational frequency** and **trust-critical status visibility**.

### Verification status — always visible

The creator shell header includes a **Verification Status Pill** — never collapsed, never behind a menu:

| Status | Pill appearance | Tap/click action |
|--------|-----------------|------------------|
| Not started | Neutral — "Complete verification" | `/creator/verify/identity` |
| In review | Warning — "Verification in review" | `/dashboard/compliance` |
| Action required | Error — "Action required" | `/dashboard/compliance` with pending items |
| Verified | Success — "Verified Creator" | `/dashboard/compliance` (read-only summary) |
| Suspended | Error — "Account restricted" | `/dashboard/compliance` with restriction detail |

This satisfies the trust-critical navigation requirement: creators always know their standing and how to resolve issues.

→ Flow: [Creator Onboarding Flow](flows/creator-onboarding-flow.md)  
→ Internal review: [Trust Verification Flow](flows/trust-verification-flow.md)

### Desktop sidebar (≥1024px)

```
┌─────────────────┬────────────────────────────────────────┐
│ [Logo]          │  Header: [Status pill] [Role ▾] [User] │
│                 ├────────────────────────────────────────┤
│ Overview        │                                        │
│ Orders          │         Main content area              │
│ Catalog         │                                        │
│ Availability    │                                        │
│ Messages        │                                        │
│ ─────────────── │                                        │
│ Analytics       │                                        │
│ Reviews         │                                        │
│ Payouts         │                                        │
│ ─────────────── │                                        │
│ Storefront      │                                        │
│ Compliance      │                                        │
│ [View storefront]│                                       │
└─────────────────┴────────────────────────────────────────┘
```

| Item | Path | Badge conditions |
|------|------|------------------|
| Overview | `/dashboard` | — |
| Orders | `/dashboard/orders` | Unconfirmed order count |
| Catalog | `/dashboard/catalog` | Draft items count |
| Availability | `/dashboard/availability` | — |
| Messages | `/dashboard/messages` | Unread message count |
| Analytics | `/dashboard/analytics` | — |
| Reviews | `/dashboard/reviews` | New reviews count |
| Payouts | `/dashboard/payouts` | Pending payout indicator |
| Storefront | `/dashboard/storefront` | — |
| Compliance | `/dashboard/compliance` | Expiring docs count |
| View storefront | `/creators/:slug` | Opens public storefront in new tab |

### Mobile bottom nav — Creator

Four primary tabs plus overflow:

| Tab | Path |
|-----|------|
| **Home** | `/dashboard` |
| **Orders** | `/dashboard/orders` |
| **Catalog** | `/dashboard/catalog` |
| **More** | Overflow sheet |

**More sheet** contains: Availability, Messages, Analytics, Reviews, Payouts, Storefront Settings, Compliance, View Storefront, Role Switch, Logout.

Verification status pill remains in **header** on mobile — not relegated to More.

---

## Global Navigation — Admin / Trust & Safety

Admin uses a **persistent left rail** at all breakpoints. Mobile collapses to icon-only rail with expand on tap — content area scrolls independently.

| Item | Path | Badge |
|------|------|-------|
| Dashboard | `/admin` | — |
| Verification | `/admin/verification` | Pending queue count |
| Moderation | `/admin/moderation` | Pending items count |
| Disputes | `/admin/disputes` (list via dashboard) | Open dispute count |
| Creators | Search-driven — `/admin/creators/:creatorId` | — |
| Settings | `/admin/settings` | — |

Admin has **no customer or creator navigation items**. Operators who need to view a creator storefront use "View as public" from Creator Admin Detail — opens customer surface in new tab with admin banner (internal-only overlay).

---

## Contextual Navigation

Contextual navigation appears within a page or section — below the global shell — and scopes the user's current task.

### Customer contextual patterns

| Context | Pattern | Example |
|---------|---------|---------|
| Creator storefront | Sticky sub-header with creator name + verification | Tabs: Menu · About · Reviews |
| Menu item detail | Breadcrumb + back | Browse → Creator → Item |
| Checkout | Step indicator (horizontal) | Cart → Details → Payment → Confirm |
| Order detail | Status timeline (vertical) | Confirmed → In production → Ready → Completed |

### Creator contextual patterns

| Context | Pattern | Example |
|---------|---------|---------|
| Order detail | Status action bar + timeline | Primary: "Mark ready" |
| Catalog | List + slide-over editor | Edit item without full page leave on tablet+ |
| Menu item editor | Breadcrumb | Catalog → Item name → Edit |
| Compliance | Checklist with section anchors | Identity · Kitchen · Documents |

### Admin contextual patterns

| Context | Pattern | Example |
|---------|---------|---------|
| Verification review | Split pane: queue list + detail | Select next without page reload |
| Dispute detail | Tabbed case file | Order · Messages · Evidence · Resolution |
| Creator admin detail | Tabbed profile | Overview · Verification · Orders · Listings · Notes |

---

## Breadcrumbs

Breadcrumbs appear on **desktop and tablet** for nested entity pages. Hidden on mobile — replaced by back button with explicit parent label.

### Format

```
[Surface root] / [Section] / [Entity] / [Current — not linked]
```

### Examples

| Page | Breadcrumb |
|------|------------|
| Menu Item Detail | Home / Maria's Kitchen / Sourdough Loaf |
| Creator Order Detail | Dashboard / Orders / Order #1042 |
| Admin Creator Detail | Admin / Creators / Maria Garcia |
| Menu Item Editor | Dashboard / Catalog / Sourdough Loaf / Edit |

### Rules

- Current page is plain text — not a link
- Truncate middle segments with ellipsis when >4 levels
- Breadcrumb taps replace history entry (not push) to prevent stack buildup
- Storefront breadcrumbs use creator display name, not slug

---

## Back Behavior

Predictable back navigation is a trust feature — users must not lose cart contents, form progress, or verification uploads.

| Scenario | Back target | Behavior |
|----------|-------------|----------|
| Item detail → Storefront | Creator storefront | Preserve scroll position on storefront |
| Storefront → Search/Browse | Previous discovery page | Restore filters from session |
| Cart → Item detail | Item detail | Cart changes preserved |
| Checkout → Cart | Cart | Warn if payment in progress |
| Checkout step → Previous step | Prior checkout step | Inline state preserved |
| Order confirmation → Orders | Order history | Replace — cannot return to checkout |
| Creator order detail → Orders list | Orders list | Restore list filter state |
| Verification step → Prior step | Previous verification step | Form autosave; confirm if upload in flight |
| Admin queue item → Queue | Queue list | Select prior item in list |
| External link → Storefront | Storefront | No back beyond storefront (no off-site loop) |
| Role switch | Prior surface home | Dashboard or Home respectively |

**Browser back button:** Application state must sync with browser history via standard history API. Checkout and verification flows push history entries per step.

**Android hardware back:** Matches in-app back button behavior — never exits app unexpectedly during checkout or verification upload.

---

## Role Switching (Creator Who Is Also Customer)

Many creators are also customers. Marketplate supports dual roles under **one account** with clear context separation.

### Account menu — role switcher

Available when user has both customer and creator profiles:

```
┌─────────────────────────┐
│ Maria Garcia            │
│ maria@example.com       │
├─────────────────────────┤
│ → Shopping on Marketplate│  (switches to Customer shell → /)
│ → Creator dashboard      │  (switches to Creator shell → /dashboard)
├─────────────────────────┤
│ Account settings         │
│ Log out                  │
└─────────────────────────┘
```

### Rules

| Rule | Detail |
|------|--------|
| **Separate shells** | Role switch replaces navigation shell entirely — no hybrid UI |
| **Preserve context** | Switching stores last path per role; returning restores it |
| **Cart isolation** | Customer cart persists across role switch; not visible in creator shell |
| **Notification routing** | Order notifications route to the shell matching recipient role |
| **Creator viewing own storefront** | "View storefront" opens customer shell in new tab — prevents editing while viewing as customer |
| **Single sign-on** | One authentication session; no re-login to switch roles |

### Creator without customer activity

Creators who have never purchased see only "Creator dashboard" in account menu — no switcher until they complete a customer purchase or explicitly opt into customer profile via first checkout.

### Customer who applies to become creator

Signup path `/creator/signup` attaches creator profile to existing account. Post-approval, role switcher appears. Customer history remains under `/orders`.

→ Flow: [Creator Onboarding Flow](flows/creator-onboarding-flow.md)

---

## Trust-Critical Navigation

Trust information must be **visible early, reachable fast, and consistent everywhere**.

### Customer trust navigation

| Signal | Where surfaced | Reachability |
|--------|----------------|--------------|
| Verification badge | Storefront header, item detail, checkout summary | Above fold on storefront |
| Kitchen / production info | Storefront About tab, item detail | One tap from item |
| Allergen information | Item detail — expanded by default | Zero taps on item page |
| Review summary | Storefront header, checkout | One tap to full reviews |
| Policies (cancel/refund) | Checkout before payment | Scroll on checkout — not hidden in link |
| Help / report | Storefront footer, order detail | Two taps max |

### Creator trust navigation

| Signal | Where surfaced | Reachability |
|--------|----------------|--------------|
| Verification status pill | Creator header — all pages | Always visible |
| Compliance checklist | `/dashboard/compliance` | One tap from header pill |
| Document expiration warnings | Dashboard banner + compliance | Dashboard home + header |
| Review alerts | Reviews nav badge | One tap |
| Restriction notices | Blocking banner on affected actions | Contextual + compliance page |

### Admin trust navigation

| Signal | Where surfaced | Reachability |
|--------|----------------|--------------|
| Queue depth | Admin nav badges | Always visible in rail |
| SLA timers | Verification and dispute detail | Open case |
| Audit trail | All admin detail pages | Tab or sidebar section |
| Risk flags | Creator admin detail header | Open creator |

→ Trust model: [Marketplace Mechanics — Trust Model](../product/marketplace-mechanics.md#trust-model)

---

## Auth & Onboarding Navigation

Auth flows use the **Minimal Auth Shell** — no global nav tabs, no cart, no dashboard links.

| Page | Back | Forward / primary |
|------|------|-----------------|
| Login | Home (customer) or prior page | Dashboard (creator) or return URL |
| Signup | Login | Email verification or home |
| Creator Signup | Login | Identity verification |
| Identity Verification | Creator signup (confirm) | Kitchen verification |
| Kitchen Verification | Identity verification | Compliance center |
| Compliance Center | Kitchen verification | Dashboard (on approval) |

**Progress indicator:** Creator onboarding displays a horizontal step indicator below header:

```
Account → Identity → Kitchen → Compliance → First listing
```

Steps are tappable only for **completed** steps — future steps are locked.

Incomplete onboarding attempting to access `/dashboard/orders` redirects to the earliest incomplete verification step with explanatory message.

---

## Search Navigation

Search is a first-class navigation entry — not buried in menus.

| Entry point | Behavior |
|-------------|----------|
| Header search (desktop) | Inline expand → submit to `/search?q=` |
| Bottom tab (mobile) | Full-screen search with recent queries |
| Browse filters | Sync to search query params when keyword added |

Search results preserve nav shell. Tapping a result opens storefront or item; back returns to results with query intact.

---

## Empty & Error Navigation

Navigation remains stable in empty and error states — do not hide nav chrome.

| State | Nav behavior | CTA |
|-------|--------------|-----|
| Empty cart | Customer nav visible | "Browse creators" → `/browse` |
| Empty orders | Customer nav visible | "Discover food" → `/` |
| Empty creator orders | Creator nav visible | "Share storefront" → copy link |
| 404 | Customer shell default | "Go home" + search |
| 403 (wrong role) | Minimal shell | "Go to dashboard" or "Go home" based on role |
| Network error | Retry in place | Nav unchanged |

→ Copy guidance: [Voice and Tone — Error Messages](../brand/voice-and-tone.md#error-messages)

---

## Accessibility Requirements

| Requirement | Standard |
|-------------|----------|
| Skip link | "Skip to main content" on all shells |
| Focus order | Logo → primary nav → main → supplementary |
| Current page | `aria-current="page"` on active nav item |
| Bottom nav | `role="navigation"` + label "Main" |
| Badges | Accessible name includes count: "Orders, 3 unconfirmed" |
| Role switcher | `aria-label="Switch between shopping and creator dashboard"` |
| Verification pill | Not color-only — includes text label and icon |

→ Full standards: [Accessibility Standards](../design-system/accessibility-standards.md)

---

## Analytics Events

| Event | Trigger | Properties |
|-------|---------|------------|
| `nav_click` | Any global nav item tap/click | `item`, `surface`, `destination_path` |
| `role_switch` | Customer ↔ creator switch | `from_surface`, `to_surface` |
| `breadcrumb_click` | Breadcrumb segment click | `segment`, `depth` |
| `back_navigation` | Back button (in-app or browser) | `from_path`, `to_path`, `method` |
| `verification_pill_click` | Creator status pill click | `status`, `destination` |

---

## Related Documents

- [Information Architecture](information-architecture.md)
- [Customer Purchase Flow](flows/customer-purchase-flow.md)
- [Creator Onboarding Flow](flows/creator-onboarding-flow.md)
- [Order Fulfillment Flow](flows/order-fulfillment-flow.md)
- [Trust Verification Flow](flows/trust-verification-flow.md)
- [Product Overview](../product/overview.md)
- [Personas](../product/personas.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
- [Design System Principles](../design-system/principles.md)
- [Voice and Tone](../brand/voice-and-tone.md)
- [Pages README](README.md)
