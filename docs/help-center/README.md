# Marketplate Help Center

> Public-facing help content architecture — source of truth for customer and creator support articles.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Audience:** Customers (primary), creators (secondary)  
**Product surface:** [`pages/customer/help.md`](../../pages/customer/help.md) — route `/help`

---

## Purpose

The Help Center deflects preventable support volume, reinforces Marketplate's trust thesis with plain-language education, and provides structured escalation when self-service is not enough.

Content here feeds the in-app Help page, SEO-indexable article routes, contextual deep links from checkout and order tracking, and support agent reference. Governing product rules live in [Marketplace Mechanics](../../product/marketplace-mechanics.md). Voice and tone standards live in [Voice and Tone](../../brand/voice-and-tone.md).

---

## Taxonomy

Articles are organized into **22 categories**. Each category has one primary article minimum; complex topics may split into sub-articles later (e.g., `verification/identity.md`).

| Category | Slug | Primary article | Primary audience |
|----------|------|-----------------|------------------|
| Getting started | `getting-started` | [getting-started.md](getting-started.md) | Customer |
| Account | `account` | [account.md](account.md) | Customer |
| Orders | `orders` | [orders.md](orders.md) | Customer |
| Payments & fees | `payments` | [payments.md](payments.md) | Customer |
| Refunds & cancellations | `refunds` | [refunds.md](refunds.md) | Customer |
| Verification | `verification` | [verification.md](verification.md) | Creator |
| Food safety & allergens | `food-safety` | [food-safety.md](food-safety.md) | Customer |
| Trust & verification badges | `trust` | [trust.md](trust.md) | Customer |
| Reviews | `reviews` | [reviews.md](reviews.md) | Customer + Creator |
| Messaging | `messaging` | [messaging.md](messaging.md) | Customer + Creator |
| Delivery | `delivery` | [delivery.md](delivery.md) | Customer |
| Pickup | `pickup` | [pickup.md](pickup.md) | Customer |
| Storefronts | `storefronts` | [storefronts.md](storefronts.md) | Creator |
| Menus & catalog | `menus` | [menus.md](menus.md) | Creator |
| Analytics | `analytics` | [analytics.md](analytics.md) | Creator |
| Notifications | `notifications` | [notifications.md](notifications.md) | Customer + Creator |
| Privacy | `privacy` | [privacy.md](privacy.md) | Customer + Creator |
| Security | `security` | [security.md](security.md) | Customer + Creator |
| Community guidelines | `community-guidelines` | [community-guidelines.md](community-guidelines.md) | Customer + Creator |
| Platform policies | `platform-policies` | [platform-policies.md](platform-policies.md) | Customer + Creator |
| Troubleshooting | `troubleshooting` | [troubleshooting.md](troubleshooting.md) | Customer + Creator |
| Accessibility | `accessibility` | [accessibility.md](accessibility.md) | Customer + Creator |
| Contact support | `contact-support` | [contact-support.md](contact-support.md) | Customer + Creator |

### Category mapping to Help page UI

The in-app Help page ([`pages/customer/help.md`](../../pages/customer/help.md)) groups categories for customers:

| Help page card | Help Center articles |
|----------------|---------------------|
| Orders | [orders.md](orders.md), [pickup.md](pickup.md), [delivery.md](delivery.md) |
| Payments & fees | [payments.md](payments.md) |
| Cancellations | [refunds.md](refunds.md) |
| Allergens & dietary | [food-safety.md](food-safety.md) |
| Verification & trust | [trust.md](trust.md), [verification.md](verification.md) |
| Account | [account.md](account.md), [notifications.md](notifications.md), [privacy.md](privacy.md), [security.md](security.md) |

Creator-specific articles surface in Creator OS help (future) and link from creator dashboard contextual help.

---

## Article Template

Every help article follows this structure. Do not publish articles missing required sections.

```markdown
# [Article Title]

> Help Center · [Category]
> Route: /help/[slug]
> Last updated: YYYY-MM-DD

## Overview
One to three paragraphs. Lead with the most important information.
State who the article is for (customer, creator, or both).

## Step-by-step guidance
### [Step name]
Numbered or procedural steps. One primary action per step.

[Screenshot: Describe exactly what the screenshot shows — UI region, labels, state]

Repeat steps and screenshot placeholders as needed.

## Common issues
| Issue | Likely cause | What to do |
|-------|--------------|------------|
| ... | ... | ... |

## FAQs
### [Question]?
Direct answer. Specific timing, amounts, or policy references where applicable.

## Related articles
- [Article title](filename.md) — one-line description
- [Page spec](../../pages/...) — when linking to product surfaces

## Escalation guidance
When self-service is insufficient: support category, expected response time,
what information to include, priority routing notes (food safety, allergic reaction, etc.).
```

### Writing rules

Follow [Voice and Tone](../../brand/voice-and-tone.md):

- **Trustworthy** — State only what verification and policy actually cover.
- **Warm** — Use creator names; acknowledge the human experience.
- **Precise** — Specific times, amounts, and policy windows — never "soon."
- **Calm** — No artificial urgency or fear-based language.
- **Scannable** — Short paragraphs, meaningful headings, tables for comparisons.

Cross-link to [Marketplace Mechanics](../../product/marketplace-mechanics.md) for system-level rules, [`pages/`](../../pages/) for UI behavior, and [`legal/`](../../legal/) for binding policy text when Phase 5 docs exist.

---

## Search & SEO

### In-app search

Help search filters articles by title and body (debounced 300ms per [Help page spec](../../pages/customer/help.md)). Optimize for:

- **Question-shaped titles** in FAQs ("How do I cancel my order?")
- **Synonyms** in body copy (pickup window, fulfillment slot, collection time)
- **Anchor stability** — FAQ answers that map to deep links (`#cancellations`, `#fees`, `#allergens`, `#verification`)

### SEO (public routes)

| Element | Standard |
|---------|----------|
| `<title>` | `[Article title] — Help Center \| Marketplate` |
| `<meta description>` | First 155 characters of Overview, or custom summary |
| Canonical | `https://marketplate.com/help/[slug]` |
| Structured data | `FAQPage` for articles with 3+ FAQs; `BreadcrumbList` for category hierarchy |
| Indexability | All customer-facing articles indexable; creator-only articles may use `noindex` until Creator OS help launches |

### Deep links from product surfaces

| Anchor / query | Source page | Target article |
|----------------|-------------|----------------|
| `#cancellations` | [Checkout](../../pages/customer/checkout.md), [Order Detail](../../pages/customer/order-detail.md) | [refunds.md](refunds.md) |
| `#fees` | [Cart](../../pages/customer/cart.md) | [payments.md](payments.md) |
| `#allergens` | [Account Settings](../../pages/customer/account-settings.md), [Menu Item Detail](../../pages/customer/menu-item-detail.md) | [food-safety.md](food-safety.md) |
| `#verification` | [Home](../../pages/customer/home.md), [Search](../../pages/customer/search.md), [Creator Storefront](../../pages/customer/creator-storefront.md) | [trust.md](trust.md) |
| `?order=[id]` | [Order Detail](../../pages/customer/order-detail.md) | [contact-support.md](contact-support.md) with order context |

---

## Escalation Paths

Self-service first. Escalate when policy exceptions, safety issues, or account access block resolution.

```
Help article → Contact support form → Support specialist → Trust & Safety / Payments ops
```

| Issue type | Support category | Response SLA | Priority queue |
|------------|------------------|--------------|----------------|
| General question | General inquiry | 24 hours | Standard |
| Order status / quality | Order issue | 24 hours | Standard |
| Payment / refund dispute | Payment & refund | 24–48 hours | Elevated if unresolved 5+ days |
| Food safety concern | Food safety | 4 hours | **Priority** |
| Allergic reaction | Food safety | 1 hour | **Critical** |
| Verification (creator) | Creator verification | 2 business days | Standard |
| Account security | Account security | 4 hours | **Priority** |
| Harassment / policy violation | Trust & safety report | 24 hours | Elevated |

Full escalation procedures: [contact-support.md](contact-support.md). Operations SOPs: [`operations/`](../../operations/) *(Phase 4)*.

### When to contact support vs. creator

| Situation | First contact |
|-----------|---------------|
| Order late, wrong item, pickup instructions | Creator via [messaging](messaging.md) |
| Creator unresponsive 24+ hours | [Contact support](contact-support.md) |
| Refund disagreement after creator contact | [Contact support](contact-support.md) |
| Suspected fraud, identity concern | [Contact support](contact-support.md) — Trust category |
| Payment charged incorrectly | [Contact support](contact-support.md) |

---

## Content Maintenance

| Trigger | Action |
|---------|--------|
| Policy change in [`legal/`](../../legal/) | Update affected articles; bump `Last updated` |
| New page spec in [`pages/`](../../pages/) | Add cross-links; update screenshot placeholders |
| Marketplace mechanics change | Review trust, orders, payments, fulfillment articles |
| Support ticket theme spike | Add FAQ or Common issues row |
| Quarterly review | Audit deflection metrics; prune outdated content |

### Analytics events

Help instrumentation per [Help page spec](../../pages/customer/help.md):

- `help_search`, `help_category_clicked`, `help_faq_expanded`
- `help_contact_started`, `help_contact_submitted`
- `help_deflection` — user leaves within 30s of FAQ expand without contacting support

---

## API & CMS (implementation reference)

| Endpoint | Purpose |
|----------|---------|
| `GET /api/v1/help/articles` | Articles by category; optional `q` search |
| `GET /api/v1/help/categories` | Category list with article counts |
| `POST /api/v1/support/tickets` | Support request submission |

Article payload fields: `id`, `category`, `question`, `answer_html`, `anchor`, `sort_order`, `related_links[]`.

v1 may bundle static markdown at build time — API optional if content is pre-rendered.

---

## Related Documents

- [Help Page Spec](../../pages/customer/help.md) — UI implementation
- [Marketplace Mechanics](../../product/marketplace-mechanics.md) — System rules
- [Voice and Tone](../../brand/voice-and-tone.md) — Writing standards
- [Creator Onboarding](../onboarding/README.md) — Creator welcome content
- [Information Architecture](../../pages/information-architecture.md) — Site structure
- [Accessibility Standards](../../design-system/accessibility-standards.md) — A11y requirements
