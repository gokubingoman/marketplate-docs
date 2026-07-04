# Data Governance

> Ownership, PII policy, retention, access control, and data quality standards for Marketplate analytics.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Analytics · Engineering · Legal

---

## Purpose

Analytics data powers product decisions, creator coaching, and trust enforcement. This document defines **how that data is owned, protected, retained, accessed, and validated** — ensuring measurement supports the trust thesis without compromising user privacy or regulatory obligations.

Governance applies to:

- Client product events ([Event Taxonomy](event-taxonomy.md))
- Server domain events ([Integration Patterns](../engineering/integration-patterns.md))
- Warehouse fact tables feeding [Metrics Definitions](metrics-definitions.md)
- Dashboards ([Dashboards](dashboards.md))

Legal and privacy policy details: `legal/` *(Phase 5 — in progress)*. Help center privacy summary: [Privacy](../docs/help-center/privacy.md).

---

## Data Ownership

### RACI matrix

| Data domain | Responsible | Accountable | Consulted | Informed |
|-------------|-------------|-------------|-----------|----------|
| Metric definitions | Analytics | Product | CS, T&S, Engineering | Leadership |
| Event taxonomy | Engineering | Analytics | Product | All eng teams |
| Client instrumentation | Engineering (surface teams) | Analytics | Product | QA |
| Domain event pipeline | Engineering (platform) | Analytics | Module owners | Ops |
| Executive dashboards | Analytics | Product | Leadership | Board |
| T&S dashboards | Analytics | Trust & Safety | Legal | Leadership |
| CS dashboards | Analytics | Customer Success | Product | CS team |
| Creator in-app analytics | Engineering (Creator API) | Product | Analytics | Creators |
| Warehouse infrastructure | Engineering (platform) | Engineering Architecture | Analytics, Security | Leadership |
| PII / privacy policy | Legal | Legal | Analytics, Security | All |

### Stewardship rules

1. **One accountable owner** per metric — listed in [Metrics Definitions](metrics-definitions.md)
2. **Schema changes** require Analytics approval + 5 business day notice to dashboard consumers
3. **Breaking changes** to event names require migration period with dual-write
4. **New PII fields** require Legal review before implementation — no exceptions
5. **Dashboard access** granted by role, not individual request — see [Access control](#access-control)

---

## PII in Analytics

### Classification

| Class | Examples | Analytics policy |
|-------|----------|------------------|
| **Prohibited — never collect** | Password, payment card, government ID number, full SSN, raw compliance document content | Block at SDK and ingestion API |
| **Prohibited — never log in events** | Email, phone, full name, street address, date of birth | Use IDs only; hash if diagnostic needed |
| **Restricted — server only** | IP address (full), precise geolocation | Coarse geo only in analytics; full IP in security logs with shorter retention |
| **Allowed — pseudonymous** | `user_id`, `anonymous_id`, `creator_id`, `order_id` | Primary analytics identifiers |
| **Allowed — aggregated** | Counts, rates, medians, persona segments | Default for dashboards |
| **Allowed — categorical** | `persona`, `market_id`, `fulfillment_type`, `error_code` | No re-identification risk when combined |

### PII rules by surface

| Surface | Additional rules |
|---------|-------------------|
| **Customer** | Search queries: store hashed `q` or `query_length` only in production analytics; full query in ops diagnostic table with 7-day retention and access restriction |
| **Creator** | Revenue visible only to owner in-app; never in cross-creator analytics exports |
| **Admin** | Operator `user_id` in audit log, not product analytics; document views audit-only |
| **Auth** | `auth.password_reset.request_success` — never log email; `auth.login.failure` — error code only |

### Consent and opt-out

| Tracking type | Consent required | Default |
|---------------|------------------|---------|
| Essential product analytics (funnels, errors) | Legitimate interest / ToS | On |
| Session replay | Explicit opt-in | Off at launch |
| Marketing attribution | Cookie consent banner | Off until accepted |
| Creator business analytics (in-app) | Creator agreement | On for verified creators |

`TODO(decision):` Final consent framework with Legal — align with `legal/privacy-policy.md`.

### SDK enforcement

Per [Event Taxonomy — Implementation](event-taxonomy.md#implementation-guide):

- Property key blocklist: `/email|phone|password|ssn|address_line|card/i`
- Ingestion API schema validation rejects prohibited fields
- Weekly automated scan of raw events for PII pattern detection

### Relationship to other stores

| Store | PII policy | Reference |
|-------|------------|-----------|
| Application logs | Structured JSON; no PII — [Architecture Logging](../engineering/architecture-overview.md#logging) | 30 days hot |
| Audit log | Operator actions; immutable — [Audit log pattern](../engineering/integration-patterns.md#audit-log-pattern) | Long-term |
| Order records | Allergen acks on order, not in analytics stream — [Order Service](../engineering/services/order-service.md) | Per retention schedule |
| Trust documents | Object storage; signed URLs — never in analytics | Compliance retention |

---

## Retention

### Analytics data retention schedule

| Data type | Hot (queryable) | Warm (archive) | Deletion |
|-----------|-----------------|----------------|----------|
| Raw client events | 90 days | 13 months | Anonymize after 14 months |
| Domain event facts (warehouse) | 24 months | 5 years (aggregates only) | Detail purge per schedule |
| Aggregated metrics (daily rollups) | Indefinite | — | — |
| Session-level funnels | 90 days | — | Delete |
| Search query diagnostic (hashed) | 7 days | — | Delete |
| Creator in-app analytics cache | 15 minutes | — | Expire |
| Dashboard exports (generated files) | 30 days | — | Delete |
| CS CRM intervention notes | Per CS policy | — | Not in analytics warehouse |

### User deletion (GDPR / CCPA)

When a user requests account deletion:

1. **Identity module** marks user deleted per [Identity Service](../engineering/services/identity-service.md)
2. **Analytics pipeline** receives `user.deleted` domain event
3. Within **30 days:**
   - Replace `user_id` with tombstone hash in raw events
   - Remove row-level links in warehouse dimension tables
   - Retain aggregated metrics (non-re-identifiable)
4. **Order financial records** retained per legal/tax requirements — de-identified in analytics

Audit log entries for trust/legal holds may be **exempt** from deletion — Legal review required.

### Alignment with infrastructure

| System | Retention | Reference |
|--------|-----------|-----------|
| Application logs | 30 days hot, 1 year archive | [Infrastructure Overview](../engineering/infrastructure-overview.md#logging) |
| Security / auth events | 90 days operational → SIEM | [Identity Service](../engineering/services/identity-service.md) |
| Audit log (trust/payment) | 7 years (financial/regulatory) | [Integration Patterns](../engineering/integration-patterns.md) |
| PostgreSQL backups | PITR 1 hour RPO | [Infrastructure Overview](../engineering/infrastructure-overview.md#disaster-recovery) |

---

## Access Control

### Tier model

| Tier | Who | Data scope | Tools |
|------|-----|------------|-------|
| **T0 — Public** | Creators (in-app) | Own creator data only | Creator Analytics API |
| **T1 — Operational** | CS, Support | Market-scoped aggregates; individual creator/order via admin tools (not warehouse) | Admin console, CS CRM |
| **T2 — Analytics** | Product, Analytics team | Full warehouse read; no raw PII columns | BI tool, SQL read replica |
| **T3 — Trust** | T&S analysts | Trust incidents, disputes, verification; audit log read | T&S dashboard, audit API |
| **T4 — Executive** | Leadership | Pre-built dashboards only; no SQL | Executive dashboard |
| **T5 — Engineering** | Platform eng | Infrastructure metrics + anonymized event samples | Observability stack |
| **T6 — Admin** | Analytics admin | Schema, pipeline config, access grants | All analytics infra |

### Access request process

1. Request via internal access ticket with role justification
2. Manager approval + Analytics admin for T2+
3. MFA required for T2+
4. Quarterly access review — revoke stale grants
5. All warehouse queries logged with `actor_id`

### Row-level security

| Table | Policy |
|-------|--------|
| Creator facts | CS sees market_id filter; creators see `creator_id = self` only |
| Customer facts | No individual customer rows for CS — cohort aggregates only |
| Trust incidents | T&S and Legal only |
| Admin events | T&S + audit; not joinable to customer PII in self-serve BI |

### Export controls

| Export type | Approval | Audit |
|-------------|----------|-------|
| Executive weekly PDF | Automated | Low sensitivity |
| CS at-risk creator list | CS manager | Logged |
| Warehouse CSV ad-hoc | Analytics + requester manager | Logged + DLP scan |
| Audit log export | T&S lead + Legal | Immutable audit of export |

`admin.creator.audit_export` event triggers compliance review if >1000 rows.

---

## Data Quality

### Quality dimensions

| Dimension | Standard | Monitoring |
|-----------|----------|------------|
| **Completeness** | ≥99% of expected domain events arrive within 5 minutes | Event lag alert |
| **Uniqueness** | Zero duplicate `event_id` in processed facts | Dedupe check daily |
| **Timeliness** | Dashboard cache within SLA (see [Dashboards](dashboards.md#implementation-notes)) | Cache age metric |
| **Validity** | 100% schema validation pass rate in production | Rejected event counter |
| **Consistency** | Verified GMV from events = Verified GMV from SQL ±0.1% | Daily reconciliation job |
| **Accuracy** | Metric spot-check vs source DB weekly during launch | Analytics QA checklist |

### Reconciliation jobs

| Job | Frequency | Action on failure |
|-----|-----------|-------------------|
| Verified GMV: events vs orders table | Daily | P1 if >0.1% drift |
| Order count: funnel vs completed orders | Daily | P2 investigate |
| Creator activation funnel vs trust states | Weekly | Product review |
| Payment success rate vs Stripe | Daily | Engineering + Payment on-call |
| Event schema registry sync | On deploy | Block deploy if mismatch |

### Incident response

Data quality incidents follow the same severity model as [Architecture — Trust failures](../engineering/architecture-overview.md#failure-modes):

| Severity | Example | Response |
|----------|---------|----------|
| P1 | Verified GMV wrong on executive dashboard | Halt dependent decisions; hotfix within 4 hours |
| P2 | Funnel undercounting due to SDK bug | Fix within 48 hours; annotate dashboard |
| P3 | Non-critical widget stale | Backlog fix; note in WBR |

Post-mortem required for P1/P2 — update metric definitions or instrumentation if root cause is definitional.

---

## Third-Party Analytics Vendors

`TODO(decision):` Product analytics vendor selection.

### Vendor evaluation criteria

| Criterion | Requirement |
|-----------|-------------|
| Data residency | US region at launch |
| DPA / BAA | Signed before production data |
| PII handling | No vendor-side PII storage without contract |
| Data deletion | Supports user deletion API |
| Subprocessor list | Legal review |
| Export | Full data export on contract termination |
| SOC 2 Type II | Required |

### Self-hosted option

PostHog self-hosted evaluated as privacy-preserving alternative — Engineering owns deployment if selected.

---

## Documentation & Change Management

| Change type | Process |
|-------------|---------|
| New metric | [Metrics Definitions](metrics-definitions.md) + dashboard widget |
| New event | [Event Taxonomy](event-taxonomy.md) + JSON Schema registry |
| Retention change | Legal review + 30-day notice to affected teams |
| Access tier change | Analytics admin + Security review |
| Vendor change | ADR in [`decisions/`](../decisions/) |

Schema registry lives in `engineering/analytics/` *(future)* or co-located with Analytics module code.

---

## Compliance Mapping

| Requirement | Analytics control |
|-------------|-------------------|
| PCI DSS | No card data in analytics — Stripe only |
| GDPR / CCPA | Deletion pipeline, consent, DPA |
| Food safety audit trail | Trust incidents + order allergen acks (order record, not analytics PII) |
| Marketplace transparency | Listing completeness metrics auditable |

Full regulatory mapping: `legal/regulatory-compliance.md` *(Phase 5)*.

---

## Related Documents

- [Analytics README](README.md)
- [Metrics Definitions](metrics-definitions.md)
- [Event Taxonomy](event-taxonomy.md)
- [Dashboards](dashboards.md)
- [Architecture Overview — Security](../engineering/architecture-overview.md#security)
- [Architecture Overview — Logging](../engineering/architecture-overview.md#logging)
- [Infrastructure Overview](../engineering/infrastructure-overview.md)
- [Integration Patterns — Audit log](../engineering/integration-patterns.md)
- [Help Center — Privacy](../docs/help-center/privacy.md)
- [Trust & Safety Standards](../docs/standards/trust-and-safety-standards.md)
