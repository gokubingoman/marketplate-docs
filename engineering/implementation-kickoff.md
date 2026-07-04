# Implementation Kickoff

> How to start building Marketplate from this documentation repository — Phase A through launch.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Engineering · Product

---

## Purpose

This document is the **engineering entry point** after documentation Phases 1–5. It translates [Build Readiness](../roadmap/build-readiness.md) into a sequenced implementation plan with doc references, ADR assumptions, and exit criteria per phase.

**Rule:** Code traces to docs. If implementation diverges, update docs or publish an ADR first.

---

## Before writing code

| Gate | Doc | Status |
|------|-----|--------|
| Architecture understood | [Architecture Overview](architecture-overview.md) | Required reading |
| ADR assumptions reviewed | [Decision Index](../decisions/README.md) | 9 Proposed ADRs — use interim stubs only in dev/staging |
| Security baseline | [Security Policy](security-policy.md) | Required for prod |
| Page specs for target sprint | [`pages/`](../pages/) | One vertical slice at a time |

**Do not enable live Stripe, production auth, or published legal text** until ADRs are **Accepted** and counsel approves `legal/`.

---

## Recommended repository layout (application code)

Separate application repo from this docs repo. Suggested monorepo structure:

```
marketplate/
├── apps/
│   ├── web/                 # Customer + Creator + Admin (Next.js or similar)
│   └── worker/              # Event consumers, scheduled jobs
├── packages/
│   ├── db/                  # Migrations, schema per module
│   ├── domain/              # Module boundaries (identity, trust, catalog, …)
│   ├── ui/                  # Design system implementation
│   └── shared/              # Types, events, utils
├── infra/                   # IaC — provider per ADR when accepted
├── docker-compose.yml       # Local: Postgres, Redis, MinIO, Mailpit
└── docs/                    # Submodule or link to marketplate-docs
```

Maps to **modular monolith** in [Architecture Overview](architecture-overview.md#strategic-approach-modular-monolith-first) — one deployable `api` + `worker` at launch.

---

## Tech stack (from architecture docs)

| Layer | Choice | Reference |
|-------|--------|-----------|
| Application | TypeScript modular monolith | [Architecture Overview](architecture-overview.md) |
| Database | PostgreSQL (schema per module) | [Data Model Overview](data/data-model-overview.md) |
| Cache / sessions | Redis | [Infrastructure Overview](infrastructure-overview.md) |
| Object storage | S3-compatible (MinIO local) | [Trust Service](services/trust-service.md) |
| Payments | Stripe Connect Express (assumption) | [ADR-006](../decisions/adr-006-stripe-connect-model.md) |
| Auth | Clerk adapter (assumption) | [ADR-004](../decisions/adr-004-auth-provider.md) |
| Events | Outbox → queue (SNS/SQS or equivalent) | [Integration Patterns](integration-patterns.md) |
| Frontend | React; design system from `design-system/` | [Components](../design-system/components/) |

Cloud provider: `TODO(decision):` — use Docker Compose locally; defer IaC until [ADR-001](../decisions/adr-001-geographic-launch-market.md) accepted.

---

## Phase A — Engineering foundation

**Goal:** Runnable local stack, CI, identity stub, core schema, design tokens.

| Step | Deliverable | Doc source |
|------|-------------|------------|
| A1 | Monorepo + Docker Compose (Postgres, Redis, MinIO) | [Infrastructure — Local dev](infrastructure-overview.md) |
| A2 | CI: lint, test, build image on PR | [Infrastructure — Deployment pipeline](infrastructure-overview.md#deployment-pipeline) |
| A3 | DB migrations — `identity`, `core` schemas | [Core Entities](data/core-entities.md) |
| A4 | Identity module: User, roles, session stub | [Identity Service](services/identity-service.md), [Authentication API](api/authentication.md) |
| A5 | Auth provider adapter (`stub` + `clerk` interface) | [ADR-004](../decisions/adr-004-auth-provider.md) |
| A6 | Design tokens + Button, Input, Badge components | [Color](../design-system/foundations/color.md), [Components](design-system/components/) |
| A7 | Structured logging + health endpoints | [Architecture — Observability](architecture-overview.md) |

**Exit criteria:** `docker compose up` → health check green; login flow (stub auth); Storybook or equivalent for core components.

---

## Phase B — Trust path (MVP critical path)

**Goal:** Creator can onboard, admin can verify, verified creator can list (unpublished → published with moderation).

| Step | Deliverable | Doc source |
|------|-------------|------------|
| B1 | Creator signup + onboarding shell | [Creator Signup](../pages/auth/creator-signup.md), [Onboarding Flow](../pages/flows/creator-onboarding-flow.md) |
| B2 | Identity / kitchen / compliance upload flows | [Identity Verification](../pages/auth/identity-verification.md), [Kitchen Verification](../pages/auth/kitchen-verification.md) |
| B3 | Trust module + audit log (append-only) | [Trust Service](services/trust-service.md) |
| B4 | Admin verification queue | [Verification Queue](../pages/admin/verification-queue.md), [Verification Review SOP](../operations/verification-review-sop.md) |
| B5 | Verification Assist integration (async, human gate) | [Verification Assist](../ai/verification-assist.md) |
| B6 | Verified-to-sell gate on catalog writes | [Marketplace Mechanics — Verified to sell](../product/marketplace-mechanics.md#marketplace-model-overview) |

**Exit criteria:** End-to-end test: creator submits → operator approves → creator adds menu item. Unverified creator cannot publish paid listing.

**Ops:** Train against [Verification Review SOP](../operations/verification-review-sop.md) before real documents.

---

## Phase C — Commerce loop

**Goal:** Customer discovers creator, checks out, creator fulfills, payout recorded.

| Step | Deliverable | Doc source |
|------|-------------|------------|
| C1 | Storefront + menu item pages | [Creator Storefront](../pages/customer/creator-storefront.md) |
| C2 | Cart + checkout + Stripe test mode | [Checkout](../pages/customer/checkout.md), [Payment Service](services/payment-service.md) |
| C3 | Order lifecycle + notifications | [Order Service](services/order-service.md), [Order Fulfillment Flow](../pages/flows/order-fulfillment-flow.md) |
| C4 | Creator order queue | [Orders dashboard](../pages/creator/orders.md) |
| C5 | Payout job (weekly assumption) | [ADR-003](../decisions/adr-003-commission-structure.md), [Payout Processing SOP](../operations/payout-processing-sop.md) |

**Exit criteria:** Test card purchase → order confirmed → creator marks fulfilled → payout row in ledger (Stripe test).

---

## Phase D — Discovery and instrumentation

| Step | Deliverable | Doc source |
|------|-------------|------------|
| D1 | Home, search, browse (verified-only) | [Discovery Service](services/discovery-service.md) |
| D2 | Reviews post-completion | [Marketplace Mechanics — Reviews](../product/marketplace-mechanics.md#reviews--community) |
| D3 | Help center surface | [Help page](../pages/customer/help.md) ← `docs/help-center/` |
| D4 | Analytics events per page spec | [Event Taxonomy](../analytics/event-taxonomy.md) |

**Exit criteria:** Events in staging warehouse/table; Verified GMV computable per [Metrics Definitions](../analytics/metrics-definitions.md).

---

## Phase E — Launch readiness

Requires **Accepted ADRs**, counsel-approved `legal/`, staffed ops per [Marketplace Launch Ops SOP](../operations/marketplace-launch-ops-sop.md).

| Step | Reference |
|------|-----------|
| Legal published | [`legal/`](../legal/README.md) |
| SOPs trained | [`operations/`](../operations/README.md) |
| Support live | [Support Playbook](../support/support-playbook.md) |
| Security review | [Security Policy](security-policy.md) |
| Soft launch | [Launch Plan](../growth/launch-plan.md) |

---

## Sprint 0 checklist (first two weeks)

- [ ] Application repo created; docs linked (submodule or README pointer to `marketplate-docs`)
- [ ] Docker Compose local stack running
- [ ] CI green on empty/test app
- [ ] ADR interim assumptions documented in repo README
- [ ] `User` + `Creator` entities migrated
- [ ] Stub auth login/logout
- [ ] Design tokens imported from `design-system/foundations/`
- [ ] First ADR acceptance workshop scheduled (001, 003, 006 minimum for commerce)

---

## Module → documentation map

| Module | Service doc | API doc | Key pages |
|--------|-------------|---------|-------------|
| Identity | [identity-service](services/identity-service.md) | [authentication](api/authentication.md) | `pages/auth/*` |
| Trust | [trust-service](services/trust-service.md) | [admin-api](api/admin-api.md) | `pages/admin/verification-*`, `pages/auth/*-verification` |
| Catalog | [catalog-service](services/catalog-service.md) | [creator-api](api/creator-api.md) | `pages/creator/catalog*`, `pages/customer/creator-storefront` |
| Order | [order-service](services/order-service.md) | [customer-api](api/customer-api.md) | `pages/customer/cart`, `checkout`, `orders/*` |
| Payment | [payment-service](services/payment-service.md) | [admin-api](api/admin-api.md) | `pages/creator/payouts`, checkout |
| Discovery | [discovery-service](services/discovery-service.md) | [customer-api](api/customer-api.md) | `pages/customer/home`, `search`, `browse` |
| Notification | [notification-service](services/notification-service.md) | — | Templates in page specs |

---

## Testing expectations

| Type | Scope |
|------|-------|
| Unit | Domain logic per module |
| Integration | Module boundaries + PostgreSQL; Stripe test mode |
| E2E | Critical paths: purchase flow, verification approval |
| Trust-critical | Verification cannot auto-approve; audit log immutable |

Trust-critical paths require higher coverage — [Glossary — Trust-Critical Path](../company/glossary.md#trust-critical-path).

---

## Related Documents

- [Build Readiness](../roadmap/build-readiness.md)
- [Architecture Overview](architecture-overview.md)
- [Infrastructure Overview](infrastructure-overview.md)
- [Data Flow](data-flow.md)
- [Decisions](../decisions/README.md)
- [Diagrams](../diagrams/README.md)
