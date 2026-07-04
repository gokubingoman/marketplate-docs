# Creator API

> Creator OS endpoints for catalog, orders, compliance, and business operations — see [API Overview](api-overview.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Engineering

---

## Purpose

Consolidated REST endpoint catalog for the Creator OS surface. Derived from [`pages/creator/`](../../pages/creator/), [`pages/auth/`](../../pages/auth/) onboarding flows, and cross-referenced with admin enforcement endpoints.

Product rules: [Marketplace Mechanics](../../product/marketplace-mechanics.md) — verified to sell, creator-owned relationship, audit everything.

---

## Authentication Summary

All Creator OS endpoints require authenticated creator context. See [Authentication — Creator scopes](authentication.md#creator-scopes).

Unverified creators access endpoints in **draft mode** — catalog and compliance writable; order acceptance blocked at payment layer.

Staff role restrictions apply per endpoint — revenue fields omitted for non-owner roles on analytics.

---

## Dashboard

Source: [Dashboard](../../pages/creator/dashboard.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/dashboard/summary` | GET | dashboard:read | Today orders, revenue, rating, pending counts |
| `/api/v1/creator/dashboard/action-items` | GET | dashboard:read | Prioritized task list with deep links |
| WebSocket/SSE `creator.{id}.orders` | Subscribe | orders:read | Realtime new order notifications |

SLA target: summary endpoint < 300ms p95.

Also consumes: `GET /api/v1/creator/orders?date=today&limit=5`, `GET /api/v1/creator/verification/status`, `GET /api/v1/creator/messages/unread-count`.

---

## Orders

Source: [Orders](../../pages/creator/orders.md), [Order Detail](../../pages/creator/order-detail.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/orders` | GET | orders:read | Paginated list; `status`, `fulfillment_type`, `date_from`, `date_to`, `allergen_flag`, `q` |
| `/api/v1/creator/orders/next-action` | GET | orders:read | Single order for primary action bar |
| `/api/v1/creator/orders/:id` | GET | orders:read | Full order detail |
| `/api/v1/creator/orders/:id/status` | PATCH | orders:write | Lifecycle transition |
| `/api/v1/creator/orders/:id/cancel` | POST | orders:write (owner) | Cancel with reason code |
| `/api/v1/creator/orders/:id/messages` | GET | messages:read | Thread preview |
| WebSocket `creator.{id}.orders` | Subscribe | orders:read | Realtime insert/update |

Order detail response includes `customer_allergen_declarations`, `item_allergens`, `checkout_allergen_ack`.

Status transitions validated server-side per [Order lifecycle](../../product/marketplace-mechanics.md#order-lifecycle):

```
confirmed → in_production → ready → in_fulfillment → completed
                                                      ↘ cancelled / refunded
```

---

## Catalog & Menu Items

Source: [Catalog](../../pages/creator/catalog.md), [Menu Item Editor](../../pages/creator/menu-item-editor.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/catalog` | GET | catalog:read | Sections + items with status, compliance flags |
| `/api/v1/creator/catalog/items` | GET | catalog:read | Flat list; `status`, `q`, `compliance_issue` |
| `/api/v1/creator/catalog/items` | POST | catalog:write | Create item |
| `/api/v1/creator/catalog/items/:id` | GET | catalog:read | Load item for edit |
| `/api/v1/creator/catalog/items/:id` | PATCH | catalog:write | Update item or quick fields |
| `/api/v1/creator/catalog/items/:id` | DELETE | catalog:write | Soft delete |
| `/api/v1/creator/catalog/items/:id/photos` | POST | catalog:write | Upload photos |
| `/api/v1/creator/catalog/items/:id/photos/:photoId` | DELETE | catalog:write | Remove photo |
| `/api/v1/creator/catalog/items/validate` | POST | catalog:write | Pre-publish compliance check |
| `/api/v1/creator/catalog/sections/order` | PUT | catalog:write | Section reorder |
| `/api/v1/creator/catalog/compliance-summary` | GET | catalog:read | Items needing attention count |

Every SKU must link to a verified production location — [Kitchen verification](../../product/marketplace-mechanics.md#kitchen-verification).

---

## Availability

Source: [Availability](../../pages/creator/availability.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/availability` | GET | availability:read | Weekly schedule, rules, exceptions |
| `/api/v1/creator/availability/schedule` | PUT | availability:write | Recurring weekly schedule |
| `/api/v1/creator/availability/rules` | PUT | availability:write | Cut-off, capacity, lead time, fulfillment types |
| `/api/v1/creator/availability/exceptions` | POST | availability:write | Closures, modified days, events |
| `/api/v1/creator/availability/exceptions/:id` | DELETE | availability:write | Remove exception |
| `/api/v1/creator/availability/conflicts` | GET | availability:read | Preview conflicts; `from`, `to` |
| `/api/v1/creator/availability/open-now` | PATCH | availability:write | Food truck session toggle |
| `/api/v1/creator/availability/public-preview` | GET | availability:read | Storefront-facing snapshot |

Capacity enforced at checkout — [Fulfillment invariants](../../product/marketplace-mechanics.md#fulfillment-invariants). GET SLA < 200ms p95.

---

## Compliance & Verification

Source: [Compliance](../../pages/creator/compliance.md), [Identity Verification](../../pages/auth/identity-verification.md), [Kitchen Verification](../../pages/auth/kitchen-verification.md), [Compliance Center](../../pages/auth/compliance-center.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/verification/status` | GET | compliance:read | Three-layer summary |
| `/api/v1/creators/me/verification/identity` | GET/PATCH | compliance:write | Identity draft and status |
| `/api/v1/creators/me/verification/identity/submit` | POST | compliance:write | Submit for human review |
| `/api/v1/creators/me/verification/identity/documents` | POST | compliance:write | Upload document |
| `/api/v1/creators/me/verification/identity/documents/:id` | DELETE | compliance:write | Remove draft document |
| `/api/v1/creators/me/verification/kitchen` | GET/PATCH | compliance:write | Kitchen draft and status |
| `/api/v1/creators/me/verification/kitchen/submit` | POST | compliance:write | Submit for review |
| `/api/v1/creators/me/verification/kitchen/documents` | POST | compliance:write | Upload artifacts |
| `/api/v1/creators/me/compliance` | GET | compliance:read | Checklist, statuses, jurisdiction |
| `/api/v1/creators/me/compliance/items/:type` | PATCH | compliance:write | Save draft |
| `/api/v1/creators/me/compliance/items/:type/submit` | POST | compliance:write | Submit for review |
| `/api/v1/creators/me/compliance/items/:type/documents` | POST | compliance:write | Upload |
| `/api/v1/creator/compliance/documents` | GET | compliance:read | Document list with expiry |
| `/api/v1/creator/compliance/documents` | POST | compliance:write | Upload document |
| `/api/v1/creator/compliance/documents/:id` | GET | compliance:read | Preview URL |
| `/api/v1/creator/compliance/submit-review` | POST | compliance:write | Batch submit |
| `/api/v1/creator/compliance/jurisdiction-rules` | GET | compliance:read | Applicable rules summary |
| `/api/v1/creator/compliance/category-rules` | GET | compliance:read | Jurisdiction restrictions |
| `/api/v1/creator/compliance/next-action` | GET | compliance:read | Primary action card |
| `/api/v1/creator/compliance/eligibility` | GET | compliance:read | Allowed/prohibited categories |
| `/api/v1/creator/kitchens` | GET | compliance:read | Verified production locations |
| `/api/v1/creator/kitchens/:id` | PATCH | compliance:write | Update kitchen artifacts |
| `/api/v1/kitchens/search` | GET | compliance:read | Search commercial kitchens / commissaries |
| `/api/v1/compliance/rules` | GET | Optional | Jurisdiction rule templates |
| `/api/v1/meta/kitchen-types` | GET | Optional | Kitchen types + jurisdiction rules |

**Status enum:** `not_started | draft | in_review | needs_information | approved | rejected`

Human review queue is admin API — no auto-approval per [Human approval on high stakes](../../product/marketplace-mechanics.md#marketplace-model-overview).

`TODO(decision):` Geographic compliance rules determine jurisdiction template library.

---

## Storefront Settings

Source: [Storefront Settings](../../pages/creator/storefront-settings.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/storefront` | GET | storefront:read | Current settings + completeness |
| `/api/v1/creator/storefront` | PATCH | storefront:write | Save profile fields |
| `/api/v1/creator/storefront/photos` | POST | storefront:write | Upload photo |
| `/api/v1/creator/storefront/photos/:id` | DELETE | storefront:write | Remove gallery image |
| `/api/v1/creator/storefront/slug/check` | GET | storefront:write | Slug availability |
| `/api/v1/creator/storefront/preview` | GET | storefront:read | Render payload for preview |

Public storefront: `GET /api/v1/creators/:slug` — see [Customer API](customer-api.md).

---

## Messages

Source: [Messages](../../pages/creator/messages.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/messages/threads` | GET | messages:read | Thread list with preview, unread |
| `/api/v1/creator/messages/threads/:id` | GET | messages:read | Messages paginated; `before`, `limit` |
| `/api/v1/creator/messages/threads/:id` | POST | messages:write | Send message |
| `/api/v1/creator/messages/threads/:id/read` | PATCH | messages:write | Mark thread read |
| `/api/v1/creator/messages/unread-count` | GET | messages:read | Badge count |
| `/api/v1/creator/messages/quick-replies` | GET | messages:read | Template list |
| WebSocket `creator.{id}.messages` | Subscribe | messages:read | Realtime inbound |

Messages immutable after send — no edit/delete in v1 (audit requirement).

---

## Reviews

Source: [Reviews](../../pages/creator/reviews.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/reviews` | GET | reviews:read | Paginated list; `filter=needs_response` |
| `/api/v1/creator/reviews/summary` | GET | reviews:read | Average, count, trend series |
| `/api/v1/creator/reviews/:id/response` | POST | reviews:write | Public response |
| `/api/v1/creator/reviews/:id/response` | PATCH | reviews:write | Edit within window |
| `/api/v1/creator/reviews/:id/flag` | POST | reviews:write | Flag for moderation |
| WebSocket `creator.{id}.reviews` | Subscribe | reviews:read | New review notification |

Reviews created by customer post-order flow — [Verified purchase only](../../product/marketplace-mechanics.md#reviews--community).

---

## Analytics

Source: [Analytics](../../pages/creator/analytics.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/analytics/summary` | GET | analytics:read | KPI cards with deltas |
| `/api/v1/creator/analytics/revenue` | GET | analytics:read | Time series; `range`, `granularity` |
| `/api/v1/creator/analytics/top-items` | GET | analytics:read | Ranked items; `range`, `limit` |
| `/api/v1/creator/analytics/customers` | GET | analytics:read | New vs repeat breakdown |
| `/api/v1/creator/analytics/fulfillment` | GET | analytics:read | On-time rate, avg prep time |
| `/api/v1/creator/analytics/export` | GET | analytics:read | CSV download |

Cached 15 minutes. Revenue fields omitted for non-owner staff.

---

## Payouts

Source: [Payouts](../../pages/creator/payouts.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/creator/payouts/summary` | GET | payouts:read (owner) | Balance, pending, holds, next payout |
| `/api/v1/creator/payouts/period` | GET | payouts:read | Current period breakdown |
| `/api/v1/creator/payouts/history` | GET | payouts:read | Paginated transfers |
| `/api/v1/creator/payouts/history/:id` | GET | payouts:read | Line items |
| `/api/v1/creator/payouts/account-link` | GET | payouts:read | Payment provider dashboard URL |
| `/api/v1/creator/payouts/account/onboard` | POST | payouts:write | Start Connect onboarding |
| `/api/v1/creator/payouts/export` | GET | payouts:read | CSV history |

Holds sync from compliance status and open disputes — exposed in `holds[]` with reason codes.

`TODO(decision):` Stripe Connect model — Standard vs Express accounts, payout schedule, fee structure.

---

## Onboarding

Source: [Creator Signup](../../pages/auth/creator-signup.md)

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/auth/signup` | POST | Create account with `account_type: "creator"` |
| `/api/v1/creators/onboarding` | GET | Onboarding progress after signup |
| `/api/v1/meta/business-types` | GET | Business type enum |

Creates audit event: `creator.account.created`.

---

## Service Ownership

| Domain | Primary service |
|--------|-----------------|
| Dashboard, orders | [Order Service](../services/order-service.md) |
| Catalog, availability, storefront | [Catalog Service](../services/catalog-service.md) |
| Verification, compliance, reviews | [Trust Service](../services/trust-service.md) |
| Payouts | [Payment Service](../services/payment-service.md) |
| Messages, notifications | [Notification Service](../services/notification-service.md) |
| Analytics | Order + Payment + Discovery (read models) |
| Auth, staff roles | [Identity Service](../services/identity-service.md) |

---

## Related Documents

- [API Overview](api-overview.md)
- [Authentication](authentication.md)
- [Customer API](customer-api.md)
- [Admin API](admin-api.md)
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Creator Onboarding Flow](../../pages/flows/creator-onboarding-flow.md)
- [Order Fulfillment Flow](../../pages/flows/order-fulfillment-flow.md)
