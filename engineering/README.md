# Engineering

System architecture, APIs, data models, and service specifications for Marketplate.

**Phase 3 status:** Complete

## Architecture

| Document | Description |
|----------|-------------|
| [Architecture Overview](architecture-overview.md) | System design, principles, high-level diagram |
| [Service Catalog](service-catalog.md) | All services and responsibilities |
| [Integration Patterns](integration-patterns.md) | Event-driven patterns, external integrations |
| [Infrastructure Overview](infrastructure-overview.md) | Cloud, deployment, environments |
| [Data Flow](data-flow.md) | End-to-end flows — purchase, onboarding, fulfillment, payout |

## API

| Document | Description |
|----------|-------------|
| [API Overview](api/api-overview.md) | REST conventions, versioning, auth, errors |
| [Authentication](api/authentication.md) | Sessions, JWT, roles, permissions |
| [Customer API](api/customer-api.md) | Discovery, cart, checkout, orders |
| [Creator API](api/creator-api.md) | Dashboard, catalog, fulfillment, payouts |
| [Admin API](api/admin-api.md) | Verification, moderation, disputes, platform |

## Data

| Document | Description |
|----------|-------------|
| [Data Model Overview](data/data-model-overview.md) | Entity relationships, conventions |
| [Core Entities](data/core-entities.md) | Users, creators, orders, catalog, trust |

## Services

| Document | Description |
|----------|-------------|
| [Identity Service](services/identity-service.md) | Auth, users, roles |
| [Trust Service](services/trust-service.md) | Verification, compliance, moderation |
| [Catalog Service](services/catalog-service.md) | Menu items, storefronts, availability |
| [Order Service](services/order-service.md) | Cart, checkout, order lifecycle |
| [Payment Service](services/payment-service.md) | Payments, payouts, disputes |
| [Notification Service](services/notification-service.md) | Email, push, SMS |
| [Discovery Service](services/discovery-service.md) | Search, browse, ranking |

## Related

- [Page specs](../pages/) — API requirements per screen
- [AI systems](../ai/) — AI platform documentation
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
