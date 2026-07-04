# Creator Storefront

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/creator/:creatorSlug`  
**Surface:** Customer marketplace  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Creator Storefront is Marketplate's primary conversion surface — where discovery becomes purchase intent. It presents a verified creator's identity, story, kitchen transparency, menu, reviews, and fulfillment options in one calm, trust-forward view.

Customers must leave this page able to answer: *Who made this food? Where is it prepared? What can I order? How do I get it?*

---

## Goals

### User goals

- Evaluate creator trustworthiness before browsing the menu
- Read the creator's story and understand their food philosophy
- Browse menu sections and find items matching dietary needs
- Add items to cart and proceed toward [Cart](cart.md)
- Read authentic reviews from verified purchases

### Business goals

- Maximize storefront → cart conversion
- Surface verification and compliance credentials prominently
- Communicate fulfillment constraints (pickup windows, lead times) before cart
- Drive repeat visits via follow/bookmark (future)
- Support creator share links as acquisition channel

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Evaluating trust before purchase |
| **Secondary** | Returning customer | Fast path to reorder favorites |
| **Anti-persona** | Competitor scraping menus | Rate-limited; no bulk export |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| [Home](home.md), [Search](search.md), [Browse](browse.md) | Creator card tap |
| Creator share link | Direct URL; primary creator acquisition |
| [Order History](order-history.md) | "Order again" |
| [Cart](cart.md) | "Continue shopping" (same creator) |
| External / social | `marketplate.com/creator/[slug]` |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Menu Item Detail](menu-item-detail.md) | Menu item tap |
| [Cart](cart.md) | Cart icon, floating cart bar |
| [Search](search.md) | Nav search |
| [Help](help.md) | "What does Verified Kitchen mean?" |

---

## Layout

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — back, search, cart                           │
├─────────────────────────────────────────────────────────────┤
│  Storefront header                                          │
│  ┌─────────┐  Creator name (h1)                             │
│  │ Avatar  │  Verification badges (Identity, Kitchen)       │
│  │ (large) │  Rating summary · cuisine tags                  │
│  └─────────┘  Fulfillment: Pickup · Delivery                │
├─────────────────────────────────────────────────────────────┤
│  Cover photo — kitchen or signature dish (optional)         │
├─────────────────────────────────────────────────────────────┤
│  About — creator story (2–4 paragraphs, expandable)         │
│  Production — "Prepared at verified kitchen in [area]"      │
├─────────────────────────────────────────────────────────────┤
│  Fulfillment info strip — hours, lead time, service area    │
├─────────────────────────────────────────────────────────────┤
│  Menu section nav — sticky tabs (Breakfast, Mains, etc.)    │
├─────────────────────────────────────────────────────────────┤
│  Menu sections                                              │
│  ┌─ Menu item card ─────────────────────────────────────┐  │
│  │  Photo, name, price, dietary badges, brief description  │  │
│  │  Sold out overlay if applicable                       │  │
│  │  Quick add (+) or tap for detail                      │  │
│  └───────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│  Reviews — aggregate + Review cards (paginated)             │
├─────────────────────────────────────────────────────────────┤
│  Policies — cancellation, allergens disclaimer link         │
├─────────────────────────────────────────────────────────────┤
│  Floating cart bar (mobile) — item count, subtotal, View cart│
└─────────────────────────────────────────────────────────────┘
```

### Content hierarchy

1. **Trust** — Identity, verification badges, rating (above fold)
2. **Story** — Human connection
3. **Menu** — Commerce
4. **Social proof** — Reviews
5. **Policies** — Pre-purchase transparency

---

## Components

| Component | Usage |
|-----------|-------|
| **Creator avatar** | Large header avatar |
| **Verification badge** | Identity + Kitchen; tooltip with credential detail |
| **Category badge** | Cuisine tags |
| **Dietary badge** | Menu item dietary tags |
| **Status badge** | "Open now" / "Closed" / "Sold out" on items |
| **Menu item card** | Menu listing with photo, price, tags |
| **Review card** | Customer reviews with date and rating |
| **Search input** | Search within menu (client-side filter) |
| **Segmented control** | Menu section tabs (sticky) |
| **Primary button** | "View cart" on floating bar |
| **Secondary button** | "Add to order" quick-add on item card |
| **Ghost button** | "Read more" on truncated story |
| **Detail modal** | Quick-add variant selection on mobile |
| **Confirmation modal** | Verification badge credential explainer |
| **Toast** (Success) | "Added to cart" with undo |
| **Pagination** | Reviews list |

---

## Interactions

### Header and trust

- Verification badge tap → **Confirmation modal** or tooltip explaining credential scope per [naming conventions](../../brand/naming-conventions.md#verification--trust-labels)
- Rating tap → scroll to reviews section
- Production location tap → expands detail (neighborhood/city; full address may appear post-purchase per policy)

### Menu

- Menu section tab → smooth scroll to section; updates URL hash `#section-slug`
- Menu search → client-side filter by name, ingredient, dietary tag; highlights matches
- Menu item card tap → [Menu Item Detail](menu-item-detail.md)
- Quick add (+) → if no variants, add 1 to cart with **Success toast** + undo (5s); if variants exist, open **Detail modal**
- Sold-out items → disabled add; **Status badge** "Sold out"; tap still opens detail for info

### Cart

- Floating cart bar appears when `cart.items > 0` for this creator
- Tap "View cart" → [Cart](cart.md)
- Cart enforces single-creator cart in v1 — adding from different creator prompts replace-cart **Confirmation modal**

### Reviews

- Paginated; sort by Most recent (default) or Highest rated
- Verified purchase label on every review
- Creator response displayed inline below review when present

### Share

- Share button (ghost, header) → native share sheet or copy link

### Keyboard

- Menu section tabs: arrow key navigation
- Menu items: Enter opens detail; `+` quick-add when focused

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Sticky menu tabs | Tabs pin with subtle shadow fade-in 200ms on scroll past header |
| Quick add | Cart icon badge bounce 150ms; toast slide-up |
| Section scroll | Smooth scroll 300ms (disabled with reduced motion) |
| Menu filter | Non-matching items fade to 40% opacity 150ms |
| Cover photo | Blur-up load 300ms |

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Stacked header; horizontal scroll menu tabs; floating cart bar; full-width item cards |
| **Tablet** | Side-by-side header (avatar + info); 2-column menu grid |
| **Desktop** | Max-width 960px content; 2-column menu; reviews in single column; sticky section nav below header |

Cover photo aspect ratio: 3:1 desktop, 16:9 mobile. Story text truncates at 3 lines on mobile with "Read more."

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Full page | Header skeleton (avatar circle + text bars) + 4 menu item card skeletons |
| Menu | Section title skeleton + item cards |
| Reviews | 2 review card skeletons |
| Cover photo | Neutral gradient placeholder |

Storefront header and first menu section prioritized in API response (field selection or parallel requests).

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Creator not found | "This storefront doesn't exist." | **Primary button** "Discover creators" → [Home](home.md) |
| Creator suspended | "This creator is not currently accepting orders." Show profile read-only, no add-to-cart | Link to [Help](help.md) |
| Menu load failure | "Menu couldn't load." inline | **Secondary button** "Try again" |
| Add to cart failure | **Error toast**: "Couldn't add item. Try again." | Retry |
| Unverified creator (edge case) | Full-page block: "This creator is not verified and cannot accept orders." | Redirect to [Search](search.md) |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| Menu empty (no published items) | "Menu coming soon. Follow for updates." (future) | Share link **Secondary button** |
| No reviews yet | "No reviews yet. Be the first to order and share your experience." | — |
| Menu search no match | "No items match '[query]' in this menu." | **Ghost button** "Clear search" |
| Section empty | Section hidden — not rendered |

---

## Permissions

| Capability | Guest | Authenticated |
|------------|-------|---------------|
| View storefront | ✓ | ✓ |
| Add to cart | ✓ | ✓ |
| Leave review | ✗ | ✓ (post-completion only) |
| View full pickup address | Post-order | Post-order |

Only verified creators with active listings appear. Draft/unverified creators return 404 or suspended state to customers.

---

## Analytics

| Event | Properties |
|-------|------------|
| `page_view` | `page: storefront`, `creator_id`, `referrer` |
| `storefront_menu_item_clicked` | `creator_id`, `item_id`, `section` |
| `storefront_quick_add` | `creator_id`, `item_id`, `quantity` |
| `storefront_section_viewed` | `creator_id`, `section_slug` (scroll impression) |
| `storefront_verification_badge_clicked` | `creator_id`, `badge_type` |
| `storefront_review_page_changed` | `creator_id`, `page` |
| `storefront_share` | `creator_id`, `method` |
| `storefront_cart_bar_clicked` | `creator_id`, `item_count` |

Storefront view → cart add rate is primary conversion metric.

---

## Accessibility

- **Page title:** `[Creator Name] — Verified [Cuisine] | Marketplate`
- **Verification badges:** Alt text per badge type; expandable detail keyboard-accessible
- **Menu sections:** `h2` per section; `nav` with `aria-label="Menu sections"` for tabs
- **Sold-out items:** `aria-disabled="true"` on add button; status communicated in accessible name
- **Quick add toast:** `aria-live="polite"` with undo action focusable
- **Reviews:** Star rating supplemented with text ("4.8 out of 5, 124 reviews")
- **Cover photo:** `alt="[Creator name] cover photo"` or decorative if redundant

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | `{Creator Name} — {Cuisine} in {City} | Marketplate` |
| `<meta name="description">` | Dynamic — creator story excerpt + verification + rating |
| Canonical | `/creator/:slug` |
| Open Graph | Creator avatar or cover photo; verification in description |
| Structured data | `LocalBusiness` or `FoodEstablishment` with `aggregateRating`, `address` (city-level) |

Storefronts are indexable — primary organic landing pages for creators.

---

## Future Improvements

- Follow creator + notification on menu updates
- "Order again" section for returning customers at top of menu
- Live "Open now" for food trucks with map
- Menu item availability by pickup window
- Photo gallery of kitchen and production
- Catering inquiry CTA for caterer personas
- Multi-language menu support

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/creators/:slug` | GET | Profile: name, story, avatar, cover, verification, rating, fulfillment config, policies |
| `/api/v1/creators/:slug/menu` | GET | Menu sections and items with dietary tags, availability, lead times |
| `/api/v1/creators/:slug/reviews` | GET | Paginated reviews; params: `sort`, `page`, `limit` |
| `/api/v1/cart/items` | POST | Add item; body: `item_id`, `quantity`, `variants`, `creator_id` |

Creator response must include:
- `verification.identity`, `verification.kitchen`, `verification.compliance_summary`
- `fulfillment.types[]`, `fulfillment.lead_time`, `fulfillment.hours`, `fulfillment.service_area`
- `production_location.display` (customer-appropriate granularity)

---

## Related Pages

- [Menu Item Detail](menu-item-detail.md) — Full item information and add to cart
- [Cart](cart.md) — Cart review after adding items
- [Home](home.md) — Discovery entry
- [Search](search.md) — Find other creators
- [Order History](order-history.md) — Reorder path
- [Help](help.md) — Verification and allergen policy FAQs
