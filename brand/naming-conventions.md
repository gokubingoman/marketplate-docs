# Naming Conventions

> Consistent rules for product names, features, UI copy, and capitalization across Marketplate.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Naming is a trust surface. Inconsistent or confusing names erode confidence — especially in food, where clarity about what something *is* affects safety and expectations.

These conventions apply to product UI, marketing, documentation, support, and engineering identifiers where user-visible.

---

## Product Naming

### Company and platform

| Name | Usage | Capitalization |
|------|-------|----------------|
| **Marketplate** | The company and platform | Always capitalized; one word |
| **Marketplate for Creators** | Creator-facing product context (if needed) | Title case |
| **Marketplate for Customers** | Customer-facing app context (if needed) | Title case |

**Correct:** "Sell on Marketplate," "Your Marketplate storefront," "Download the Marketplate app"

**Incorrect:** "marketplate," "Market Plate," "MarketplateApp," "MP" in customer-facing copy

TODO(decision): Consumer app name at launch — see [ADR-009](../decisions/adr-009-consumer-app-naming.md) (recommends unified **Marketplate**).

### Creator vs. customer products

| Audience | Preferred term | Avoid |
|----------|----------------|-------|
| Food entrepreneur | **Creator** | Seller, vendor, merchant, partner (internal ops excepted) |
| Buyer | **Customer** | User, consumer, buyer (internal analytics excepted) |
| Creator's business | **[Creator Name]** or **storefront** | Shop (ambiguous with Shopify), store (retail connotation) |

In UI, prefer the **creator's actual name** over generic labels: "Order from Maria's Kitchen" not "Order from creator."

---

## Feature Naming

### Principles

1. **Descriptive over clever** — "Pickup windows" not "TimeSlots Pro"
2. **Food-native vocabulary** — Terms creators already use
3. **Consistent across surfaces** — Same name in UI, docs, and support
4. **No trademark conflicts** — Avoid names that mirror competitor features

### Standard feature names

| Feature | Name | Not |
|---------|------|-----|
| Creator profile page | **Storefront** | Shop page, vendor page |
| Order collection point | **Pickup** | Fulfillment, handoff |
| Scheduled availability | **Pickup window** | Time slot, delivery window |
| Weekly offering | **Menu** | Catalog, inventory |
| Recurring orders | **Subscription** | Auto-order, repeat buy |
| Identity check | **Identity verification** | ID check, KYC (customer-facing) |
| Production site check | **Kitchen verification** | Facility audit |
| Buyer feedback | **Review** | Rating, feedback |
| Trust indicators | **Verification badge** | Trust seal, certified |

New features require a name review against this doc before launch. Significant naming changes get an ADR in [`decisions/`](../decisions/).

---

## Verification & Trust Labels

Verification labels are **credential-based**, not marketing superlatives.

| Label | Meaning | Usage |
|-------|---------|-------|
| **Verified Identity** | Government ID + identity check complete | Creator profile, checkout trust strip |
| **Verified Kitchen** | Production environment verified | Creator profile, menu pages |
| **Food safety documentation on file** | Required docs submitted and reviewed | Creator profile, compliance contexts |

**Do not use:** "Certified," "Approved," "Top Creator," "Premium Seller" unless tied to a defined, auditable program.

---

## UI Copy Conventions

### Buttons and CTAs

| Pattern | Example | Notes |
|---------|---------|-------|
| Primary action | **Place order** | Verb-first, sentence case |
| Secondary action | **View menu** | Verb-first |
| Destructive action | **Cancel order** | Name the consequence |
| Navigation | **Back to menu** | Destination clear |

**One primary action per screen** — per [design principles](../design-system/principles.md). Secondary actions use ghost or text button styling.

### Labels and headings

- **Sentence case** for UI labels, buttons, headings, and toasts: "Pickup details," not "Pickup Details"
- **Title case** for marketing headlines and document titles only
- **No periods** on button labels or standalone headings
- **No ellipsis** on buttons except "Loading…" and in-progress states

### Numbers, money, and time

| Type | Format | Example |
|------|--------|---------|
| Currency | Symbol + two decimals | $24.00 |
| Time | 12-hour with AM/PM, en-dash for ranges | 11:00 AM–11:30 AM |
| Dates | Weekday + month + day | Saturday, July 12 |
| Quantities | Numerals | 2 items |

Use the customer's locale for formatting at implementation time; US English defaults at launch.

### States

| State | Copy pattern |
|-------|--------------|
| Loading | "Loading menu…" / "Placing order…" |
| Empty | "[Thing] is empty. [Action to fix]." |
| Success | "[Thing] confirmed." + next step if needed |
| Error | See [voice-and-tone.md](voice-and-tone.md#error-messages) |

---

## Capitalization Rules

| Context | Rule | Example |
|---------|------|---------|
| Product name | Always capitalize | Marketplate |
| Feature names (UI) | Sentence case | Pickup window |
| Feature names (docs title) | Title case | Pickup Window |
| Creator names | As creator styles them | Maria's Kitchen |
| Verification labels | Title case | Verified Identity |
| Generic food terms | Lowercase unless proper noun | sourdough bread, French macarons |
| Acronyms | All caps on first use with expansion | SLA (Service Level Agreement) |
| File/code identifiers | kebab-case or snake_case per engineering standards | `pickup-window`, `verified_identity` |

---

## Terminology: Preferred vs. Avoid

| Preferred | Avoid | Reason |
|-----------|-------|--------|
| Creator | Vendor, seller | Brand-aligned, human |
| Customer | User | Commerce clarity |
| Storefront | Shop, page | Distinct from generic e-commerce |
| Pickup | Delivery (when not delivery) | Accurate fulfillment model |
| Menu | Catalog | Food-native |
| Order | Transaction | Human commerce |
| Verification | Certification (unless official) | Precision |
| Marketplate | The platform, our app | Definite, confident |

---

## Internal vs. External Naming

| Context | Convention |
|---------|------------|
| Customer-facing UI | Follow this document strictly |
| Support macros | Match UI terms exactly |
| Engineering / API | Descriptive English; user-visible strings reference copy doc |
| Analytics events | snake_case: `order_placed`, `verification_completed` |
| Internal ops | "Partner" or "vendor" acceptable in B2B contracts; not in product UI |

---

## Naming New Features

Before naming a new feature:

1. Check this doc and [voice-and-tone.md](voice-and-tone.md) for existing terms
2. Prefer a name creators already use in conversation
3. Test: Would a customer know what this is without explanation?
4. Document the name in the feature spec and link here if it becomes a platform-standard term

---

## Related Documents

- [Founding Constitution](../company/constitution.md)
- [Brand Strategy](brand-strategy.md)
- [Voice and Tone](voice-and-tone.md)
- [Design System Principles](../design-system/principles.md)
- [Components Overview](../design-system/components-overview.md)
- [Feature Doc Template](../templates/feature-doc-template.md)
