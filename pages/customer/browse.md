# Customer Browse

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Route:** `/browse` and `/browse/:collectionSlug`  
**Surface:** Customer marketplace  
**Phase:** 2  
**Status:** Draft  
**Last updated:** 2026-07-03

---

## Purpose

The Browse page is Marketplate's curated discovery surface for customers who want to explore without a specific search query. Collections group verified creators by cuisine, dietary focus, fulfillment model, seasonality, or editorial curation.

Browse complements [Search](search.md) by providing structured entry points — "Vegan meal prep," "Weekend bakery," "Food trucks near you" — while maintaining the same trust standards on every card.

---

## Goals

### User goals

- Explore food creators by category or themed collection
- Understand collection context (why these creators are grouped)
- Find creators matching a lifestyle or occasion (weeknight dinners, holiday treats)
- Transition smoothly to [Creator Storefront](creator-storefront.md) or refine via [Search](search.md)

### Business goals

- Merchandise verified supply into discoverable groups
- Drive exploration depth (collections viewed per session)
- Support editorial and algorithmic collections with integrity rules
- Surface supply gaps when collections are thin

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [End Customer (Trust-Seeking Buyer)](../../product/personas.md#end-customer-trust-seeking-buyer) | Exploratory discovery mode |
| **Secondary** | Gift or occasion shopper | Seasonal collections |
| **Anti-persona** | Power user with exact item in mind | Should use Search instead |

---

## Navigation

### Entry points

| Source | Context |
|--------|---------|
| [Home](home.md) collection cards | Deep-link to `/browse/:slug` |
| [Search](search.md) empty state | "Browse categories" |
| Top nav "Browse" (desktop) | Collection index at `/browse` |
| Marketing campaigns | Collection-specific landing URLs |

### Exit points

| Destination | Trigger |
|-------------|---------|
| [Creator Storefront](creator-storefront.md) | Creator card tap |
| [Search](search.md) | "Search in this collection" bar |
| [Browse](browse.md) (other collection) | Related collection chips |
| [Home](home.md) | Breadcrumb, logo |

### Breadcrumbs

`Home > Browse > [Collection Name]` on collection detail view.

---

## Layout

### Index view (`/browse`)

```
┌─────────────────────────────────────────────────────────────┐
│  Top nav bar                                                │
├─────────────────────────────────────────────────────────────┤
│  Page header — "Browse verified creators"                   │
│  Subhead — calm trust line                                  │
├─────────────────────────────────────────────────────────────┤
│  Collection grid                                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐        │
│  │  Photo       │  │  Photo       │  │  Photo       │        │
│  │  Title       │  │  Title       │  │  Title       │        │
│  │  Creator cnt │  │  Creator cnt │  │  Creator cnt │        │
│  └──────────────┘  └──────────────┘  └──────────────┘        │
├─────────────────────────────────────────────────────────────┤
│  Browse by dietary — horizontal chip row                    │
├─────────────────────────────────────────────────────────────┤
│  Browse by fulfillment — cards (Pickup, Delivery, etc.)   │
└─────────────────────────────────────────────────────────────┘
```

### Collection detail (`/browse/:slug`)

```
┌─────────────────────────────────────────────────────────────┐
│  Breadcrumbs                                                │
├─────────────────────────────────────────────────────────────┤
│  Collection hero — image, title, description, creator count │
│  Trust note — "All creators are verified"                   │
├─────────────────────────────────────────────────────────────┤
│  Search within collection — Search input (scoped)           │
├─────────────────────────────────────────────────────────────┤
│  Optional filter chips — dietary, fulfillment (pre-set)     │
├─────────────────────────────────────────────────────────────┤
│  Creator cards grid                                         │
├─────────────────────────────────────────────────────────────┤
│  Related collections — horizontal scroll                    │
└─────────────────────────────────────────────────────────────┘
```

### Grid

| View | Mobile | Tablet | Desktop |
|------|--------|--------|---------|
| Collection index | 1-col cards | 2-col | 3-col |
| Collection detail creators | 1-col list | 2-col | 3-col |

---

## Components

| Component | Usage |
|-----------|-------|
| **Breadcrumbs** | Collection detail wayfinding |
| **Search input** | Scoped search within collection |
| **Creator card** | Creator listings in collection |
| **Verification badge** | On every creator card |
| **Category badge** | Collection tags; cuisine labels |
| **Dietary badge** | Dietary-focused collections |
| **Creator avatar** | Card header |
| **Primary button** | Collection index hero CTA (if applicable) |
| **Ghost button** | Related collection navigation |
| **Checkbox** | Optional inline filters on collection detail |
| **Pagination** | Creator list pagination |
| **Segmented control** | Toggle "Creators" / "Menu items" (future — hide in v1) |

---

## Interactions

### Collection index

- Tap collection card → `/browse/:slug`
- Tap dietary chip → collection detail with dietary filter pre-applied
- Tap fulfillment card → collection detail filtered by fulfillment type

### Collection detail

- Creator card → [Creator Storefront](creator-storefront.md)
- Scoped search submit → filters creators within collection; updates URL `?q=`
- Related collection chip → navigate to sibling collection
- Filter chips toggle dietary/fulfillment within collection context

### Trust

- Collection hero displays: "All creators in this collection have completed identity and kitchen verification."
- Creators who lose verification status are removed from collection on next index refresh — never shown with stale badge

### Keyboard

- Collection cards are focusable links with visible focus ring
- Arrow keys navigate grid on desktop (roving tabindex pattern)

---

## Animations

| Interaction | Motion |
|-------------|--------|
| Collection index load | Cards fade-in stagger 50ms |
| Navigate to collection | Page transition fade 200ms |
| Filter chip toggle | Background color transition 150ms |
| Hero image load | Blur-up from low-res placeholder 300ms |

No parallax on collection hero. Respect `prefers-reduced-motion`.

---

## Responsive Behaviour

| Breakpoint | Adaptations |
|------------|-------------|
| **Mobile** | Full-width collection cards; hero image 16:9; sticky scoped search below hero |
| **Tablet** | 2-column grids; hero text overlay on image |
| **Desktop** | 3-column grids; hero side-by-side (image + text) |

Collection description never truncated on mobile — full text with comfortable line height.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| Collection index | 6 collection card skeletons |
| Collection detail hero | Image skeleton + title/text bars |
| Creator grid | Creator card skeletons matching expected count |
| Scoped search | Inline spinner in results area |

Collection metadata loads before creator list (hero first paint).

---

## Error States

| Scenario | UI | Recovery |
|----------|-----|----------|
| Collection not found (404) | "This collection doesn't exist or has been removed." | **Primary button** "Browse all" → `/browse` |
| Creator list API failure | Inline section error | **Secondary button** "Try again" |
| Collection empty (0 creators) | See Empty States | — |
| Image load failure | Neutral placeholder with cuisine icon | — |

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| Collection with 0 creators | "Creators are being added to this collection. Check back soon." | **Secondary button** "Browse all collections" |
| Scoped search zero results | "No creators in this collection match '[query]'." | **Ghost button** "Clear search" |
| Index has no collections (pre-launch) | "Collections are coming soon. Search for verified creators in the meantime." | **Primary button** "Search creators" → [Search](search.md) |

---

## Permissions

| Capability | Guest | Authenticated |
|------------|-------|---------------|
| View browse index | ✓ | ✓ |
| View collection detail | ✓ | ✓ |
| Scoped search | ✓ | ✓ |

All collections enforce minimum trust thresholds per [merchandising rules](../../product/marketplace-mechanics.md#merchandising-rules). Featured collections on [Home](home.md) use stricter thresholds than long-tail browse collections.

---

## Analytics

| Event | Properties |
|-------|------------|
| `page_view` | `page: browse | browse_collection`, `collection_slug` |
| `browse_collection_opened` | `slug`, `source: home | index | related` |
| `browse_creator_clicked` | `collection_slug`, `creator_id`, `position` |
| `browse_scoped_search` | `collection_slug`, `q`, `result_count` |
| `browse_filter_applied` | `collection_slug`, `filter` |
| `browse_related_collection_clicked` | `from_slug`, `to_slug` |

---

## Accessibility

- **Collection cards:** `aria-label="[Title], [N] verified creators"`
- **Hero image:** Descriptive `alt` — "[Collection name] — verified local food creators"
- **Breadcrumbs:** `nav` with `aria-label="Breadcrumb"`
- **Scoped search:** `aria-label="Search within [collection name]"`
- **Creator grid:** `ul` / `li` structure; heading hierarchy h1 (collection) → h2 (creator names)
- **Related collections:** Horizontal scroll announced with `aria-label="Related collections"`

---

## SEO

| Element | Value |
|---------|-------|
| Index `<title>` | Browse Verified Food Creators | Marketplate |
| Collection `<title>` | `{Collection Name} — Verified Local Food | Marketplate` |
| `<meta name="description">` | Dynamic per collection — include creator count and trust language |
| Canonical | `/browse/:slug` |
| Structured data | `ItemList` of creators with `name`, `url` (storefront) |

Collection pages are indexable — editorial content value for organic discovery.

---

## Future Improvements

- Personalized collection ordering based on order history
- "New in [collection]" badge for recently added creators
- Collection subscriptions — notify when new creators join
- Creator-submitted collection applications (ops-reviewed)
- Seasonal auto-rotating hero collections
- Blend menu item cards in collection detail for item-forward collections

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/browse/collections` | GET | Index — all active collections with `slug`, `title`, `description`, `image_url`, `creator_count`, `tags` |
| `/api/v1/browse/collections/:slug` | GET | Collection detail metadata |
| `/api/v1/browse/collections/:slug/creators` | GET | Paginated creators; params: `q`, `dietary[]`, `fulfillment`, `page`, `limit` |
| `/api/v1/browse/collections/:slug/related` | GET | Related collection slugs |

All creators in response must have `verification_status: verified`. Collections return `min_trust_tier` for ops auditing.

---

## Related Pages

- [Home](home.md) — Collection entry cards
- [Search](search.md) — Intent-driven discovery
- [Creator Storefront](creator-storefront.md) — Conversion destination
- [Menu Item Detail](menu-item-detail.md) — Item-level browse (future)
- [Help](help.md) — Collection curation FAQ
