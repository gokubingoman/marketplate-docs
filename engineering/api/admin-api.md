# Admin API

> Internal operations endpoints for Trust & Safety and platform configuration — see [API Overview](api-overview.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Engineering

---

## Purpose

Consolidated REST endpoint catalog for the Admin / Trust & Safety surface. Derived from [`pages/admin/`](../../pages/admin/) and enforcement flows in [Marketplace Mechanics](../../product/marketplace-mechanics.md).

**Invariant:** All mutating admin actions produce immutable audit records. AI recommends; humans approve on verification — [Human approval on high stakes](../../product/marketplace-mechanics.md#marketplace-model-overview).

Admin routes are never exposed in customer or creator navigation — [Information Architecture](../../pages/information-architecture.md).

---

## Authentication Summary

All admin endpoints require admin role with appropriate scopes. See [Authentication — Admin scopes](authentication.md#admin-scopes).

Internal-only network policies apply in production (VPN/IP allowlist recommended).

---

## Dashboard

Source: [Admin Dashboard](../../pages/admin/admin-dashboard.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/admin/dashboard/summary` | GET | admin.dashboard:read | Queue counts, SLA status |
| `/api/v1/admin/dashboard/health` | GET | admin.dashboard:read | Trend metrics; `range=7d` |
| `/api/v1/admin/dashboard/alerts` | GET | admin.dashboard:read | Actionable alert list |
| `/api/v1/admin/audit/feed` | GET | admin.audit:read | Recent admin actions paginated |

### Summary response

```json
{
  "data": {
    "queues": {
      "verification": { "count": 47, "sla_status": "warning", "median_age_hours": 36 },
      "moderation": { "count": 12, "sla_status": "ok" },
      "disputes": { "count": 8, "urgent": 2 },
      "creator_activation": { "count": 23 }
    }
  }
}
```

---

## Verification Queue

Source: [Verification Queue](../../pages/admin/verification-queue.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/admin/verification/queue` | GET | admin.verification:read | Paginated list with filters |
| `/api/v1/admin/verification/items/:id` | GET | admin.verification:read | Full item + documents + AI flags |
| `/api/v1/admin/verification/items/:id/approve` | POST | admin.verification:write | Approve with checklist |
| `/api/v1/admin/verification/items/:id/reject` | POST | admin.verification:write | Reject with rationale |
| `/api/v1/admin/verification/items/:id/request-info` | POST | admin.verification:write | Request info message |
| `/api/v1/admin/verification/items/:id/notes` | POST | admin.verification:write | Internal note |
| `/api/v1/admin/verification/items/:id/documents/:docId/url` | GET | admin.verification:read | Signed preview URL |

### Approve request

```json
{
  "checklist": {
    "id_verified": true,
    "name_matches_entity": true,
    "address_confirmed": true
  },
  "ai_flags_dismissed": [
    { "flag_id": "uuid", "reason": "Expiry date verified manually on secondary doc" }
  ],
  "internal_notes": "Approved — cottage food registration valid through 2027"
}
```

Reject and request-info require creator-visible `rationale` field.

Decisions emit webhook/event → creator verification status update on [Identity Verification](../../pages/auth/identity-verification.md), [Kitchen Verification](../../pages/auth/kitchen-verification.md), [Compliance Center](../../pages/auth/compliance-center.md).

AI flags from internal ML service — not editable, only dismissable with logged note.

`TODO(decision):` Concurrent review locking model for queue items.

---

## Moderation Queue

Source: [Moderation Queue](../../pages/admin/moderation-queue.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/admin/moderation/queue` | GET | admin.moderation:read | Paginated moderation items |
| `/api/v1/admin/moderation/items/:id` | GET | admin.moderation:read | Full context + history |
| `/api/v1/admin/moderation/items/:id/decide` | POST | admin.moderation:write | Decision with action |
| `/api/v1/admin/moderation/items/:id/escalate` | POST | admin.moderation:write | Escalate to senior/legal |
| `/api/v1/admin/moderation/policies` | GET | admin.moderation:read | Policy snippets for UI |

### Decide request

```json
{
  "action": "remove_content",
  "rationale": "Review violates harassment policy — targeted personal attack",
  "duration": null,
  "notify_parties": true
}
```

Actions map to [Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder): education → warning → listing restriction → order suspension → account suspension → permanent removal.

Actions emit audit events and notifications per policy templates.

---

## Disputes

Source: [Dispute Detail](../../pages/admin/dispute-detail.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/admin/disputes/:id` | GET | admin.disputes:read | Full case + order + parties |
| `/api/v1/admin/disputes/:id/messages` | GET | admin.disputes:read | Message thread |
| `/api/v1/admin/disputes/:id/messages` | POST | admin.disputes:write | Operator platform message |
| `/api/v1/admin/disputes/:id/request-info` | POST | admin.disputes:write | Request info workflow |
| `/api/v1/admin/disputes/:id/resolve` | POST | admin.disputes:write | Resolve case |
| `/api/v1/admin/disputes/:id/escalate` | POST | admin.disputes:write | Escalate case |
| `/api/v1/admin/disputes/:id/audit` | GET | admin.disputes:read | Audit trail |

### Resolve request

```json
{
  "outcome": "partial_refund",
  "amount": 2400,
  "rationale": "Order partially consumed; creator agreed to 50% refund",
  "notify": true
}
```

Outcomes: `full_refund`, `partial_refund`, `credit`, `no_action`.

Payment integration: `POST /api/v1/admin/payments/refund` invoked by resolve — idempotent with dispute ID as Idempotency-Key.

Dispute stages per [Marketplace Mechanics — Disputes](../../product/marketplace-mechanics.md#disputes).

---

## Creator Administration

Source: [Creator Admin Detail](../../pages/admin/creator-admin-detail.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/admin/creators/:id` | GET | admin.creators:read | Profile summary + KPIs |
| `/api/v1/admin/creators/:id/verification` | GET | admin.creators:read | Verification history |
| `/api/v1/admin/creators/:id/compliance` | GET | admin.creators:read | Compliance items |
| `/api/v1/admin/creators/:id/orders` | GET | admin.creators:read | Paginated order summary |
| `/api/v1/admin/creators/:id/disputes` | GET | admin.creators:read | Dispute list |
| `/api/v1/admin/creators/:id/trust` | GET | admin.creators:read | Moderation + metrics |
| `/api/v1/admin/creators/:id/notes` | POST | admin.creators:write | Internal note |
| `/api/v1/admin/creators/:id/actions/suspend` | POST | admin.creators:write (senior) | Suspend with rationale |
| `/api/v1/admin/creators/:id/actions/reinstate` | POST | admin.creators:write (senior) | Reinstate |
| `/api/v1/admin/creators/:id/actions/request-reverification` | POST | admin.creators:write | Trigger re-verification |
| `/api/v1/admin/creators/:id/audit` | GET | admin.creators:read | Full audit log |

Status changes push notifications to creator-facing verification and compliance pages.

---

## Platform Settings

Source: [Platform Settings](../../pages/admin/platform-settings.md)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/admin/settings/:category` | GET | admin.settings:read | Current settings for category |
| `/api/v1/admin/settings/:category` | PATCH | admin.settings:write | Save with changes + rationale |
| `/api/v1/admin/settings/:category/history` | GET | admin.settings:read | Change audit log |
| `/api/v1/admin/settings/:category/rollback` | POST | admin.settings:write | Rollback to version |
| `/api/v1/admin/settings/jurisdictions` | GET/POST | admin.settings:write | Jurisdiction templates |
| `/api/v1/admin/settings/feature-flags` | GET/PATCH | admin.settings:write | Flag management |

### Settings categories

| Category | Examples |
|----------|----------|
| `verification` | SLA thresholds, human approval required (read-only invariant) |
| `reviews` | Review window, pay-to-remove (read-only: false) |
| `fees` | Platform commission — `TODO(decision):` commission structure |
| `compliance` | Grace periods, renewal reminders |
| `notifications` | Template IDs, channel defaults |
| `discovery` | Featured collection rules, min trust tier |

**Audit schema:** `{ id, category, actor_id, timestamp, before_json, after_json, rationale }`

Secrets never returned in GET — reference IDs only.

Hardcoded invariants (API enforced, read-only in UI):
- `verification.human_approval_required: true`
- `reviews.pay_to_remove: false`

---

## Payments (Admin)

| Endpoint | Method | Scope | Purpose |
|----------|--------|-------|---------|
| `/api/v1/admin/payments/refund` | POST | admin.disputes:write | Execute refund (**Idempotency-Key required**) |

Invoked by dispute resolution and platform force-cancel scenarios.

---

## Service Ownership

| Domain | Primary service |
|--------|-----------------|
| Verification queue | [Trust Service](../services/trust-service.md) |
| Moderation | [Trust Service](../services/trust-service.md) |
| Disputes | [Trust Service](../services/trust-service.md) + [Payment Service](../services/payment-service.md) |
| Creator admin | [Trust Service](../services/trust-service.md) + [Identity Service](../services/identity-service.md) |
| Platform settings | Platform config service (Trust Service admin module) |
| Audit feed | All services → [AuditLog](../data/core-entities.md#auditlog) |
| Dashboard aggregates | Read models across services |

---

## Related Documents

- [API Overview](api-overview.md)
- [Authentication](authentication.md)
- [Creator API](creator-api.md)
- [Trust Service](../services/trust-service.md)
- [Payment Service](../services/payment-service.md)
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Trust Verification Flow](../../pages/flows/trust-verification-flow.md)
