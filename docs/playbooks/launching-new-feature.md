# Launching a New Feature

> End-to-end operational playbook for docs-first feature rollout across product, engineering, trust, operations, and support.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Playbook type:** Cross-functional orchestration

---

## Purpose

This playbook orchestrates **feature launch** from specification through production rollout, operational readiness, and post-launch measurement. Marketplate follows a docs-first culture: [Documentation Is Production Code](../company/values.md#6-documentation-is-production-code). A feature is not done until pages, engineering services, operations SOPs (where applicable), Help content, and training are aligned.

This is not a deployment runbook alone. It coordinates Product, Engineering, Design, Trust & Safety, Operations, Support, and Analytics — with explicit trust impact review for any customer- or creator-facing change.

**Governing bar:** [Quality Over Volume](../company/values.md#2-quality-over-volume) — cut scope before cutting quality.

---

## Trigger

| Trigger | Example |
|---------|---------|
| **Roadmap commitment** | Feature approved for quarter |
| **ADR decision** | Architectural change requiring new user-facing capability |
| **Regulatory requirement** | Compliance field added to verification flow |
| **Trust gap remediation** | Allergen acknowledgment enhancement at checkout |
| **Creator OS improvement** | Batch production view for meal prep |

**Gate 0:** Feature has named PM owner, engineering lead, and trust impact classification (none / low / medium / high).

---

## Stakeholders

| Role | Team | Responsibility |
|------|------|----------------|
| **Product Manager** | Product | Spec, rollout plan, go/no-go |
| **Engineering Lead** | Engineering | Implementation, deploy, monitoring |
| **Designer** | Design | Page specs, design system compliance |
| **Trust & Safety Lead** | Trust & Safety | Trust impact review (medium/high) |
| **Legal** | Legal | Terms/policy updates if needed |
| **Operations** | Ops | SOP updates for operator-facing changes |
| **Support Lead** | Support | Help articles, agent macros, training |
| **Marketing** | Marketing | Release comms (if customer-visible) |
| **Analytics** | Data | Event taxonomy, dashboard, success metrics |
| **AI Platform** | Engineering | AI system updates if feature touches trust/discovery |

---

## Prerequisites

Before development starts:

| Prerequisite | Owner |
|--------------|-------|
| Feature brief linked to [Product Overview](../../product/overview.md) pillar(s) | PM |
| Trust impact classification documented | PM + Trust Lead |
| Page spec(s) drafted in `pages/` | Design + PM |
| API changes spec'd in `engineering/api/` if applicable | Engineering |
| ADR for significant architectural decisions | Engineering |
| Success metrics defined | PM + Analytics |
| Rollout strategy chosen: flag · phased · big-bang | PM + Engineering |
| `TODO(decision):` items flagged for founder input — not silently deferred | PM |

**Trust impact classification:**

| Level | Examples | Required review |
|-------|----------|-----------------|
| **None** | Internal admin tooling cosmetic | Engineering only |
| **Low** | Creator dashboard UX improvement, no trust data change | PM + Design |
| **Medium** | New listing field, checkout step change | + Trust Lead + Support |
| **High** | Verification flow change, ranking factor, enforcement action | + Legal, full playbook, staged rollout |

---

## Phase-by-Phase Execution

### Phase 1 — Specify (1–3 weeks)

| Step | Actor | Action | Artifact |
|------|-------|--------|----------|
| 1.1 | PM | Write feature brief: problem, scope, out-of-scope, personas | Product doc |
| 1.2 | PM + Design | Page spec(s) per [Pages README](../../pages/README.md) | `pages/[domain]/[page].md` |
| 1.3 | PM | Update or reference flow doc if journey changes | `pages/flows/` |
| 1.4 | Engineering | Service design, API endpoints, events | `engineering/services/`, `engineering/api/` |
| 1.5 | Trust Lead (medium/high) | Trust impact memo: verification, transparency, enforcement implications | Linked from spec |
| 1.6 | Analytics | Event taxonomy additions | `analytics/` |
| 1.7 | PM | Review against [Design Principles](../../design-system/principles.md) and [Anti-patterns](../../product/marketplace-mechanics.md#anti-patterns-explicitly-rejected) | Checklist sign-off |

**Exit criteria:** Spec review approved by PM, Eng Lead, Design; Trust Lead for medium/high.

---

### Phase 2 — Build (sprint-dependent)

| Step | Actor | Action |
|------|-------|--------|
| 2.1 | Engineering | Implement behind feature flag (default off in production) |
| 2.2 | Engineering | Unit + integration tests; E2E for trust-critical paths |
| 2.3 | Design | Design system components; accessibility review |
| 2.4 | AI Platform (if applicable) | Model/prompt updates through eval pipeline — [AI Platform](../../ai/README.md) |
| 2.5 | PM | Iterate against spec; scope cuts documented |
| 2.6 | Engineering | Observability: logs, metrics, alerts per service doc standards |

**Trust-critical features additionally require:**

- Human approval paths preserved — no auto-approve regression
- Audit log emission for mutating actions
- AI assist boundaries documented if ML involved

→ [Trust Service testing standards](../../engineering/services/trust-service.md#testing)

---

### Phase 3 — Operational Readiness (1–2 weeks pre-launch)

| Step | Actor | Action | Artifact |
|------|-------|--------|----------|
| 3.1 | Ops (medium/high trust) | Draft or update SOP in `operations/` | Future Phase 4 SOP |
| 3.2 | Support | Help article draft; update FAQ embeddings for Support Assist | `/help` |
| 3.3 | Support | Agent training session + macro updates | Support wiki |
| 3.4 | Trust Ops (if admin UI) | Operator training on new queue/checklist fields | Training recording |
| 3.5 | Legal (if needed) | Terms, seller agreement, refund policy updates | `legal/` |
| 3.6 | Marketing (if customer-visible) | Release notes, email draft, in-app announcement copy | Comms doc |
| 3.7 | PM | **Launch readiness review** — all rows in checklist below green | Sign-off doc |

**Launch readiness checklist:**

- [ ] Page spec matches implemented UI
- [ ] API docs updated
- [ ] Flow doc updated if journey changed
- [ ] Feature flag configured in staging and production
- [ ] Monitoring and alerts configured
- [ ] Help article published or scheduled
- [ ] Support team trained
- [ ] Trust ops trained (if applicable)
- [ ] Analytics events verified in staging
- [ ] Rollback plan documented
- [ ] Legal sign-off (if applicable)

---

### Phase 4 — Staged Rollout

| Step | Actor | Action |
|------|-------|--------|
| 4.1 | Engineering | Deploy to staging; QA sign-off |
| 4.2 | PM + Eng | Enable flag for internal dogfood (employees) |
| 4.3 | PM | Beta cohort if applicable (selected creators/customers) |
| 4.4 | Data | Monitor feature metrics and error rates |
| 4.5 | Trust Lead (high) | Shadow period for AI/trust changes — min 48h per [AI Platform](../../ai/README.md) |
| 4.6 | PM | Go/no-go for general availability |

**Rollout patterns:**

| Pattern | Use when |
|---------|----------|
| **Feature flag %** | Low-risk UX improvements |
| **Creator beta → GA** | Creator OS changes |
| **Market-scoped flag** | Geographic feature — see [Launching a New Market](launching-new-market.md) |
| **Big-bang** | Bug fixes, required compliance changes — with comms |

---

### Phase 5 — General Availability & Comms

| Step | Actor | Action |
|------|-------|--------|
| 5.1 | Engineering | Enable feature flag at 100% (or target %) |
| 5.2 | Marketing | Ship release comms per plan |
| 5.3 | Support | Monitor ticket volume spike; war room if high-trust feature |
| 5.4 | PM | Announce in #product-releases with doc links |
| 5.5 | PM | Update [Product Overview](../../product/overview.md) or pillar doc if scope changed |

---

### Phase 6 — Post-Launch (2–4 weeks)

| Step | Actor | Action |
|------|-------|--------|
| 6.1 | PM | Measure against success metrics defined in Phase 1 |
| 6.2 | Data | Launch report: adoption, conversion impact, errors |
| 6.3 | PM | Collect support feedback — doc gaps, UX confusion |
| 6.4 | Engineering | Remove flag after stable period; clean up dead code |
| 6.5 | All | Retro if launch had incidents or significant metric miss |

---

## Decision Points

| Decision | Owner | Options | Default |
|----------|-------|---------|---------|
| Ship vs. delay (trust concern) | Trust Lead + PM | Delay · Ship with mitigation · Cut scope | Delay if trust weakened — [Values](../company/values.md#1-trust-is-the-product) |
| Beta vs. direct GA | PM | Beta · GA · Internal only | Beta for high-trust or creator-workflow changes |
| Rollback | Eng on-call + PM | Rollback flag · Hotfix forward | Rollback if P0/P1; hotfix if isolated |
| SOP required | Trust Lead | Yes · No | Yes for any operator workflow change |
| Public announcement | Marketing + PM | Announce · Silent ship | Announce customer-facing trust/commerce changes |
| AI model promote | AI Platform + Trust Lead | Promote · Hold | Hold if eval gate not passed |

---

## Communication Templates

### Template: Internal Launch Announcement

**Channel:** Slack `#product-releases`

```
📦 SHIPPED — [Feature name]

PM: @[name] · Eng: @[name]
Trust impact: [None/Low/Medium/High]

What: [One sentence]
Who: [Creators / Customers / Operators / All]
Docs: [Page spec link] · [Flow link if updated]
Flag: `[flag_name]` — [100% / staged %]
Metrics: [Primary success metric]

Support: Help article [link]
Rollback: Disable `[flag_name]` in [admin tool]
```

### Template: Creator Release Email (significant OS change)

```
Subject: New in your dashboard — [Feature name]

Hi [Creator first name],

We've added [feature] to help you [benefit in plain language].

[What changed — 2–3 bullets]

[Try it now →]

Questions? Visit Help or reply to this email.

— The Marketplate team
```

### Template: Launch Readiness Review Invite

```
Subject: Launch readiness — [Feature name] — [Date]

Attendees: PM, Eng Lead, Design, Trust Lead, Support Lead

Agenda:
1. Demo in staging
2. Launch readiness checklist walk-through
3. Rollback plan review
4. Comms timing
5. Go/no-go decision

Pre-read: [Spec link] · [Trust impact memo if applicable]
```

---

## Metrics

| Metric | Definition | When measured |
|--------|------------|---------------|
| Launch on-time | Actual GA vs. planned | Launch day |
| Defect rate (7d) | P0/P1 bugs filed / feature | 7 days post-GA |
| Adoption rate | Users engaging with feature / eligible users | 14 days post-GA |
| Primary success metric | Defined per feature in spec | 30 days post-GA |
| Support ticket delta | Feature-tagged tickets vs. baseline | 14 days post-GA |
| Doc completeness | Launch checklist items complete at GA | Launch day |
| Rollback events | Count | Ongoing |

---

## Post-Incident / Retro

**Required retro when:**

- P0/P1 incident caused by feature launch
- Rollback executed
- Trust metric regression (false approve rate, dispute rate)
- Support ticket spike > 2× forecast

**Retro outputs:**

- ADR if architectural lesson
- Spec and flow doc updates
- Playbook amendment
- Eval pipeline update for AI features
- Launch readiness checklist item added

---

## Related Documents

### Standards & process
- [Company Values — Documentation Is Production Code](../company/values.md#6-documentation-is-production-code)
- [docs/standards/](../standards/)
- [Design System Principles](../../design-system/principles.md)
- [Brand Voice & Tone](../../brand/voice-and-tone.md)

### Product & pages
- [Product Overview](../../product/overview.md)
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Pages README](../../pages/README.md)
- [Page flows](../../pages/flows/)

### Engineering
- [Engineering README](../../engineering/README.md)
- [Service Catalog](../../engineering/service-catalog.md)
- [Trust Service](../../engineering/services/trust-service.md)

### AI
- [AI Platform — Evaluation pipeline](../../ai/README.md#evaluation-pipeline)

### Related playbooks
- [Launching a New Market](launching-new-market.md)
- [Launching a Creator](launching-a-creator.md)
- [Trust & Safety Escalation](trust-safety-escalation.md)
- [Onboarding a New Employee](onboarding-new-employee.md)
