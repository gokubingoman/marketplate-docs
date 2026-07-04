# Marketplace Launch Ops SOP

> Standard Operating Procedure for Phase 1 marketplace launch day operations — go/no-go execution, staffing, monitoring, and rollback. — [Founding Constitution](../company/constitution.md)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Growth · Trust & Safety · Support · Engineering  
**Strategy companion:** [Launch Plan](../growth/launch-plan.md) · [Launching a New Market](../docs/playbooks/launching-new-market.md)

---

## Purpose

This SOP operationalizes launch execution for Company Phase 1 — Marketplace. It translates [Launch Plan](../growth/launch-plan.md) checklists into staffed workflows with explicit go/no-go authority, queue readiness, and incident routing.

Launch is not marketing-only. Operations must be staffed for verification volume, support tickets, trust incidents, and payment/payout monitoring before demand marketing scales.

**Launch geography:** `TODO(decision):` Geographic launch market — procedures use `[Launch Market]` until ADR resolved.

---

## Trigger

| Trigger | Source |
|---------|--------|
| Pre-launch go/no-go meeting complete | Launch Lead |
| Soft launch start date | Launch Plan Phase 2 exit criteria met |
| Public launch date | Soft launch liquidity thresholds met |
| Launch rollback condition | Engineering or Trust IC |

---

## Owner

| Role | Launch responsibility |
|------|----------------------|
| **Launch Lead** | Go/no-go decisions, cross-team coordination |
| **Trust & Safety Lead** | Verification queue staffing, incident IC |
| **Support Lead** | Tier 1 staffing, macro readiness, escalation paths |
| **Engineering Lead** | Platform stability, feature flags, `#incidents` |
| **Creator Success Lead** | Founding cohort activation, first-order coaching |
| **Finance** | Payment/payout monitoring |
| **Founder / Executive Sponsor** | Final public launch approval |

---

## Prerequisites

### Pre-launch (T-7 days)

| Check | Owner | Verified |
|-------|-------|----------|
| Legal framework counsel-reviewed or soft-launch exception documented | Legal | ☐ |
| Help Center articles live for launch market | Support | ☐ |
| Support macros tested — [Macro Library](../support/macro-library.md) | Support | ☐ |
| Verification queue staffed for 2× expected volume | Trust | ☐ |
| [Verification Review SOP](verification-review-sop.md) trained | Trust | ☐ |
| [Platform Admin SOP](platform-admin-sop.md) shift schedule published | Ops | ☐ |
| Payment and payout smoke tests in production | Engineering + Finance | ☐ |
| Analytics events firing per [Event Taxonomy](../analytics/event-taxonomy.md) | Engineering | ☐ |
| Founding creator cohort verified (minimum supply target) | Creator Success | ☐ |
| Rollback runbook reviewed | Engineering | ☐ |

### Soft launch (T-0)

| Check | Owner | Verified |
|-------|-------|----------|
| Feature flags: discovery limited to `[Launch Market]` | Engineering | ☐ |
| On-call rotation active (Eng, Trust, Support) | All | ☐ |
| `#launch-war-room` channel staffed | Launch Lead | ☐ |
| Executive dashboard live — [Dashboards](../analytics/dashboards.md) | Analytics | ☐ |

---

## Workflow

### Step 1 — Launch day standup (T-0 morning)

1. Launch Lead confirms go/no-go with Trust, Support, Engineering, CS leads.
2. Review overnight queue depth: verification, moderation, support.
3. Confirm on-call contacts posted in `#launch-war-room`.
4. No-go criteria: unresolved P0 from pre-launch checklist, payment smoke test failure, verification SLA staffing gap.

### Step 2 — Soft launch monitoring (hours 0–72)

| Monitor | Threshold | Action |
|---------|-----------|--------|
| Verification queue depth | > 2× SLA backlog | Trust Lead adds staff; pause creator acquisition ads |
| Support ticket volume | > 2× forecast | Support Lead activates overflow macros; escalate P1 patterns |
| Payment failure rate | > 2% checkout attempts | Engineering IC; consider checkout disable |
| Trust incidents | Any P0 food safety | [Food Safety Incident SOP](food-safety-incident-sop.md) |
| Platform error rate | > 1% 5xx | Engineering `#incidents` |
| First orders completing | < 3 in 48h | Creator Success outreach to founding cohort |

Hourly checkpoint in `#launch-war-room` for first 48 hours.

### Step 3 — Public launch go/no-go (soft launch exit)

Launch Lead confirms with Executive Sponsor:

| Criterion | Source |
|-----------|--------|
| Verified GMV threshold met | [Launch Plan — Soft launch exit](../growth/launch-plan.md) |
| Trust incident rate within guardrails | [Trust Metrics](../product/success-metrics-overview.md#trust-metrics) |
| Support SLA adherence ≥ target | Support dashboard |
| No open P0 incidents | T&S + Engineering |
| Legal counsel sign-off for public marketing claims | Legal + Marketing |

**No-go:** Extend soft launch; do not scale paid acquisition.

### Step 4 — Public launch execution

1. Marketing activates full channel mix per [Acquisition Channels](../growth/acquisition-channels.md).
2. Trust increases verification staffing 1.5× forecast for 2 weeks.
3. Support extends hours per `TODO(decision):` support hours by market.
4. Daily executive readout: Verified GMV, active verified creators, dispute rate, NPS sample.

### Step 5 — Rollback

| Condition | Action | Authority |
|-----------|--------|-----------|
| Payment integrity failure | Disable checkout; preserve orders in flight | Engineering Lead + Launch Lead |
| Verification bypass discovered | Freeze new creator approvals; audit queue | Trust Lead |
| Food safety P0 cluster | Pause new orders for affected creators | T&S IC |
| Platform outage > 30 min | Status page; comms per Engineering incident response | Engineering IC |

Post-rollback: postmortem within 48 hours; no public relaunch until remediation verified.

---

## AI Responsibilities

| System | Role | Autonomous? |
|--------|------|-------------|
| Verification Assist | Queue prioritization during volume spike | Pre-process only |
| Support Assist | Macro suggestions | Operator confirms |
| Discovery ranking | Verified-only gate | Hard gate — no override |

---

## Human Responsibilities

| Action | Owner |
|--------|-------|
| Go/no-go decisions | Launch Lead + Executive Sponsor |
| Verification SLA during surge | Trust Lead |
| Customer comms during incidents | Support under IC direction |
| Rollback execution | Engineering + Launch Lead |
| Marketing pause during trust crisis | Marketing + Trust Lead |

---

## Escalation Rules

| Condition | Escalate to | Timeline |
|-----------|-------------|----------|
| P0 trust or safety incident | T&S IC | 15 minutes |
| Payment outage | Engineering IC | Immediate |
| Media inquiry on launch | Comms + Legal + Launch Lead | 1 hour |
| Founder decision blocker at go/no-go | Executive Sponsor | Same meeting |

---

## SLA

| Stage | Target |
|-------|--------|
| Launch day standup | T-0 by 9:00 local |
| Hourly war-room updates (first 48h) | On the hour |
| Public launch decision | Within 24h of soft launch exit review |
| Rollback decision | ≤ 30 minutes from trigger confirmation |

---

## Audit Logging

| Event | Record |
|-------|--------|
| Go/no-go decisions | Launch Lead rationale in `#launch-war-room` + ADR if scope change |
| Rollback | Engineering incident ticket + Launch Lead sign-off |
| Staffing changes | Trust/Support lead notes |

---

## Resolution

Launch phase closes when: public launch criteria met and sustained for 2 weeks, or soft launch extended with documented plan.

Hand off to steady-state ops: [Platform Admin SOP](platform-admin-sop.md), [Customer Success lifecycle](../docs/customer-success/customer-lifecycle.md).

---

## Post Mortem

Required after: any rollback, P0 incident during launch window, or missed liquidity targets causing launch delay > 2 weeks.

---

## Metrics

| Metric | Launch target (indicative) |
|--------|---------------------------|
| Verified creators with live listings | Per [Launch Plan](../growth/launch-plan.md) |
| First orders (soft launch) | ≥ founding cohort activation |
| Verification SLA adherence | ≥ 95% |
| Support first response | Per [Support Playbook](../support/support-playbook.md) |
| Trust incident rate | Within guardrails |

→ [Launch Plan — Success criteria](../growth/launch-plan.md)

---

## Future Automation

- Automated launch dashboard with go/no-go signal aggregation
- Queue depth alerting with auto-staffing notifications
- Feature flag orchestration tied to launch phase ADR

---

## Related Documents

- [Launch Plan](../growth/launch-plan.md)
- [Go-to-Market Strategy](../growth/go-to-market-strategy.md)
- [Launching a New Market](../docs/playbooks/launching-new-market.md)
- [Platform Admin SOP](platform-admin-sop.md)
- [Verification Review SOP](verification-review-sop.md)
- [Build Readiness](../roadmap/build-readiness.md)
