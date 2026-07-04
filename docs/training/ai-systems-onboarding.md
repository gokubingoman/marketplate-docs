# AI Systems Onboarding

> Onboarding guide for AI Platform engineers and ML engineers building Marketplate's AI systems. **What to do** and **why**.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** AI Platform  
**Reports to:** AI Platform Lead → Engineering

Index: [Employee Training](README.md)

---

## Role Purpose

AI Platform builds systems that **remove repetitive work and improve consistency** — without replacing human accountability on verification, moderation, enforcement, or customer-facing policy answers.

**Why this role exists:** Support volume, verification documents, and moderation reports scale with marketplace growth. AI scales operational capacity. But a false-positive kitchen approval is a food safety risk; a false-negative creator rejection damages a livelihood. **AI recommends; humans approve** is not a slogan — it is an architecture constraint.

Every AI system documents purpose, inputs, outputs, evaluation, fallbacks, confidence thresholds, security, human review, and monitoring before deploy.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | Shared foundation + [AI Philosophy](../../company/constitution.md#ai-philosophy) | Trust impact matrix |
| **1–2** | [AI Platform README](../../ai/README.md) | Platform architecture and eval pipeline |
| **2** | [Verification Assist](../../ai/verification-assist.md) | Highest-stakes system |
| **2–3** | [Moderation Assist](../../ai/moderation-assist.md) | Enforcement assist boundaries |
| **3** | [Support Assist](../../ai/support-assist.md) | Customer-facing retrieval limits |
| **3–4** | [Discovery Ranking](../../ai/discovery-ranking.md) | Trust gates — violation rate must be 0 |
| **4** | [Trust Service](../../engineering/services/trust-service.md) + [Discovery Service](../../engineering/services/discovery-service.md) | Service integration points |
| **5** | [AI doc template](../../templates/ai-doc-template.md) + eval pipeline walkthrough | Documentation standard |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Company Philosophy — AI](../../company/company-philosophy.md#ai-philosophy) | Trust impact → AI role matrix |
| [Values — Humans Decide; AI Assists](../../company/values.md#7-humans-decide-ai-assists) | Behavioral constraint |
| [AI Platform README](../../ai/README.md) | Inference, PII, observability, config |
| All four system docs in [ai/](../../ai/) | Verification, Moderation, Support, Discovery |
| [AI doc template](../../templates/ai-doc-template.md) | Required sections |
| [Trust Verification Flow](../../pages/flows/trust-verification-flow.md) | Human approval gate |

### Week 2–4 (role depth)

| Document | Why |
|----------|-----|
| [Engineering Architecture Overview](../../engineering/architecture-overview.md) | System context |
| [Integration Patterns](../../engineering/integration-patterns.md) | Async pipelines, events |
| [Platform Settings](../../pages/admin/platform-settings.md) | Runtime thresholds |
| [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Trust invariants to encode |
| [Trust & Safety Standards](../standards/trust-and-safety-standards.md) | Policy inputs for classifiers |
| [prompts/](../../prompts/) | Full prompts — not duplicated in ai/ |

### Admin surfaces (your outputs)

| Document | Why |
|----------|-----|
| [Verification Queue](../../pages/admin/verification-queue.md) | AI summary UX |
| [Moderation Queue](../../pages/admin/moderation-queue.md) | Severity/category presentation |
| [Help](../../pages/customer/help.md) | Support Assist retrieval surface |

---

## Systems Access

| System | Access level | Purpose |
|--------|--------------|---------|
| **Inference cluster** | Developer / deploy | Model serving |
| **Embedding / vector index** | Developer | FAQ, semantic search |
| **Eval pipeline** | Developer | Benchmarks, regression gates |
| **Observability dashboards** | View + alert config | Latency, fallback, drift |
| **Trust enclave** | Scoped | Verification docs — PII isolation |
| **Platform settings (AI)** | Read (write: Lead + T&S sign-off) | Threshold tuning |
| **Documentation repo** | Write | System specs, version bumps |
| **prompts/ repo** | Write via review | Prompt changes |

**Security defaults:** No cross-tenant PII batching. Provider zero-retention. No training on production customer data without consent and legal review.

---

## Decision Framework

### Trust impact matrix (authoritative)

From [Company Philosophy — AI](../../company/company-philosophy.md#ai-philosophy):

| Trust Impact | AI Role | Human Role |
|--------------|---------|------------|
| **High** (verification, moderation, compliance) | Recommend + confidence score | Approve/reject every decision |
| **Medium** (support triage, content suggestions) | Draft/classify; auto-act above threshold with audit | Review samples; handle exceptions |
| **Low** (internal search, doc generation) | Auto-act with logging | Periodic eval |

### Build vs buy vs rules

| Prefer | When |
|--------|------|
| **Deterministic rules** | Trust gates, compliance expiry, hard filters |
| **Classifiers with eval** | Moderation categories, document quality |
| **LLM with strict schema** | Extraction, summarization — never sole decision |
| **No AI** | When rules are clearer and auditable |

**Anti-pattern:** Using AI to avoid building clear rules where rules suffice.

### Deploy checklist (blocking)

- [ ] System doc complete per [AI doc template](../../templates/ai-doc-template.md)
- [ ] Offline benchmarks pass regression gate
- [ ] Shadow traffic 48h minimum for trust systems
- [ ] T&S human sign-off for trust-critical promotions
- [ ] Fallback path tested — pipeline never blocks core flows
- [ ] `model_version` on every output
- [ ] PII handling review complete
- [ ] Platform Settings defaults: **no auto-approve verification; no auto-suspend**

### Eval pipeline (follow every time)

```
Label maintenance → Offline benchmarks → Regression gate
→ Shadow traffic (48h+) → Human sign-off (T&S/Product)
→ Promote model_version + doc version bump
→ Online monitoring + weekly sample audit
```

Blocking metrics examples: [AI README — Evaluation](../../ai/README.md#evaluation-pipeline)

---

## Escalation

| Trigger | Escalate to | Action |
|---------|-------------|--------|
| Fallback spike affecting queue SLAs | AI on-call + Trust Ops | Incident; consider rollback |
| Trust gate violation in Discovery | T&S + AI Lead (immediate) | Halt promotion; root cause |
| PII leak suspicion | Security + Legal | Containment protocol |
| Stakeholder requests auto-approve | T&S + Executive | Default deny; ADR if exception |
| Eval regression on harassment recall | T&S before any promote | Safety metric blocking |
| Provider outage | Eng on-call | Confirm fallback path active |

---

## Success Criteria

### Week 1
- [ ] Trace one verification submission through AI pipeline to queue UI
- [ ] Explain eval pipeline and blocking metrics without notes
- [ ] Document one gap or improvement in system doc (PR)

### Day 30
- [ ] Ship change through full eval pipeline with T&S sign-off (if trust-touching)
- [ ] Zero undocumented prompts in production
- [ ] Fallback tested for owned system — documented result

### Day 90
- [ ] Own observability dashboard slice (fallback rate, cost, drift)
- [ ] Lead weekly sample audit rotation with T&S
- [ ] Author ADR for significant model or architecture decision

---

## Related Documents

- [Employee Training](README.md)
- [Trust & Safety Onboarding](trust-safety-onboarding.md) — Sign-off partner
- [Engineering Onboarding](engineering-onboarding.md) — Service integration
- [ai/](../../ai/)
- [engineering/](../../engineering/)
- [pages/admin/platform-settings.md](../../pages/admin/platform-settings.md)
- [docs/standards/](../standards/)
- [templates/ai-doc-template.md](../../templates/ai-doc-template.md)
