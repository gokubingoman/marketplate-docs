# Authentication & Authorization

> Roles, sessions, JWT, and RBAC for Marketplate — see [Founding Constitution](../../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Engineering

---

## Purpose

Define how users authenticate across the three Marketplate surfaces (Customer Marketplace, Creator OS, Admin) and how authorization is enforced at the API layer. Implemented primarily by [Identity Service](../services/identity-service.md).

Product context: [Information Architecture — Authentication & Access Matrix](../../pages/information-architecture.md#authentication--access-matrix), [Marketplace Mechanics — Verified to sell](../../product/marketplace-mechanics.md#marketplace-model-overview).

`TODO(decision):` Auth provider selection (Auth0, Clerk, custom) affects token format and social login availability.

---

## Account Types & Roles

Marketplate uses a **single User record** with one or more **roles**. A person may hold both customer and creator roles (role switching in UI).

| Role | Surface | Description |
|------|---------|-------------|
| **Customer** | Customer Marketplace | Browse, cart, checkout, orders, account |
| **Creator — Owner** | Creator OS | Full creator account control |
| **Creator — Staff (orders)** | Creator OS | View/advance orders; no cancel/refund |
| **Creator — Staff (read-only)** | Creator OS | View-only access |
| **Admin — Trust & Safety** | Admin | Verification, moderation, disputes |
| **Admin — Senior reviewer** | Admin | Override rejected items, escalate |
| **Admin — Creator Success** | Admin | View queue, internal notes — `TODO(decision):` scope |
| **Admin — Read-only** | Admin | View without actions |
| **Admin — Platform config** | Admin | Platform settings management |

### Creator verification states

Separate from auth roles — governs commerce capability:

| State | Can access Creator OS | Can accept paid orders |
|-------|:---------------------:|:----------------------:|
| Onboarding | ✓ | ✗ |
| Identity approved, kitchen pending | ✓ | ✗ |
| Fully verified | ✓ | ✓ |
| Suspended | ✓ (read-only banner) | ✗ |
| Removed | ✗ | ✗ |

---

## Session vs JWT

### Web clients (recommended v1)

| Mechanism | Usage |
|-----------|-------|
| **HttpOnly secure cookie** | Primary session transport for web |
| **Session store** | Redis-backed session with 30-day sliding expiry |
| **CSRF token** | Double-submit cookie on mutating requests |

Flow: `POST /api/v1/auth/login` → server sets `mp_session` cookie → subsequent requests authenticated via cookie.

### Mobile & API clients

| Mechanism | Usage |
|-----------|-------|
| **JWT access token** | Short-lived (15 min), Bearer header |
| **Refresh token** | Long-lived (30 days), rotated on use, stored securely on device |

Flow: `POST /api/v1/auth/login` with `Accept: application/json` → returns `{ access_token, refresh_token, expires_in }`.

### Guest cart sessions

Anonymous customers receive a `mp_guest` cookie (7-day) linking session-scoped cart. On login/signup, guest cart merges with account cart per [Cart page spec](../../pages/customer/cart.md).

---

## Auth Endpoints

Consolidated from auth page specs:

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/v1/auth/signup` | POST | None | Create customer or creator account |
| `/api/v1/auth/login` | POST | None | Authenticate; return session or JWT |
| `/api/v1/auth/logout` | POST | Required | Invalidate session/tokens |
| `/api/v1/auth/session` | GET | Cookie/token | Validate session; return user + roles |
| `/api/v1/auth/verify-email` | POST | None | Confirm email token |
| `/api/v1/auth/resend-verification` | POST | None | Resend confirmation email |
| `/api/v1/auth/password-reset/request` | POST | None | Queue reset email |
| `/api/v1/auth/password-reset/validate-token` | GET | None | Validate token before form |
| `/api/v1/auth/password-reset/confirm` | POST | None | Set new password |

Login response (success):

```json
{
  "data": {
    "user": {
      "id": "uuid",
      "email": "user@example.com",
      "roles": ["customer"],
      "email_verified": true
    },
    "creator": null,
    "redirect_url": "/"
  }
}
```

Creator login additionally includes `creator: { id, slug, verification_status }`.

---

## RBAC Permission Matrix

Permissions are evaluated as `{resource}:{action}` scopes. Middleware checks scope before handler execution.

### Customer scopes

| Scope | Endpoints |
|-------|-----------|
| `cart:read`, `cart:write` | `/api/v1/cart/*` |
| `checkout:write` | `/api/v1/checkout/*` |
| `orders:read`, `orders:write` | `/api/v1/customers/me/orders/*` |
| `profile:read`, `profile:write` | `/api/v1/customers/me/*` |
| `support:write` | `/api/v1/support/tickets` |

### Creator scopes

| Scope | Roles | Endpoints |
|-------|-------|-----------|
| `creator.dashboard:read` | All staff | `/api/v1/creator/dashboard/*` |
| `creator.orders:read` | All staff | `GET /api/v1/creator/orders*` |
| `creator.orders:write` | Owner, Staff-orders | `PATCH .../status`, cancel |
| `creator.catalog:read` | All staff | `GET /api/v1/creator/catalog/*` |
| `creator.catalog:write` | Owner | Catalog mutations |
| `creator.availability:write` | Owner | `/api/v1/creator/availability/*` |
| `creator.compliance:write` | Owner | Compliance uploads |
| `creator.payouts:read` | Owner | `/api/v1/creator/payouts/*` |
| `creator.analytics:read` | Owner (revenue), Staff (aggregates) | `/api/v1/creator/analytics/*` |
| `creator.messages:write` | Owner, Staff-orders | `/api/v1/creator/messages/*` |
| `creator.storefront:write` | Owner | `/api/v1/creator/storefront/*` |

Revenue fields omitted from analytics responses for non-owner staff.

### Admin scopes

| Scope | Roles | Endpoints |
|-------|-------|-----------|
| `admin.verification:read` | All admin | `GET .../verification/*` |
| `admin.verification:write` | T&S reviewer, Senior | Approve/reject/request-info |
| `admin.moderation:write` | T&S reviewer | Moderation decisions |
| `admin.disputes:write` | T&S reviewer, Senior | Dispute resolution |
| `admin.creators:write` | Senior | Suspend/reinstate |
| `admin.settings:write` | Platform config | Settings PATCH |
| `admin.audit:read` | All admin | Audit feeds |

### Separation of duties

- Operators cannot review verification items for their own test accounts in production.
- Destructive admin actions (suspend, reject, refund) require rationale in request body — logged to [AuditLog](../data/core-entities.md#auditlog).

---

## Authorization Middleware

Request pipeline:

```
Request → Extract credentials → Validate session/JWT → Load user + roles
       → Resolve creator context (Creator OS routes)
       → Check permission scopes → Handler
```

### Creator context resolution

Creator OS routes require `X-Creator-Id` header or implicit from authenticated user's primary creator account. Staff users are linked via `CreatorMembership` with role assignment.

### Resource ownership checks

| Resource | Rule |
|----------|------|
| Customer orders | `order.customer_id == auth.user_id` |
| Creator orders | `order.creator_id == auth.creator_id` |
| Admin resources | Scope check only — no ownership |
| Public discovery | No auth required; verified-only filter server-side |

---

## Security Requirements

| Requirement | Implementation |
|-------------|----------------|
| Password storage | bcrypt (cost ≥ 12) or delegated to auth provider |
| Session fixation | Regenerate session ID on login |
| Brute force protection | Rate limits on auth endpoints; exponential backoff |
| Email verification | Required before checkout (customer) and verification submission (creator) |
| Audit logging | All auth events: login, logout, failed login, password reset, role changes |
| MFA | `TODO(decision):` Required for admin in v1? |
| Token expiry | Access 15 min; refresh 30 days; password reset 1 hour |

---

## Multi-Role Users

Creators who also purchase as customers hold both role sets. UI role switching does not re-authenticate — session contains all roles; active surface determines default API context.

Customer endpoints use customer scopes regardless of creator role. Creator endpoints require explicit creator context.

---

## Related Documents

- [API Overview](api-overview.md)
- [Identity Service](../services/identity-service.md)
- [Customer API](customer-api.md)
- [Creator API](creator-api.md)
- [Admin API](admin-api.md)
- [Core Entities — User](../data/core-entities.md#user)
- [Login page spec](../../pages/auth/login.md)
- [Information Architecture](../../pages/information-architecture.md)
