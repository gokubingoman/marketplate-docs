# Customer Home

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/`  
**Surface:** Customer marketplace (web + mobile)  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Customer Home page is Marketplate's discovery landing surface — the first impression for trust-seeking buyers. It answers three questions immediately: *Who can I buy from here? Are they verified? How do I start?*

This page exists to convert curiosity into confident exploration. It showcases verified local creators, provides a prominent search entry point, and reinforces Marketplate's trust thesis before the customer commits to a specific storefront or menu item.

---

## Goals

### User goals

- Quickly discover verified food creators near them or in their area of interest
- Understand what Marketplate is and why buying here is different from anonymous delivery apps
- Start a search or browse path with minimal friction
- See social proof (ratings, verification, repeat purchase signals) at a glance

### Business goals

- Drive click-through to [Search](search.md), [Browse](browse.md), and [Creator Storefront](creator-storefront.md)
- Establish trust positioning in the first 5 seconds of session
- Surface featured verified creators who meet minimum trust thresholds
- Capture location context (when permitted) to improve discovery relevance
- Measure discovery funnel entry and first-click depth

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | First-time and returning visitors seeking verified local food |
| **Secondary** | Returning customer with order history | Personalized "Order again" and favorites modules |
| **Anti-persona** | Price-comparison delivery app user | Not optimized for speed-first anonymous ordering |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| Direct URL / bookmark | Default landing |
| Marketing campaigns | UTM-tagged acquisition |
| Creator share links | May deep-link to storefront; home remains global entry |
| Mobile app launch | Tab bar "Home" selection |
| Post-logout redirect | Returns to home |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Search](search.md) | Search input submit, suggested query tap, filter chip |
| [Browse](browse.md) | Category/collection card tap |
| [Creator Storefront](creator-storefront.md) | Featured creator card, "Order again" card |
| [Order History](order-history.md) | Active order banner, tab bar "Orders" |
| [Account Settings](account-settings.md) | Top nav account menu |
| [Help](help.md) | Footer link, trust explainer "Learn more" |

### Global chrome

- **Top nav bar:** Logo (home), Search input (collapsed on mobile → expands on tap), Cart icon with count badge, Account avatar/menu
- **Tab bar (mobile):** Home (active), Search, Orders, Account

---

## Layout

### Content hierarchy (top to bottom)

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — logo, search, cart, account                    │
├─────────────────────────────────────────────────────────────┤
│  Hero — headline, trust value prop, primary search entry      │
├─────────────────────────────────────────────────────────────┤
│  Trust strip — "Verified creators · Kitchen transparency"     │
├─────────────────────────────────────────────────────────────┤
│  Active order banner (if applicable) — status + link        │
├─────────────────────────────────────────────────────────────┤
│  Order again — horizontal scroll of recent creators           │
├─────────────────────────────────────────────────────────────┤
│  Featured verified creators — 2-col grid / horizontal scroll  │
├─────────────────────────────────────────────────────────────┤
│  Browse collections — category cards (cuisine, dietary)     │
├─────────────────────────────────────────────────────────────┤
│  Near you (location-aware) — creator cards with distance      │
├─────────────────────────────────────────────────────────────┤
│  How Marketplate works — 3-step trust explainer (collapsed   │
│  on mobile behind "Learn how verification works")             │
├─────────────────────────────────────────────────────────────┤
│  Footer — Help, policies, social                            │
└─────────────────────────────────────────────────────────────┘
```

### Grid

| Breakpoint | Layout |
|------------|--------|
| Mobile (320–767px) | Single column; horizontal scroll rows for cards |
| Tablet (768–1023px) | 2-column creator grid; full-width hero |
| Desktop (1024px+) | Max-width 1200px container; 3-column creator grid; hero with inline search |

### Visual weight

- Food photography and creator avatars carry visual interest; UI chrome stays neutral
- Verification badges appear on every creator card — never below the fold on card face
- Whitespace between sections per [design principles](../../design-system/principles.md)

---

## Components

| Component | Usage on this page |
|-----------|-------------------|
| **Top nav bar** | Persistent global navigation |
| **Tab bar (mobile)** | Bottom navigation on mobile |
| **Search input** | Hero search; expands from nav on mobile |
| **Primary button** | "Search creators" (hero CTA when search empty) |
| **Secondary button** | "Browse all categories" |
| **Ghost button** | "Learn how verification works" |
| **Creator card** | Featured creators, near-you results, order-again row |
| **Verification badge** | On every creator card — Identity + Kitchen where applicable |
| **Category badge** | Cuisine tags on creator cards |
| **Dietary badge** | Featured dietary collections (e.g., "Vegan-friendly") |
| **Order card** (compact) | Active order banner — status, ETA, link to [Order Detail](order-detail.md) |
| **Creator avatar** | Creator card header |
| **Status badge** | Active order status in banner |
| **Toast** (Info) | Location permission prompt result |

---

## Interactions

### Search entry

- Tapping search input focuses field; on mobile, may navigate to [Search](search.md) with keyboard open
- Typing shows inline suggestions (creators, cuisines, recent searches) — debounced 300ms
- Submit navigates to [Search](search.md) with query param `?q=`
- Clear button (×) resets input

### Creator cards

- Tap card body → [Creator Storefront](creator-storefront.md)
- Verification badge tap → tooltip/modal explaining credential (does not navigate away)
- Long-press (mobile) → no action in v1 (avoid hidden gestures)

### Location

- "Near you" section shows location prompt if permission not granted
- "Use my location" → browser geolocation API; on deny, section hidden with "Set location in account" link to [Account Settings](account-settings.md)
- Manual location override via account preferred address

### Order again

- Visible only for authenticated users with completed orders
- Tap → [Creator Storefront](creator-storefront.md) with last-ordered items highlighted (future: direct reorder)

### Collections

- Tap category card → [Browse](browse.md) with collection slug

### Keyboard

- Tab order: skip link → logo → search → cart → account → main content sections
- Enter on focused creator card opens storefront

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Page load | Staggered fade-in for card rows (50ms offset); respects `prefers-reduced-motion` |
| Search focus | Input expands 200ms ease-out on mobile |
| Card hover (desktop) | Subtle elevation increase, 150ms |
| Active order banner | Slide-down on mount if order status changed since last visit |
| Skeleton → content | Crossfade 200ms when data resolves |

No auto-playing carousels. Featured creators use manual horizontal scroll on mobile.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Hero stacks vertically; search full-width; creator rows horizontal scroll; trust strip single line with truncation + expand; tab bar visible |
| **Tablet** | 2-column grids; search inline in hero; tab bar hidden if top nav sufficient |
| **Desktop** | 3-column creator grid; "How it works" visible inline; sticky top nav on scroll |

**Content parity:** Verification badges, ratings, and fulfillment type visible on all breakpoints — never hidden on mobile.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Initial page | Full-page skeleton: hero placeholder, 6 creator card skeletons, 4 collection card skeletons |
| Featured creators | Creator card skeletons with image + text bars |
| Near you | Deferred load after location resolved; skeleton until ready |
| Order again | Skeleton row; hidden until auth + data confirmed |
| Search suggestions | Inline spinner in dropdown after 300ms debounce |

Progressive loading: above-the-fold hero and featured creators first; near-you and order-again lazy-loaded.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Featured creators API failure | Inline error in section: "We couldn't load featured creators." | **Secondary button** "Try again" |
| Location service error | Near-you section shows manual location CTA | Link to [Account Settings](account-settings.md) |
| Partial data (some cards fail) | Render successful cards; omit failed with logged error | Automatic retry on scroll-into-view |
| Auth token expired (order banner) | Banner hidden; no blocking error | Silent re-auth prompt on next protected action |
| Network offline | Top **Info toast**: "You're offline. Some content may be outdated." | Cached featured list if available |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| No featured creators in market (launch) | "Verified creators are coming to your area. Browse categories or search to explore." | **Primary button** "Browse categories" → [Browse](browse.md) |
| Location granted, zero nearby | "No verified creators near you yet. Try expanding your search." | **Secondary button** "Search all creators" → [Search](search.md) |
| New user, no order again | Section omitted entirely — not shown |
| No active orders | Banner omitted — not shown |

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| View home | ✓ | ✓ |
| Search / browse | ✓ | ✓ |
| View creator cards | ✓ | ✓ |
| Order again module | ✗ | ✓ (with order history) |
| Active order banner | ✗ | ✓ |
| Location personalization | Opt-in | Uses account address + opt-in geolocation |
| Cart badge count | Session cart | Persisted cart |

Unverified creators never appear in featured or near-you modules per [marketplace mechanics](../../product/marketplace-mechanics.md#ranking-principles).

---

## Analytics

### Page events

| Event | Properties |
|-------|------------|
| `page_view` | `page: home`, `referrer`, `utm_*` |
| `home_search_initiated` | `source: hero | nav` |
| `home_search_submitted` | `query`, `suggestion_used: boolean` |
| `home_creator_card_clicked` | `creator_id`, `section: featured | near_you | order_again`, `position` |
| `home_collection_clicked` | `collection_slug`, `section` |
| `home_trust_explainer_opened` | — |
| `home_location_prompt_shown` | — |
| `home_location_granted` | `precision: coarse | fine` |

### Funnel metrics

- Home → storefront CTR by section
- Home → search CTR
- Time to first click
- Bounce rate vs. discovery depth

→ [Customer Metrics](../../product/success-metrics-overview.md#customer-metrics)

---

## Accessibility

- **Landmark regions:** `banner` (nav), `main` (content), `contentinfo` (footer)
- **Skip link:** "Skip to featured creators" as first focusable element
- **Search input:** `aria-label="Search verified food creators"`, autocomplete listbox with `aria-activedescendant`
- **Creator cards:** Entire card is one focusable link; verification badge has separate focus stop with `aria-describedby` tooltip
- **Horizontal scroll rows:** Arrow key navigation between cards; `aria-label` on scroll container
- **Active order banner:** `role="status"` with `aria-live="polite"` on status change
- **Color:** Ratings and verification never conveyed by color alone
- **Touch targets:** Minimum 44×44px on all interactive elements
- **Motion:** All animations disabled when `prefers-reduced-motion: reduce`

→ [Accessibility Standards](../../design-system/accessibility-standards.md)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Marketplate — Verified Local Food from Independent Creators |
| `<meta name="description">` | Discover and order from verified local chefs, bakers, and food creators. Identity and kitchen verification on every storefront. |
| Canonical | `https://marketplate.com/` |
| Open Graph | Brand image + tagline; no creator-specific content on home |
| Structured data | `WebSite` with `SearchAction` potential (sitelinks search box) |

Home is indexable. No `noindex`.

---

## Future Improvements

- Personalized home feed based on dietary preferences from [Account Settings](account-settings.md)
- "Follow creator" module for opted-in notifications
- Seasonal editorial hero with founder-curated collections
- Map view entry for food trucks and pop-ups
- A/B test trust explainer placement vs. implicit trust via badges only
- Guest checkout completion prompt on return visit

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/discovery/featured` | GET | Featured verified creators; query: `lat`, `lng`, `limit` |
| `/api/v1/discovery/collections` | GET | Browse collection cards for home |
| `/api/v1/discovery/nearby` | GET | Location-aware creators; requires `lat`, `lng`, `radius_km` |
| `/api/v1/customers/me/orders/active` | GET | Active order banner (auth) |
| `/api/v1/customers/me/orders/recent-creators` | GET | Order again row (auth) |
| `/api/v1/search/suggest` | GET | Typeahead suggestions; query: `q`, `limit` |
| `/api/v1/cart` | GET | Cart count for nav badge |

All discovery endpoints must enforce verified-only filter for featured modules. Response includes: `creator_id`, `slug`, `name`, `avatar_url`, `verification_status`, `rating_summary`, `cuisine_tags`, `fulfillment_types`, `distance_km` (if location provided).

---

## Related Pages

- [Search](search.md) — Full search results with filters
- [Browse](browse.md) — Category and collection browsing
- [Creator Storefront](creator-storefront.md) — Creator profile and menu
- [Order Detail](order-detail.md) — Active order tracking from banner
- [Order History](order-history.md) — Past orders
- [Account Settings](account-settings.md) — Location and dietary preferences
- [Help](help.md) — Trust and verification FAQs
