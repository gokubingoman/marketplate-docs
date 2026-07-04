# API Overview

> REST API conventions for Marketplate — see [Founding Constitution](../../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Engineering

---

## Purpose

This document defines platform-wide API conventions for all Marketplate clients (customer marketplace, Creator OS, Admin console) and third-party integrations. Individual endpoint catalogs live in [Customer API](customer-api.md), [Creator API](creator-api.md), and [Admin API](admin-api.md).

Governing product rules: [Marketplace Mechanics](../../product/marketplace-mechanics.md). Page-level requirements: [`pages/`](../../pages/).

---

## Base URL & Versioning

| Environment | Base URL |
|-------------|----------|
| Production | `https://api.marketplate.com/api/v1` |
| Staging | `https://api.staging.marketplate.com/api/v1` |
| Local | `http://localhost:8080/api/v1` |

### Versioning strategy

- **URL path versioning:** All public endpoints are prefixed with `/api/v1`.
- **Breaking changes** require a new major version (`/api/v2`). Non-breaking additive changes (new optional fields, new endpoints) ship within v1.
- **Deprecation:** Deprecated endpoints return `Deprecation: true` and `Sunset: <RFC 7231 date>` headers for a minimum 90-day notice period.
- **Client contract:** Mobile and web clients pin to a minimum supported API version at build time; server maintains backward compatibility within the pinned major version.

`TODO(decision):` Whether to expose a public OpenAPI spec and developer portal for partner integrations.

---

## Protocol & Format

| Rule | Convention |
|------|------------|
| **Protocol** | HTTPS only in non-local environments |
| **Request body** | JSON (`Content-Type: application/json`) |
| **Response body** | JSON (`Content-Type: application/json; charset=utf-8`) |
| **Timestamps** | ISO 8601 UTC (`2026-07-03T18:30:00Z`) |
| **Money** | Integer minor units (cents) + ISO 4217 currency code |
| **IDs** | UUID v4 for internal IDs; public slugs for creator storefronts and menu items |
| **Null vs omit** | Explicit `null` for cleared optional fields on PATCH; omit fields not requested via sparse fieldsets (future) |

### Request headers

| Header | Required | Purpose |
|--------|----------|---------|
| `Authorization` | Conditional | Bearer token or session cookie — see [Authentication](authentication.md) |
| `Content-Type` | POST/PATCH/PUT | `application/json` |
| `Accept` | Recommended | `application/json` |
| `Idempotency-Key` | Conditional | Required on payment and order placement — see below |
| `X-Request-Id` | Optional | Client-generated correlation ID; echoed in response |
| `X-Client-Surface` | Recommended | `customer` · `creator` · `admin` — analytics and rate-limit tiers |

### Response envelope

Successful list responses:

```json
{
  "data": [ ... ],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 142,
    "has_more": true
  }
}
```

Successful single-resource responses:

```json
{
  "data": { ... }
}
```

---

## Pagination

Cursor-based pagination is preferred for real-time lists (orders, messages). Offset pagination is acceptable for stable admin tables.

### Offset pagination

| Param | Default | Max | Description |
|-------|---------|-----|-------------|
| `page` | `1` | — | 1-indexed page number |
| `limit` | `20` | `100` | Items per page |

Response `meta`: `{ page, limit, total, has_more }`.

### Cursor pagination

| Param | Description |
|-------|-------------|
| `cursor` | Opaque token from previous response |
| `limit` | Items per page (default 20, max 100) |

Response `meta`: `{ next_cursor, has_more, limit }`.

Used by: order queues, message threads, audit feeds, search results.

---

## Error Format

All errors use a consistent JSON structure:

```json
{
  "error": {
    "code": "cart.validation_failed",
    "message": "Your cart cannot proceed to checkout.",
    "details": [
      {
        "field": "lines[0].quantity",
        "code": "item_unavailable",
        "message": "Sourdough loaf is sold out."
      }
    ],
    "request_id": "req_abc123"
  }
}
```

### HTTP status codes

| Status | Usage |
|--------|-------|
| `200` | Success (GET, PATCH, PUT) |
| `201` | Resource created |
| `204` | Success with no body (DELETE) |
| `400` | Malformed request, validation failure |
| `401` | Missing or invalid authentication |
| `403` | Authenticated but insufficient permissions |
| `404` | Resource not found (or not visible to caller) |
| `409` | Conflict — concurrent edit, idempotency replay mismatch, invalid state transition |
| `422` | Semantic validation failure (business rules) |
| `429` | Rate limit exceeded |
| `500` | Unexpected server error |
| `503` | Service unavailable — retry with backoff |

### Error code naming

Dot-separated namespace: `{domain}.{reason}` — e.g. `checkout.capacity_exceeded`, `order.invalid_transition`, `verification.checklist_incomplete`.

Never expose internal stack traces or PII in error messages.

---

## Rate Limits

Rate limits protect platform integrity and comply with abuse prevention requirements per [Marketplace Mechanics — Audit everything](../../product/marketplace-mechanics.md#marketplace-model-overview).

| Tier | Scope | Limit | Window |
|------|-------|-------|--------|
| **Anonymous** | Per IP | 120 requests | 1 minute |
| **Authenticated customer** | Per user | 300 requests | 1 minute |
| **Creator** | Per creator account | 600 requests | 1 minute |
| **Admin** | Per operator | 1000 requests | 1 minute |
| **Auth endpoints** | Per IP + email | 10 attempts | 15 minutes |
| **Search suggest** | Per IP | 60 requests | 1 minute |

### Rate limit headers

```
X-RateLimit-Limit: 300
X-RateLimit-Remaining: 287
X-RateLimit-Reset: 1720035600
```

On `429`:

```json
{
  "error": {
    "code": "rate_limit.exceeded",
    "message": "Too many requests. Retry after 42 seconds.",
    "retry_after_seconds": 42
  }
}
```

---

## Idempotency Keys

Required on endpoints that create financial or order side effects:

| Endpoint | Scope |
|----------|-------|
| `POST /api/v1/checkout/orders` | Order creation + payment authorization |
| `POST /api/v1/admin/payments/refund` | Refund execution |
| `POST /api/v1/creator/payouts/account/onboard` | Connect onboarding session |

### Behavior

1. Client sends `Idempotency-Key: <uuid>` header.
2. Server stores `(key, endpoint, user_id, response_hash)` for **24 hours**.
3. Duplicate request with same key returns **original response** with `Idempotent-Replayed: true` header.
4. Same key with **different body** returns `409` with `idempotency.key_body_mismatch`.

---

## Real-Time Channels

WebSocket and SSE endpoints supplement REST for live updates:

| Channel | Audience | Events |
|---------|----------|--------|
| `customer.{user_id}.orders.{order_id}` | Customer | Order status changes |
| `creator.{creator_id}.orders` | Creator | New orders, status updates |
| `creator.{creator_id}.messages` | Creator | Inbound messages |
| `creator.{creator_id}.reviews` | Creator | New reviews |

Connection requires valid session/JWT. Channels are scoped to authenticated principal — no cross-tenant subscription.

---

## Cross-Cutting Concerns

### Trust enforcement

- Discovery endpoints return **verified creators only** for featured modules — [Ranking principles](../../product/marketplace-mechanics.md#ranking-principles).
- Unverified creators cannot accept paid orders — enforced at checkout and order service layer.
- Admin actions require immutable audit trails — [Audit everything](../../product/marketplace-mechanics.md#marketplace-model-overview).

### File uploads

Document and photo uploads use presigned URL flow:

1. `POST /api/v1/.../documents` → returns `{ upload_url, document_id, expires_at }`
2. Client PUTs file directly to object storage
3. Client confirms upload → server validates and queues for review

Max file size: 10 MB (images), 25 MB (PDF documents). Allowed MIME types enforced server-side.

### Geocoding

Address autocomplete and zone validation use internal geocoding service. Debounced client calls (300ms). Coordinates stored on `CustomerAddress` and `Kitchen` entities — see [Core Entities](../data/core-entities.md).

---

## Open Decisions

| Decision | API impact |
|----------|------------|
| `TODO(decision):` Auth provider | Session vs JWT implementation, OAuth social login endpoints |
| `TODO(decision):` Stripe Connect model | Payment method storage, Connect account webhooks, payout API shape |
| `TODO(decision):` Geographic compliance rules | Jurisdiction-scoped validation rules, locale headers |

---

## Related Documents

- [Authentication](authentication.md)
- [Customer API](customer-api.md)
- [Creator API](creator-api.md)
- [Admin API](admin-api.md)
- [Data Model Overview](../data/data-model-overview.md)
- [Service Catalog](../service-catalog.md)
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Information Architecture](../../pages/information-architecture.md)
