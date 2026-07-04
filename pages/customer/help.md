# Help

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/help`  
**Surface:** Customer marketplace (web + mobile)  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Help page is Marketplate's customer-facing trust and support hub — searchable FAQs, policy explainers, verification education, and a path to human support. It answers *How does Marketplate keep me safe? What are the rules? Something went wrong — who do I contact?*

This page exists to deflect preventable support volume, reinforce the trust thesis with plain-language education, and provide contextual assistance when customers arrive from checkout, order tracking, or discovery surfaces with a specific question.

---

## Goals

### User goals

- Find answers quickly without contacting support
- Understand verification badges, kitchen transparency, and how Marketplate differs from anonymous delivery apps
- Learn cancellation, refund, fee, and allergen policies before and after purchase
- Contact support with order context when self-service fails
- Access help from any customer surface via consistent footer and contextual deep links

### Business goals

- Reduce "where is my order?" and policy clarification tickets
- Increase trust conversion by explaining verification credibly
- Provide policy URLs required at [Checkout](checkout.md) acknowledgment
- Capture support contact funnel with categorization for ops
- Measure FAQ effectiveness via search and deflection rate

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Pre- and post-purchase questions |
| **Secondary** | Customer with active order issue | Arrives via `?order=[id]` deep link |
| **Anti-persona** | Creator seeking dashboard help | Redirect to Creator OS help (future) |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| Global footer | "Help" link on all customer pages |
| [Home](home.md) | "Learn how verification works"; trust explainer CTA |
| [Creator Storefront](creator-storefront.md) | "What does Verified Kitchen mean?" |
| [Search](search.md) | Verification filter tooltip |
| [Cart](cart.md) | Fee and policy explainer links |
| [Checkout](checkout.md) | Cancellation policy checkbox; allergen FAQ |
| [Order Detail](order-detail.md) | "Get help with this order" — `?order=[id]` |
| [Order History](order-history.md) | Footer link |
| [Account Settings](account-settings.md) | Privacy and allergen disclaimer links |
| [Menu Item Detail](menu-item-detail.md) | Allergen disclaimer link |
| External / SEO | Direct `/help` or `/help#cancellations` |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Home](home.md) | Logo; "Back to shopping" |
| [Order Detail](order-detail.md) | Order-specific help resolved — "View your order" |
| [Order History](order-history.md) | "Track your orders" |
| [Browse](browse.md) | Empty FAQ search CTA |
| [Account Settings](account-settings.md) | "Manage notification preferences" |
| External | Legal policies in [`legal/`](../../legal/); mailto support |

### Global chrome

- **Top nav bar:** Logo, search, cart, account — help is secondary surface; minimal distraction
- **Tab bar (mobile):** Visible; no dedicated Help tab — reached via footer or contextual links

### Breadcrumbs

`Help` (root) · `Help > [Category]` when category selected

---

## Layout

### Content hierarchy (top to bottom)

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — logo, search, cart, account                  │
├─────────────────────────────────────────────────────────────┤
│  Page header — "Help center" (h1)                           │
│  Search input — "Search help articles"                      │
├─────────────────────────────────────────────────────────────┤
│  Order context banner (if ?order=) — Order #, status, link  │
├─────────────────────────────────────────────────────────────┤
│  Trust explainer — "How Marketplate works"                  │
│  3-step: Verified creators · Kitchen transparency ·         │
│  You know who made your food                                │
│  Verification badge glossary — Identity · Kitchen · Reviews │
├─────────────────────────────────────────────────────────────┤
│  FAQ categories — grid of category cards                    │
│  Orders · Payments & fees · Cancellations · Allergens ·     │
│  Verification · Account                                     │
├─────────────────────────────────────────────────────────────┤
│  FAQ accordion — questions within selected category         │
│  Expand/collapse answers with anchor IDs                    │
├─────────────────────────────────────────────────────────────┤
│  Contact support — category select, message, order attach   │
│  Expected response time · escalation note                   │
├─────────────────────────────────────────────────────────────┤
│  Footer — Privacy · Terms · Legal                           │
└─────────────────────────────────────────────────────────────┘
```

### Grid

| Breakpoint | Layout |
|------------|--------|
| Mobile (320–767px) | Single column; category grid 2×3; trust explainer collapsible |
| Tablet (768–1023px) | Single column; category grid 3×2 |
| Desktop (1024px+) | Max-width 960px; two-column FAQ when category selected (nav left, content right) |

### Anchor sections (required deep links)

| Anchor | Linked from |
|--------|-------------|
| `#cancellations` | [Checkout](checkout.md), [Order Detail](order-detail.md) |
| `#fees` | [Cart](cart.md) |
| `#allergens` | [Account Settings](account-settings.md), [Menu Item Detail](menu-item-detail.md) |
| `#verification` | [Home](home.md), [Search](search.md), [Creator Storefront](creator-storefront.md) |
| `#orders` | Order tracking FAQs |
| `#contact` | Support form section |

---

## Components

| Component | Usage on this page |
|-----------|-------------------|
| **Top nav bar** | Global navigation |
| **Search input** | FAQ search |
| **Order card** (compact) | Order context banner when `?order=` present |
| **Status badge** | Order status in context banner |
| **Verification badge** | Trust explainer glossary |
| **Category card** | FAQ category grid tiles |
| **Accordion** | FAQ Q&A expand/collapse |
| **Primary button** | "Contact support"; "View order" (context banner) |
| **Secondary button** | "Browse creators" (empty search) |
| **Ghost button** | "See all categories" |
| **Text input** | Support form name, email |
| **Textarea** | Support message |
| **Select** | Support category dropdown |
| **Checkbox** | Attach order to ticket (pre-checked when `?order=`) |
| **Toast** (Success) | Support ticket submitted |
| **Toast** (Error) | Submit failure |
| **Banner** (Info) | Expected response time |

---

## Interactions

### Help search

- **Search input** filters FAQ accordion in real time — debounced 300ms
- Matches question title and answer body
- No results → empty state with **Secondary button** "Contact support" and suggested categories
- Clear (×) resets filter and category selection

### Trust explainer

- Always visible above FAQ categories — not buried
- Three steps with icons:
  1. **Verified creators** — Identity verification explained
  2. **Kitchen transparency** — Where food is made
  3. **Accountability** — Reviews from verified purchases; platform moderation
- **Verification badge** glossary: tap badge → expand definition modal
  - **Verified Identity** — Government ID and business registration verified
  - **Verified Kitchen** — Production location documented and approved
- **Ghost button** "Learn more about verification" expands full explainer inline
- Link to [Creator Storefront](creator-storefront.md) example optional in v2

### FAQ categories

| Category | Sample topics |
|----------|---------------|
| **Orders** | Tracking, pickup windows, missed pickup, order not ready |
| **Payments & fees** | What fees cover, tax, receipts, payment methods |
| **Cancellations** | Customer cancel window, refunds, creator-initiated cancel |
| **Allergens & dietary** | Platform disclaimer, creator responsibility, severe allergies |
| **Verification & trust** | Badge meanings, unverified creators, reporting concerns |
| **Account** | Password, addresses, notifications, delete account |

- Category card tap → scroll to accordion group; URL updates `?category=`
- FAQ item expand → URL hash `#cancellations`, `#fees`, etc. for shareable anchors

### Key FAQ content (v1)

**Cancellations** (`#cancellations`):
- Customer may cancel within creator/policy window before production starts
- Custom orders and deposits may have different rules — disclosed at checkout
- Refunds process in 5–10 business days to original payment method
- Creator-initiated cancel → full refund automatically
- Link to [Order Detail](order-detail.md) for cancel action when eligible

**Fees** (`#fees`):
- Item price set by creator; platform service fee shown at [Cart](cart.md) and checkout
- Fees support verification, payments, and customer support
- Tax calculated based on jurisdiction and fulfillment type
- No hidden fees — total shown before payment

**Allergens** (`#allergens`):
- Creators disclose allergens per item; customers must acknowledge at checkout
- Marketplate does not guarantee allergen-free preparation — kitchens may handle multiple ingredients
- Severe allergies: restate in checkout notes; contact creator via order when urgent
- Link to [Account Settings](account-settings.md) for exclusion preferences

### Order context banner

- Shown when `?order=[orderId]` query param present (from [Order Detail](order-detail.md))
- **Order card** compact: order number, **Status badge**, creator name
- **Primary button** "View order" → [Order Detail](order-detail.md)
- Pre-selects support category "Order issue" and attaches order ID

### Contact support

- Form fields: category **Select**, name, email (pre-filled if auth), message **Textarea**
- **Checkbox** "Include order #[number]" when order context available
- **Primary button** "Submit" → POST ticket → **Success toast** "We typically respond within 24 hours."
- Unauthenticated users can submit — email required
- Duplicate submission guard: disable button 30s after success
- Sensitive issues (food safety, allergic reaction): category routes to priority queue

### Keyboard

- Skip link → search → category grid → accordion headers
- Accordion: Enter/Space toggles; arrow keys move between headers
- Support form: logical tab order; error summary at top on validation fail

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Category select | Accordion group fade-in 200ms |
| FAQ expand | Accordion height 200ms ease-out |
| Search filter | Results crossfade 150ms |
| Trust explainer expand | Height 250ms ease-out |
| Support submit success | **Success toast** slide-up; form replace with confirmation card |

Respect `prefers-reduced-motion`: instant accordion toggle; no crossfade.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Trust explainer collapsed behind "How Marketplate works"; category grid 2 columns; sticky contact CTA at bottom when scrolling FAQs |
| **Tablet** | Trust explainer visible; category grid 3 columns |
| **Desktop** | Two-column layout with sticky category nav; trust explainer always expanded |

**Content parity:** Cancellation, fee, and allergen policy summaries accessible on all breakpoints — not desktop-only footnotes.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Initial load | Search skeleton + 6 category card skeletons + 4 accordion skeletons |
| FAQ content | Static markdown/CMS — no loading after shell |
| Support submit | **Primary button** loading "Sending…" |
| Order context banner | Compact **Order card** skeleton when fetching order |

Help content may be statically generated at build time — target TTFB < 200ms.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| FAQ load failure (CMS) | "Help content unavailable." | **Primary button** "Try again" |
| Support submit failed | **Error toast**: "Couldn't send message. Try again." | Retry |
| Invalid order context (`?order=`) | Banner omitted; generic support form | — |
| Order fetch failed for banner | "Couldn't load order details." inline in banner | Proceed without attachment |
| Search error | Treat as zero results | Clear search |
| Rate limited (support spam) | "Too many requests. Try again in an hour." | — |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| Search zero results | "No articles match '[query]'." | **Primary button** "Contact support" · **Secondary button** "Clear search" |
| Category has no articles (edge) | "Articles coming soon." | **Ghost button** "Browse all categories" |

---

## Permissions

| Capability | Guest | Authenticated customer |
|------------|-------|------------------------|
| View help / FAQs | ✓ | ✓ |
| Search FAQs | ✓ | ✓ |
| View trust explainer | ✓ | ✓ |
| Contact support | ✓ (email required) | ✓ (pre-filled) |
| Attach order to ticket | ✗ (manual order # entry) | ✓ (own orders via picker or `?order=`) |
| View order context banner | ✗ | ✓ (own order only) |

Help is fully public except order-attached context requires ownership verification.

---

## Analytics

### Page events

| Event | Properties |
|-------|------------|
| `page_view` | `page: help`, `category`, `order_id`, `referrer_page` |
| `help_search` | `query`, `result_count` |
| `help_category_clicked` | `category` |
| `help_faq_expanded` | `faq_id`, `category` |
| `help_anchor_navigated` | `anchor: cancellations | fees | allergens | verification` |
| `help_trust_explainer_opened` | — |
| `help_verification_badge_clicked` | `badge: identity | kitchen` |
| `help_contact_started` | `category` |
| `help_contact_submitted` | `category`, `order_attached: boolean` |
| `help_order_context_viewed` | `order_id` |
| `help_deflection` | `faq_id` — fired when user navigates away within 30s of expand without contact |

### Funnel metrics

- FAQ search → answer expand rate
- Help → contact support conversion rate
- Contextual entry (`?order=`) → ticket submission rate
- Trust explainer engagement vs. storefront conversion (correlation)

→ [Customer Metrics](../../product/success-metrics-overview.md#customer-metrics)

---

## Accessibility

- **Landmark regions:** `banner` (nav), `main` (help content), `search` (FAQ search), `contentinfo` (footer)
- **Page heading:** h1 "Help center"
- **Trust explainer:** h2 "How Marketplate works"; steps in ordered list
- **FAQ accordion:** `button` headers with `aria-expanded`; panel `id` linked via `aria-controls`
- **Anchor sections:** Heading elements with stable `id` attributes for deep links
- **Search:** `aria-label="Search help articles"`; live region announces result count
- **Support form:** Required fields marked; errors in `role="alert"` summary
- **Verification badges:** Text labels always visible — not icon-only

→ [Accessibility Standards](../../design-system/accessibility-standards.md)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Help Center — Verified Local Food | Marketplate |
| `<meta name="description">` | FAQs on orders, fees, cancellations, allergens, and how Marketplate verification works. Contact support for order help. |
| Canonical | `https://marketplate.com/help` |
| Structured data | `FAQPage` for top FAQ entries (cancellations, fees, verification) |

Help is indexable. Policy anchors (`#cancellations`, `#fees`) may be linked from checkout and cart.

---

## Future Improvements

- In-app chat support with order context
- AI-assisted FAQ search with cited answers
- Localized help content by market/jurisdiction
- Creator-specific policy overrides surfaced in order help
- Video walkthrough of verification process
- Community forum / peer Q&A (moderated)
- Proactive help suggestions on [Order Detail](order-detail.md) by status

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/help/articles` | GET | FAQ content by category; optional `q` search |
| `/api/v1/help/categories` | GET | Category list with counts |
| `/api/v1/support/tickets` | POST | Submit support request |
| `/api/v1/customers/me/orders/:orderId` | GET | Order context banner (auth, own order) |

Support ticket payload:
- `category`, `name`, `email`, `message`
- `order_id` (optional, verified ownership)
- `referrer_page`, `user_agent` (for routing)

FAQ content may be served from static CMS at build time — API optional for v1 if content is bundled.

Response for articles includes:
- `id`, `category`, `question`, `answer_html`, `anchor`, `sort_order`, `related_links[]`

---

## Related Pages

- [Home](home.md) — Trust explainer entry; footer link
- [Creator Storefront](creator-storefront.md) — Verification badge context
- [Search](search.md) — Verification filter education
- [Browse](browse.md) — Collection curation FAQ
- [Menu Item Detail](menu-item-detail.md) — Allergen disclaimer
- [Cart](cart.md) — Fee explainer
- [Checkout](checkout.md) — Cancellation policy acknowledgment
- [Order Detail](order-detail.md) — Order-specific help entry
- [Order History](order-history.md) — Order tracking FAQs
- [Account Settings](account-settings.md) — Notification and dietary preference management
