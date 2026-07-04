# ADR-008: Analytics and BI Stack

**Status:** Proposed  
**Date:** 2026-07-03  
**Deciders:** Founders · Engineering · Product · Analytics

---

## Decision

**Pending founder approval.**

Select the **product analytics SDK**, **event pipeline**, and **BI/dashboard tool** for Phase 1 instrumentation and executive reporting.

---

## Background

[Analytics folder](../analytics/) defines metrics, events, dashboards, and governance. [Event Taxonomy](../analytics/event-taxonomy.md) specifies client + server events from 37 page specs.

Requirements:

- Verified GMV as north star with trust guardrails ([Metrics Definitions](../analytics/metrics-definitions.md))
- PII blocklist at ingestion ([Data Governance](../analytics/data-governance.md))
- Server domain events from Payment, Order, Trust services
- Dashboards for Executive, T&S, CS, Product ([Dashboards](../analytics/dashboards.md))
- SOC 2 path; GDPR/CCPA when launch market requires

---

## Options

| Layer | Option A (recommended stack) | Option B | Option C |
|-------|------------------------------|----------|----------|
| **Product analytics SDK** | PostHog (self-host or cloud) | Amplitude | Segment + multiple destinations |
| **Event pipeline** | Kafka or SNS/SQS → warehouse | Direct SDK → warehouse only | RudderStack |
| **Warehouse** | BigQuery | Snowflake | Postgres analytics replica (Phase 1 only) |
| **BI / dashboards** | Metabase on warehouse | Looker | PostHog built-in dashboards only |
| **Real-time ops** | CloudWatch + custom alerts | Datadog | Grafana |

---

## Reasoning (recommended direction)

**Recommend Option A — PostHog + BigQuery + Metabase:**

| Choice | Rationale |
|--------|-----------|
| **PostHog** | Open-source option; feature flags co-located; session replay optional (PII scrubbed); reasonable cost at Phase 1 scale |
| **BigQuery** | Serverless; scales with GMV; SQL aligns with metrics-definitions SQL examples |
| **Metabase** | Self-serve dashboards for CS/Ops without Looker cost; maps to [Dashboards spec](../analytics/dashboards.md) |
| **SNS/SQS → Lambda → BQ** | Simple event bus before Kafka; sufficient to 1M events/day |

**Not Phase 1:** Full Kafka cluster, Segment enterprise contract, real-time ML feature store.

PII rules: hash search queries in production; blocklist email, phone, full name in event properties per data governance.

---

## Alternatives considered

- **Amplitude + Looker** — strong but higher cost before product-market fit.
- **Postgres-only analytics** — acceptable for soft launch ≤30 days; migrate before public launch scale.

---

## Tradeoffs

| Gain | Sacrifice |
|------|-----------|
| Integrated flags + analytics (PostHog) | PostHog session replay needs strict PII config |
| BigQuery scales without ops | GCP vendor commitment |
| Metabase democratizes dashboards | Less polished than Looker for executives |

---

## Impact

| Area | Change when accepted |
|------|---------------------|
| All page specs | SDK snippet in Analytics sections |
| Integration patterns | Domain event → pipeline wiring |
| Engineering CI | Event schema validation |
| Data Governance | Vendor DPAs, retention jobs |
| Executive reporting | Metabase dashboard URLs |

---

## Interim implementation

- Emit structured logs + server events to PostgreSQL `analytics_events` staging table
- Manual weekly Verified GMV SQL until pipeline live
- Feature flags: env-based until PostHog provisioned
- Do not send production PII to any vendor until ADR **Accepted** + DPA signed

---

## Related Documents

- [Analytics README](../analytics/README.md)
- [Event Taxonomy](../analytics/event-taxonomy.md)
- [Data Governance](../analytics/data-governance.md)
- [Architecture Overview — Analytics module](../engineering/architecture-overview.md)
- [Integration Patterns](../engineering/integration-patterns.md)
