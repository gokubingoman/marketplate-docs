# Customer Search

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/search`  
**Query params:** `q`, `cuisine`, `dietary`, `fulfillment`, `verified_only`, `lat`, `lng`, `sort`  
**Surface:** Customer marketplace  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Search page is Marketplate's primary intent-driven discovery surface. Customers arrive with a specific need — a cuisine, dietary requirement, creator name, or fulfillment preference — and expect results that are relevant, verified, and transparent.

Search optimizes for **fit and confidence**, not infinite scroll engagement. Every result card must answer: *Who is this? Are they verified? How do I get their food?*

---

## Goals

### User goals

- Find verified creators and menu items matching a query or filter combination
- Refine results by cuisine, dietary needs, fulfillment type, and verification status
- Compare creators at a glance via trust signals (badges, ratings, fulfillment)
- Navigate quickly to a [Creator Storefront](creator-storefront.md) or [Menu Item Detail](menu-item-detail.md)

### Business goals

- Convert search intent to storefront visits and cart additions
- Enforce ranking principles: verified creators rank above unverified (unverified excluded when `verified_only` default is on)
- Capture filter usage for supply gap analysis (zero-result queries)
- Minimize time-to-relevant-result

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Often arrives with dietary or cuisine intent |
| **Secondary** | Returning customer searching by creator name | Direct navigation pattern |
| **Anti-persona** | User expecting restaurant chain results | Copy and filters set food-creator expectations |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| [Home](home.md) hero/nav search | Query pre-filled |
| [Browse](browse.md) "Search within collection" | Collection context preserved |
| Direct URL with query params | Shareable filtered search |
| Tab bar "Search" (mobile) | Empty search state |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Creator Storefront](creator-storefront.md) | Creator result card tap |
| [Menu Item Detail](menu-item-detail.md) | Menu item result tap |
| [Browse](browse.md) | "Browse all categories" empty-state CTA |
| [Home](home.md) | Logo tap, back navigation |

---

## Layout

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar — search input (expanded), cart, account       │
├─────────────────────────────────────────────────────────────┤
│  Filter bar — cuisine, dietary, fulfillment, verified only  │
│  [Mobile: "Filters" button opens filter sheet]              │
├─────────────────────────────────────────────────────────────┤
│  Results header — "24 verified creators for 'vegan'"        │
│  Sort: Relevance | Nearest | Top rated                      │
├─────────────────────────────────────────────────────────────┤
│  Results list                                               │
│  ┌─ Creator result card ─────────────────────────────────┐  │
│  │  Avatar, name, verification badges, rating, tags    │  │
│  │  Fulfillment: Pickup · Delivery                       │  │
│  │  Optional: top menu item thumbnails (max 3)           │  │
│  └───────────────────────────────────────────────────────┘  │
│  ┌─ Menu item result card (when item-level match) ──────┐  │
│  │  Photo, item name, price, dietary badges, creator     │  │
│  └───────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│  Pagination — load more (not infinite scroll)             │
└─────────────────────────────────────────────────────────────┘
```

### Result types

| Type | When shown |
|------|------------|
| **Creator results** | Default; creator name, cuisine, or bio match |
| **Menu item results** | Item name, ingredient, or allergen match; grouped under creator or interleaved per relevance |

### Grid

- Mobile: single-column full-width cards
- Tablet: single column with wider cards
- Desktop: single column max-width 800px centered (scannable list, not grid — calm discovery)

---

## Components

| Component | Usage |
|-----------|-------|
| **Search input** | Persistent, pre-filled with query; clear and submit |
| **Select / dropdown** | Sort control |
| **Checkbox** | Multi-select dietary filters; "Verified only" toggle |
| **Radio** | Single-select fulfillment type in filter sheet |
| **Category badge** | Cuisine tags on results; filter chips |
| **Dietary badge** | On item results and creator tags |
| **Verification badge** | Required on every creator result |
| **Creator card** | Creator-level results |
| **Menu item card** | Item-level results with creator attribution |
| **Creator avatar** | Result card header |
| **Primary button** | "Apply filters" in mobile filter sheet |
| **Ghost button** | "Clear all filters" |
| **Secondary button** | "Browse categories" in empty state |
| **Pagination** | Load more results |
| **Form modal** (mobile) | Full-screen filter sheet |
| **Toast** (Info) | "Filters applied" on mobile after sheet close |

---

## Interactions

### Search

- Query updates on submit (Enter or search icon tap) — not on every keystroke for results (suggestions only while typing)
- Debounced suggestions dropdown: recent searches, popular cuisines, matching creator names
- URL sync: all query and filter state reflected in URL for shareability and back-navigation

### Filters

| Filter | Type | Options (v1) |
|--------|------|--------------|
| Cuisine | Multi-select | Italian, Mexican, Asian, Bakery, Meal prep, BBQ, etc. |
| Dietary | Multi-select | Vegan, Vegetarian, Gluten-free, Dairy-free, Nut-free, Halal, Kosher |
| Fulfillment | Single-select | Any, Pickup, Delivery, Catering, Pop-up event |
| Verified only | Toggle (default ON) | When off, unverified creators appear with clear "Not verified" label — never mixed badge styling |

- Filter chips appear below search bar showing active filters; tap × to remove
- Mobile: "Filters" opens full-screen **Form modal** with Apply/Clear

### Sort

- Options: Relevance (default), Nearest (requires location), Top rated
- Changing sort re-fetches without clearing filters

### Results

- Creator card tap → [Creator Storefront](creator-storefront.md)
- Menu item card tap → [Menu Item Detail](menu-item-detail.md)
- Verification badge tap → credential tooltip (inline, non-navigating)
- "Load more" appends next page; focus moves to first new result

### Keyboard

- `/` focuses search from anywhere on page (when no input focused)
- Filter chips reachable via Tab; Delete/Backspace removes focused chip
- Escape closes suggestion dropdown and mobile filter sheet

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Filter chip add/remove | Chip scale-in 150ms; removal fade-out 100ms |
| Results update | Crossfade 200ms on filter/sort change |
| Mobile filter sheet | Slide-up 300ms ease-out; backdrop fade |
| Load more | New cards stagger fade-in 50ms offset |
| Skeleton resolve | Crossfade to content 200ms |

Respect `prefers-reduced-motion`: instant swap, no stagger.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Filters in bottom sheet modal; sort as dropdown; single-column results; sticky search bar |
| **Tablet** | Inline filter chips with overflow scroll; filter sheet optional |
| **Desktop** | Full inline filter bar; horizontal chip row; wider result cards with inline menu thumbnails |

Sticky search bar on scroll (all breakpoints). Results header remains visible below filters.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Initial search | 6 result card skeletons + filter bar skeleton |
| Filter/sort change | Results area skeleton overlay; filters remain interactive |
| Load more | Inline spinner below last result; existing results persist |
| Suggestions | Three suggestion skeleton lines in dropdown |

Search does not block entire page on re-query — only results region updates.

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Search API failure | "We couldn't complete your search. Check your connection and try again." | **Primary button** "Try again" |
| Invalid query (empty after trim) | Inline validation: "Enter a search term or browse categories." | Focus search input |
| Location required for "Nearest" sort, unavailable | Sort reverts to Relevance; **Warning toast**: "Nearest sort requires location. Enable in account settings." | Link to [Account Settings](account-settings.md) |
| Timeout | Same as API failure with "This is taking longer than usual." | Retry + link to [Help](help.md) |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| Zero results with filters | "No verified creators match your filters in this area." | **Ghost button** "Clear filters" + **Secondary button** "Browse all categories" |
| Zero results, query only | "No results for '[query]'. Try a different term or browse categories." | Suggested alternate queries (if available) |
| Verified-only off, zero results | Same as above — do not suggest turning off verification |
| New market, no supply | "Verified creators are coming soon. Set your location to be notified." | **Primary button** "Set location" |

Log zero-result queries for supply planning per [marketplace mechanics](../../product/marketplace-mechanics.md#liquidity).

---

## Permissions

| Capability | Guest | Authenticated |
|------------|-------|---------------|
| Search and filter | ✓ | ✓ |
| View results | ✓ | ✓ |
| Save recent searches | Session only | Persisted to account |
| "Nearest" sort | Requires geolocation or account address | Uses saved address |

Default `verified_only=true` for all users. Unverified results (when toggled off) display with distinct non-badge styling — never impersonate verification.

---

## Analytics

| Event | Properties |
|-------|------------|
| `page_view` | `page: search`, `q`, active filters |
| `search_executed` | `q`, `filters[]`, `result_count`, `latency_ms` |
| `search_filter_applied` | `filter_type`, `filter_value` |
| `search_filter_cleared` | `filter_type` or `all` |
| `search_sort_changed` | `sort` |
| `search_result_clicked` | `result_type: creator | item`, `position`, `creator_id`, `item_id` |
| `search_zero_results` | `q`, `filters[]` |
| `search_load_more` | `page`, `results_loaded` |

---

## Accessibility

- **Search input:** `role="search"`, `aria-label="Search verified creators and menu items"`
- **Filter bar:** `aria-label="Search filters"`; each chip has `aria-label="Remove [filter] filter"`
- **Verified only toggle:** `aria-describedby` explaining what verification means
- **Results count:** `aria-live="polite"` region announces "24 results found" on update
- **Sort dropdown:** Labeled `aria-label="Sort results"`
- **Mobile filter sheet:** Focus trap; return focus to Filters button on close
- **Result cards:** Heading level 2 for creator name; verification status in accessible name
- **Pagination:** "Load more" announces new result count to screen readers

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | `{query} — Search verified food creators | Marketplate` (dynamic) |
| `<meta name="description">` | Search results for verified local food creators matching your criteria. |
| Canonical | Self-referencing with query params |
| `robots` | `noindex` on filtered/paginated variants to avoid duplicate content; index base `/search` only if editorial |

Dynamic search result pages are generally `noindex, follow`.

---

## Future Improvements

- Search within menu items as default blended view
- Spell correction and synonym mapping ("gf" → gluten-free)
- Saved searches with notification when new creators match
- Voice search on mobile
- Map view toggle for food truck results
- Faceted item-level filters (price range, lead time)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/search` | GET | Primary search; params: `q`, `cuisine[]`, `dietary[]`, `fulfillment`, `verified_only`, `lat`, `lng`, `sort`, `page`, `limit` |
| `/api/v1/search/suggest` | GET | Typeahead; params: `q`, `limit` |
| `/api/v1/search/facets` | GET | Available filter counts for current query (optional v1) |

Response shape per result:
```json
{
  "type": "creator | menu_item",
  "creator": { "id", "slug", "name", "avatar_url", "verification", "rating", "fulfillment_types", "distance_km" },
  "menu_item": { "id", "name", "price", "photo_url", "dietary_tags" },
  "relevance_score": 0.92
}
```

Ranking must follow [marketplace mechanics](../../product/marketplace-mechanics.md#ranking-principles): verification first, then relevance, quality, proximity, personalization.

---

## Related Pages

- [Home](home.md) — Discovery landing and search entry
- [Browse](browse.md) — Curated collections without query intent
- [Creator Storefront](creator-storefront.md) — Creator conversion from results
- [Menu Item Detail](menu-item-detail.md) — Item conversion from results
- [Account Settings](account-settings.md) — Saved address for nearest sort
- [Help](help.md) — "How verification works" from filter tooltip
