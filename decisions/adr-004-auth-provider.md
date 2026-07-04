# ADR-004: Authentication Provider

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Engineering · Security

---

## Decision

**Pending founder approval.**

Select the authentication provider for customer, creator, and admin login — or build native auth on the Identity Service.

---

## Background

[Identity Service](../engineering/services/identity-service.md) owns sessions, roles, and RBAC. [Authentication API](../engineering/api/authentication.md) defines JWT + session model across three surfaces.

Requirements:

- Email/password + magic link minimum
- MFA required for **all admin** ([Access Control](../engineering/access-control.md))
- Social login optional for customers (Google, Apple)
- Role switching (customer ↔ creator) on single User record
- SOC 2 / security review path for admin access
- Web-first Phase 1; mobile SDK compatibility Phase 2

`TODO(decision):` markers appear in identity-service, authentication.md, infrastructure-overview.

---

## Options

| Option | Provider | Pros | Cons |
|--------|----------|------|------|
| **A — Clerk** | Managed auth + UI components | Fast MVP; MFA built-in; good DX | Vendor lock-in; cost at scale; custom admin flows |
| **B — Auth0** | Enterprise identity platform | Mature; SSO path for enterprise Phase 15 | Complex pricing; heavier integration |
| **C — Supabase Auth / Firebase** | BaaS auth | Cheap; quick start | Less suited to custom admin RBAC matrix |
| **D — Native (Identity Service + passkeys)** | Self-hosted sessions in Identity Service | Full control; no per-MAU auth tax | Build + maintain MFA, recovery, breach response |

---

## Reasoning (recommended direction)

**Recommend Option A — Clerk for Phase 1**, with abstraction layer in Identity Service to allow migration:

1. Fastest path to MFA-enforced admin and role metadata.
2. Engineering team focuses on trust/commerce critical path, not auth primitives.
3. Identity Service wraps Clerk as `AuthProvider` adapter — swap later if needed.
4. Clerk Organizations map poorly to creator staff roles — **custom RBAC stays in Identity Service**, not Clerk roles alone.

Admin MFA: enforce via Clerk + platform gate (no admin API access without `mfa_verified` claim).

---

## Alternatives considered

- **Native from day one** — rejected for Phase 1 timeline; revisit if auth costs exceed $X/month at scale (define at acceptance).
- **Auth0** — viable alternative if enterprise SSO is near-term priority; Clerk wins on DX for small team.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Weeks saved on auth infrastructure | Vendor dependency |
| MFA for admin out of box | Custom creator staff RBAC still custom-built |
| Pre-built login UI | Brand customization limits |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| Identity Service | AuthProvider adapter implementation |
| Login/signup page specs | Clerk components vs custom |
| Admin console | MFA enrollment gate |
| Security policy | IdP in vendor inventory |
| Mobile Phase 2 | Native SDK selection |

---

## Interim implementation

- Identity Service: `AuthProvider` interface with `StubAuthProvider` for local dev
- Environment variables: `AUTH_PROVIDER=clerk|stub`
- Do not provision production Clerk tenant until ADR **Accepted**

---

## Related Documents

- [Identity Service](../engineering/services/identity-service.md)
- [Authentication API](../engineering/api/authentication.md)
- [Access Control](../engineering/access-control.md)
- [Login page spec](../pages/auth/login.md)
