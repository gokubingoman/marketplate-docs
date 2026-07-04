# Customer API

> Discovery, commerce, and account endpoints for the Customer Marketplace — see [API Overview](api-overview.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Engineering

---

## Purpose

Consolidated REST endpoint catalog for the Customer Marketplace surface. Endpoints are derived from page specs in [`pages/customer/`](../../pages/customer/) and auth flows in [`pages/auth/`](../../pages/auth/).

Product rules: [Marketplace Mechanics](../../product/marketplace-mechanics.md) — trust transparency, single-creator cart, verified-only discovery.

---

## Authentication Summary

| Endpoint group | Anonymous | Customer auth |
|----------------|:---------:|:-------------:|
| Discovery (home, search, browse, storefront, items) | ✓ | ✓ |
| Cart | ✓ (session) | ✓ |
| Checkout, orders, account | ✗ | ✓ |
| Help (read) | ✓ | ✓ |
| Support tickets | ✓ | ✓ (order-linked) |

See [Authentication](authentication.md) for session details.

---

## Discovery & Search

Source: [Home](../../pages/customer/home.md), [Search](../../pages/customer/search.md), [Browse](../../pages/customer/browse.md)

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/v1/discovery/featured` | GET | Optional | Featured verified creators; `lat`, `lng`, `limit` |
| `/api/v1/discovery/collections` | GET | Optional | Collection cards for home |
| `/api/v1/discovery/nearby` | GET | Optional | Location-aware creators; `lat`, `lng`, `radius_km` |
| `/api/v1/search` | GET | Optional | Primary search; `q`, `cuisine[]`, `dietary[]`, `fulfillment`, `verified_only`, `lat`, `lng`, `sort`, `page`, `limit` |
| `/api/v1/search/suggest` | GET | Optional | Typeahead; `q`, `limit` |
| `/api/v1/search/facets` | GET | Optional | Filter counts for current query (v1 optional) |
| `/api/v1/browse/collections` | GET | Optional | All active collections |
| `/api/v1/browse/collections/:slug` | GET | Optional | Collection metadata |
| `/api/v1/browse/collections/:slug/creators` | GET | Optional | Paginated creators in collection |
| `/api/v1/browse/collections/:slug/related` | GET | Optional | Related collection slugs |

### Search result shape

```json
{
  "data": [{
    "type": "creator",
    "creator": {
      "id": "uuid",
      "slug": "maria-kitchen",
      "name": "Maria's Kitchen",
      "avatar_url": "https://...",
      "verification": { "identity": true, "kitchen": true },
      "rating": { "average": 4.8, "count": 124 },
      "fulfillment_types": ["pickup", "delivery"],
      "distance_km": 2.3
    },
    "relevance_score": 0.92
  }],
  "meta": { "page": 1, "limit": 20, "total": 48, "has_more": true }
}
```

Ranking follows [Marketplace Mechanics — Ranking principles](../../product/marketplace-mechanics.md#ranking-principles).

---

## Storefront & Menu

Source: [Creator Storefront](../../pages/customer/creator-storefront.md), [Menu Item Detail](../../pages/customer/menu-item-detail.md)

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/v1/creators/:slug` | GET | Optional | Profile, verification, fulfillment, policies |
| `/api/v1/creators/:slug/menu` | GET | Optional | Menu sections and items |
| `/api/v1/creators/:slug/reviews` | GET | Optional | Paginated reviews; `sort`, `page`, `limit` |
| `/api/v1/creators/:slug/items/:itemSlug` | GET | Optional | Full item detail |
| `/api/v1/storefronts/:slug` | GET | Optional | Public storefront render payload (creator settings preview) |

Creator response must include `verification.identity`, `verification.kitchen`, `verification.compliance_summary`, `fulfillment.types[]`, and `production_location.display`.

Item response fields: `id`, `slug`, `name`, `description`, `photos[]`, `price`, `variants[]`, `addons[]`, `ingredients[]`, `allergens[]`, `dietary_tags[]`, `lead_time_hours`, `availability_status`, `max_quantity`, `creator`, `section_name`.

---

## Cart

Source: [Cart](../../pages/customer/cart.md)

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/v1/cart` | GET | Session/customer | Full cart with pricing and validation |
| `/api/v1/cart/items` | POST | Session/customer | Add item; `item_id`, `quantity`, `variants`, `addons`, `special_instructions` |
| `/api/v1/cart/items/:lineId` | PATCH | Session/customer | Update quantity, variants |
| `/api/v1/cart/items/:lineId` | DELETE | Session/customer | Remove line |
| `/api/v1/cart/validate` | POST | Session/customer | Pre-checkout validation |
| `/api/v1/cart/reorder` | POST | Customer | Populate from order ID |

### Cart response

```json
{
  "data": {
    "id": "uuid",
    "creator": {
      "id": "uuid", "slug": "...", "name": "...",
      "verification": {}, "minimum_order": 2500,
      "accepting_orders": true
    },
    "lines": [{
      "id": "uuid", "item_id": "uuid", "quantity": 2,
      "unit_price": 1200, "line_total": 2400,
      "allergens": ["nuts"], "availability_status": "available"
    }],
    "pricing": {
      "subtotal": 2400, "service_fee": 200,
      "tax_estimate": 208, "total": 2808
    },
    "validation": {
      "errors": [], "warnings": [],
      "minimum_order_progress": { "current": 2400, "required": 2500 }
    }
  }
}
```

**Invariant:** Single-creator cart enforced — adding from different creator triggers replace-cart flow on client; server returns `409 cart.creator_conflict` if not handled.

---

## Checkout

Source: [Checkout](../../pages/customer/checkout.md)

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/v1/checkout/session` | GET | Customer | Restore checkout state |
| `/api/v1/checkout/session` | PATCH | Customer | Save step progress (fulfillment, contact) |
| `/api/v1/checkout/fulfillment-options` | GET | Customer | Available windows; `creator_id`, `cart_id` |
| `/api/v1/checkout/validate-delivery` | POST | Customer | Address zone validation |
| `/api/v1/checkout/orders` | POST | Customer | Place order (**Idempotency-Key required**) |
| `/api/v1/customers/me/payment-methods` | GET | Customer | Saved payment methods |

### Place order request

```json
{
  "cart_id": "uuid",
  "fulfillment": {
    "type": "pickup",
    "window_id": "uuid"
  },
  "contact": {
    "name": "Jane Doe",
    "phone": "+15551234567",
    "email": "jane@example.com"
  },
  "payment_method_id": "pm_xxx",
  "acknowledgments": {
    "cancellation_policy": true,
    "allergens": true
  },
  "order_notes": "Please leave at door",
  "allergy_restatement": "Severe tree nut allergy"
}
```

Response: `{ order_id, confirmation_url, payment_status }`.

Payment capture timing varies by fulfillment model — [Marketplace Mechanics — Payment model](../../product/marketplace-mechanics.md#payment-model).

`TODO(decision):` Stripe Connect model determines payment method tokenization and authorization flow.

---

## Orders

Source: [Order Confirmation](../../pages/customer/order-confirmation.md), [Order Detail](../../pages/customer/order-detail.md), [Order History](../../pages/customer/order-history.md)

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/v1/customers/me/orders` | GET | Customer | Paginated list; `status`, `page`, `limit` |
| `/api/v1/customers/me/orders/active` | GET | Customer | Active orders only |
| `/api/v1/customers/me/orders/recent-creators` | GET | Customer | Order-again row (home) |
| `/api/v1/customers/me/orders/:orderId` | GET | Customer | Full order detail |
| `/api/v1/customers/me/orders/:orderId/confirmation` | GET | Customer | Confirmation payload |
| `/api/v1/customers/me/orders/:orderId/calendar` | GET | Customer | `.ics` pickup calendar file |
| `/api/v1/customers/me/orders/:orderId/events` | GET | Customer | Status timeline |
| `/api/v1/customers/me/orders/:orderId/cancel` | POST | Customer | Cancel with reason |
| `/api/v1/customers/me/orders/:orderId/reorder` | POST | Customer | Pre-populate cart |
| `/api/v1/customers/me/orders/:orderId/review` | POST | Customer | Submit verified-purchase review |
| WebSocket `customer.{user_id}.orders.{order_id}` | Subscribe | Customer | Real-time status updates |

Order lifecycle: [Marketplace Mechanics — Order lifecycle](../../product/marketplace-mechanics.md#order-lifecycle).

Reviews require verified purchase — [Reviews & community](../../product/marketplace-mechanics.md#reviews--community).

---

## Account & Preferences

Source: [Account Settings](../../pages/customer/account-settings.md)

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/v1/customers/me` | GET | Customer | Profile, preferences, notifications |
| `/api/v1/customers/me` | PATCH | Customer | Update profile fields |
| `/api/v1/customers/me/addresses` | GET | Customer | List saved addresses |
| `/api/v1/customers/me/addresses` | POST | Customer | Add address |
| `/api/v1/customers/me/addresses/:id` | PATCH | Customer | Update address |
| `/api/v1/customers/me/addresses/:id` | DELETE | Customer | Remove address |
| `/api/v1/customers/me/addresses/:id/default` | POST | Customer | Set default |
| `/api/v1/customers/me/preferences/dietary` | PATCH | Customer | Dietary chips + allergen alerts |
| `/api/v1/customers/me/preferences/notifications` | PATCH | Customer | Notification toggles |
| `/api/v1/customers/me/delete` | POST | Customer | Account deletion request |

Address autocomplete via platform geocoding service (debounced 300ms client-side).

---

## Help & Support

Source: [Help](../../pages/customer/help.md)

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/v1/help/articles` | GET | Optional | FAQ by category; optional `q` search |
| `/api/v1/help/categories` | GET | Optional | Category list with counts |
| `/api/v1/support/tickets` | POST | Optional | Submit support request |

Support ticket payload: `category`, `name`, `email`, `message`, optional `order_id` (verified ownership), `referrer_page`, `user_agent`.

FAQ content may be static CMS in v1 — API optional if bundled at build time.

---

## Auth Endpoints (Customer)

Source: [Login](../../pages/auth/login.md), [Signup](../../pages/auth/signup.md), [Password Reset](../../pages/auth/password-reset.md)

See [Authentication](authentication.md) for full auth endpoint catalog.

Customer signup: `POST /api/v1/auth/signup` with `account_type: "customer"`.

---

## Service Ownership

| Domain | Primary service |
|--------|-----------------|
| Discovery, search, browse | [Discovery Service](../services/discovery-service.md) |
| Storefront, menu items | [Catalog Service](../services/catalog-service.md) |
| Cart, checkout, orders | [Order Service](../services/order-service.md) |
| Payments | [Payment Service](../services/payment-service.md) |
| Account, auth | [Identity Service](../services/identity-service.md) |
| Notifications | [Notification Service](../services/notification-service.md) |
| Reviews (write) | [Trust Service](../services/trust-service.md) |

---

## Related Documents

- [API Overview](api-overview.md)
- [Authentication](authentication.md)
- [Creator API](creator-api.md)
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Customer Purchase Flow](../../pages/flows/customer-purchase-flow.md)
- [Information Architecture](../../pages/information-architecture.md)
