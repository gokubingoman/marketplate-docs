# Creator Reviews (Reputation Management)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/dashboard/reviews`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Reviews page lets creators **read customer feedback, respond publicly, and monitor reputation** — star ratings, written reviews, and aggregate scores that appear on their [Creator Storefront](../customer/creator-storefront.md). Responding professionally turns feedback into trust signal.

Marketplate does not allow pay-to-remove reviews per platform invariants in [Platform Settings](../admin/platform-settings.md). Creators can flag policy violations for [Moderation Queue](../admin/moderation-queue.md) review — not delete legitimate criticism.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| See all reviews with ratings and order context | Transparent reputation builds marketplace trust |
| Respond to reviews thoughtfully and quickly | Improve customer retention and storefront conversion |
| Monitor rating trends over time | Early warning for quality or fulfillment issues |
| Flag abusive or fraudulent reviews | Protect creators without suppressing honest feedback |

**Primary action on this screen:** Respond to the most recent unanswered review — or read flagged/negative reviews requiring attention.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Baker](../../product/personas.md#baker) | Visual product quality feedback |
| **Secondary** | [Independent Chef](../../product/personas.md#independent-chef) | Personal relationship with reviewers |
| **Secondary** | [Meal Prep Business](../../product/personas.md#meal-prep-business) | Batch quality consistency signals |
| **Anti-persona** | Customers writing reviews | Review submission happens post-order on customer surface |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Sidebar nav | "Reviews" — badge for new unanswered |
| [Dashboard](./dashboard.md) | Rating stat card → Reviews |
| [Analytics](./analytics.md) | Rating trend link |
| Email | "You received a new 5-star review" |
| [Storefront Settings](./storefront-settings.md) | Reviews count on preview |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Order Detail](./order-detail.md) | Order link on review row |
| [Messages](./messages.md) | Follow up privately after public response (manual) |
| [Dashboard](./dashboard.md) | Sidebar home |
| [Creator Storefront](../customer/creator-storefront.md) | Preview public reviews tab |

### Breadcrumbs

`Dashboard → Reviews`

---

## Layout

Summary header + filterable review list. Response composer inline on expand.

```
┌─────────────────────────────────────────────────────────────────┐
│ Dashboard → Reviews                                             │
├─────────────────────────────────────────────────────────────────┤
│ ┌──────────┐  4.8 average · 124 reviews · 96% recommend       │
│ │ ★★★★★    │  [sparkline: 90-day rating trend]                │
│ └──────────┘                                                    │
│ [ All ] [ Needs response (2) ] [ 1–2 stars ] [ Flagged ]        │
├─────────────────────────────────────────────────────────────────┤
│ ┌ Review card ─────────────────────────────────────────────────┐│
│ │ ★★★★★ · Sarah M. · Jul 1, 2026 · Order #1042                 ││
│ │ "Best sourdough in the neighborhood!"                        ││
│ │ Your response: "Thank you Sarah! ..." · Jul 2                ││
│ └──────────────────────────────────────────────────────────────┘│
│ ┌ Review card ─────────────────────────────────────────────────┐│
│ │ ★★☆☆☆ · James L. · Jun 28 · Order #1038                      ││
│ │ "Pickup window was confusing."                                 ││
│ │ [ Write response... ]                    [ Flag review ]     ││
│ └──────────────────────────────────────────────────────────────┘│
│ [ Load more ]                                                   │
└─────────────────────────────────────────────────────────────────┘
```

**Content hierarchy:**

1. Aggregate rating summary + trend
2. Filter tabs
3. Review list — newest first by default
4. Inline response composer on expand

---

## Components

| Component | Usage on this page | DS reference |
|-----------|-------------------|--------------|
| **Sidebar nav** | Creator OS navigation; new review badge | [Navigation — Sidebar](../../design-system/components-overview.md#navigation) |
| **Dashboard stat card** | Average rating, count | [Cards — Dashboard stat](../../design-system/components-overview.md#cards) |
| **Sparkline / chart** | Rating trend | [Charts](../../design-system/components-overview.md#charts) |
| **Segmented control** | Filter tabs | [Segmented control](../../design-system/components-overview.md#segmented-control) |
| **Review card** | Rating, text, customer, order link | [Cards](../../design-system/components-overview.md#cards) |
| **Star rating display** | Read-only stars | [Rating](../../design-system/components-overview.md#rating) |
| **Textarea** | Response composer | [Inputs — Textarea](../../design-system/components-overview.md#inputs) |
| **Primary button** | Post response | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | Flag review, view order | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Modal** | Flag review reason selection | [Modals](../../design-system/components-overview.md#modals) |
| **Avatar** | Customer initial | [Avatars](../../design-system/components-overview.md#avatars) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Filter tabs** | Client or server filter; update URL `?filter=needs_response` |
| **Review expand** | Show full text, order items summary, response composer if none |
| **Post response** | One public response per review; editable for 24h then locked — `TODO(decision):` |
| **Flag review** | Modal: reason (spam, harassment, not a customer, etc.); submits to moderation |
| **Order link** | Opens [Order Detail](./order-detail.md) |
| **Sort** | Default newest; optional highest/lowest rating |
| **Load more** | Paginate list |
| **Trend chart** | Read-only; tap data point shows reviews in that week (future) |

**Response guidelines:** Inline tip linking to help — professional tone; no incentives for reviews (policy).

---

## Animations

| Trigger | Motion | Duration |
|---------|--------|----------|
| Page load | Summary card fade-up | 200ms |
| New review (realtime) | List item slide in | 300ms |
| Response posted | Success check on card | 200ms |
| Filter change | List crossfade | 200ms |

Respect `prefers-reduced-motion`: instant list updates.

---

## Responsive Behaviour

| Breakpoint | Layout changes |
|------------|----------------|
| **Mobile (320–767px)** | Full-width cards; composer below review text |
| **Tablet (768–1023px)** | Same list layout |
| **Desktop (1024px+)** | Optional max-width list centered for readability |

Star ratings and text never truncated without "Read more" expand.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| **Summary** | Skeleton rating + count |
| **Review list** | Skeleton cards (5) |
| **Post response** | Button spinner |
| **Flag submit** | Modal button loading |

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| **Reviews fetch failed** | "Reviews couldn't load" | Retry |
| **Response failed** | "Response couldn't post. Try again." | Retry |
| **Response too long** | "Keep responses under 500 characters" | Trim text |
| **Flag failed** | "Couldn't submit flag" | Retry |
| **Review removed by moderation** | Card shows "Review removed per policy" | — |
| **Edit window expired** | "Responses can't be edited after 24 hours" | — |

---

## Empty States

| Scenario | Display | Primary action |
|----------|---------|----------------|
| **No reviews yet** | "Reviews appear after customers complete orders" | [Share storefront] → [Storefront Settings](./storefront-settings.md) |
| **Needs response empty** | "All reviews have responses" | — |
| **Filter no results** | "No reviews match this filter" | Clear filter |

---

## Permissions

| Role | Access |
|------|--------|
| **Creator owner** | Read all, respond, flag |
| **Creator staff — orders** | Read reviews; respond if enabled in team settings — `TODO(decision):` |
| **Creator staff — kitchen** | Read-only |
| **Unverified creator** | Empty state — reviews enabled after first completed orders |
| **Suspended creator** | Read-only; cannot respond |

Only verified purchase reviews displayed — verified buyer badge on customer surface.

---

## Analytics

| Event | Properties | Purpose |
|-------|------------|---------|
| `creator_reviews_viewed` | `average_rating`, `total_count`, `needs_response_count` | Engagement |
| `creator_reviews_filter_changed` | `filter` | Concern patterns |
| `creator_reviews_response_posted` | `review_id`, `rating`, `response_time_hours` | Response SLA |
| `creator_reviews_flagged` | `review_id`, `reason` | Moderation volume |
| `creator_reviews_order_clicked` | `order_id` | Context usage |

Funnel: negative review → creator response → no escalation to dispute.

---

## Accessibility

| Requirement | Implementation |
|-------------|----------------|
| **Page title** | `<h1>Reviews</h1>` |
| **Star ratings** | Text alternative: "4 out of 5 stars" |
| **Review list** | `<ul role="list">`; each review is `<li>` |
| **Composer** | `aria-label="Your response to review from {customer}"` |
| **Filters** | Tab semantics with `aria-selected` |
| **Flag modal** | Focus trap; reason radio group labeled |

---

## SEO

Not applicable — authenticated creator surface. Public reviews indexed on [Creator Storefront](../customer/creator-storefront.md) `#reviews` anchor.

---

## Future Improvements

- Response templates for common thank-yous
- AI-suggested response drafts (human post only)
- Review request prompts after order (customer-side automation)
- Item-level reviews linked to [Catalog](./catalog.md)
- Sentiment tagging for ops insights
- Benchmark vs. category average

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `GET /api/v1/creator/reviews` | GET | Paginated list; `?filter=needs_response` |
| `GET /api/v1/creator/reviews/summary` | GET | Average, count, trend series |
| `POST /api/v1/creator/reviews/{id}/response` | POST | `{ body }` public response |
| `PATCH /api/v1/creator/reviews/{id}/response` | PATCH | Edit within window |
| `POST /api/v1/creator/reviews/{id}/flag` | POST | `{ reason, details? }` |
| WebSocket `creator.{id}.reviews` | Subscribe | New review notification |

Reviews created by customer post-order flow — not on this page.

---

## Related Pages

- [Dashboard](./dashboard.md) — rating stat card
- [Analytics](./analytics.md) — rating trends correlation
- [Storefront Settings](./storefront-settings.md) — public presentation
- [Orders](./order-detail.md) — order context per review
- [Messages](./messages.md) — private follow-up
- Customer-facing: [Creator Storefront](../customer/creator-storefront.md)
- Admin: [Moderation Queue](../admin/moderation-queue.md) — flagged reviews
- Admin: [Creator Admin Detail](../admin/creator-admin-detail.md) — trust metrics
- Admin: [Platform Settings](../admin/platform-settings.md) — review policy invariants
