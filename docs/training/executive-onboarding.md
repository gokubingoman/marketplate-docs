# Executive Onboarding

> Onboarding guide for founders, executives, and senior leadership. **What to do** and **why** Marketplate is governed this way.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Executive Team  
**Audience:** C-suite, VPs, founders, board observers with operational access

Index: [Employee Training](README.md)

---

## Role Purpose

Executive leadership sets direction, resolves `TODO(decision):` blockers, and models the company's values — especially when trust and growth conflict.

**Why this governance exists:** Marketplate is building infrastructure for independent food creators over a decade, not optimizing for the next quarter's GMV. The [Founding Constitution](../../company/constitution.md) exists so decisions remain consistent when founders are not in the room — and so AI agents and new leaders inherit the same context.

Your job is not to bypass process. It is to **clarify tradeoffs**, approve exceptions with documentation, and protect the trust thesis.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | [Founding Constitution](../../company/constitution.md) (full read) | Authoritative governance model |
| **1** | [Mission](../../company/mission.md) · [Vision](../../company/vision.md) · [Values](../../company/values.md) | Decision sequence internalized |
| **2** | [Company Philosophy](../../company/company-philosophy.md) (all sections) | Cross-domain frameworks |
| **2** | [Executive Summary](../internal/executive-summary.md) · [Company Overview](../internal/company-overview.md) | External-facing narrative alignment |
| **3** | [Product Overview](../../product/overview.md) + [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Product identity and invariants |
| **3** | [Success Metrics](../../product/success-metrics-overview.md) | North star and trust metrics |
| **4** | [Admin Dashboard](../../pages/admin/admin-dashboard.md) + platform health tour | Operational pulse |
| **5** | [Phased Rollout](../../roadmap/phased-rollout.md) + documentation repo tour | Institutional memory model |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Founding Constitution](../../company/constitution.md) | Single governing reference |
| [Company Philosophy](../../company/company-philosophy.md) | How teams decide without you |
| [Market Context](../../company/market-context.md) | Category positioning vs delivery apps |
| [Product Overview](../../product/overview.md) | What we build and refuse to build |
| [Marketplace Mechanics](../../product/marketplace-mechanics.md) | Trust model — your non-negotiables |
| [Success Metrics](../../product/success-metrics-overview.md) | How success is measured |
| [Partner Handbook](../internal/partner-handbook.md) | Internal operating norms |

### Ongoing (leadership depth)

| Document | Why |
|----------|-----|
| [Brand Strategy](../../brand/brand-strategy.md) | External expression of mission |
| [Engineering Architecture Overview](../../engineering/architecture-overview.md) | Technical scale and risk |
| [AI Platform README](../../ai/README.md) | AI governance and human-in-the-loop |
| [Marketplate Standards](../standards/marketplate-standards.md) | Company-wide quality manual |
| [decisions/](../../decisions/) | ADR history — read before reversing |
| [docs/playbooks/](../playbooks/) | Incident and launch orchestration |

---

## Systems Access

| System | Access level | Purpose |
|--------|--------------|---------|
| **Admin dashboard** | Read (executive view) | Trust metrics, queue health |
| **Analytics / BI** | Full | North star, unit economics, trust KPIs |
| **Documentation repo** | Write | ADR approval, constitution updates |
| **Platform settings** | Executive override (audited) | Exceptional threshold changes |
| **Incident channel** | Member | `#incidents` — trust-impacting events |
| **Board / investor materials** | Via [Executive Summary](../internal/executive-summary.md) | Consistent external narrative |

Minimize production write access — use break-glass protocol with audit when required.

---

## Decision Framework

### Values sequence (when tradeoffs conflict)

From [Values — Using Values in Decisions](../../company/values.md#using-values-in-decisions):

1. **Trust check** — Verification, safety, transparency
2. **Creator check** — Durable businesses for independent food entrepreneurs
3. **Clarity check** — Reduce uncertainty for users and teammates
4. **Long-term check** — Still correct at 10× scale?

If still unresolved → executive decision with ADR. **Do not silently compromise trust.**

### Founder decision queue (`TODO(decision):`)

Teams prefix blockers requiring executive input. Your Week 1 goal: find open `TODO(decision):` items in repo and resolve or assign.

**Why documented decisions:** Undocumented exceptions become precedent. Precedent erodes trust uniformly.

### Exception approval (trust-impacting)

Time-bounded exceptions (e.g., pilot market with altered verification) require:

- Written ADR with rollback plan
- T&S sign-off
- Customer/creator transparency plan
- Expiration date

### What executives should not do

- Bypass verification for growth targets
- Pressure auto-approve AI thresholds without eval + T&S
- Ship without documentation ("we'll fix docs later")
- Override moderation without audit trail

---

## Escalation

Executives receive escalations that cannot resolve at T&S or functional lead level:

| Category | Your role |
|----------|-----------|
| Trust vs revenue | Decide with trust default; document if exception |
| Legal / regulatory | Partner with counsel; no product launch without clearance |
| Food safety incident | Executive comms; resource allocation |
| Fraud at scale | Authorize containment; customer/creator notification |
| AI model promotion dispute | Arbitrate Product vs T&S with eval data |
| Cross-functional priority | Align roadmap to mission filter |

Playbooks: [Trust & Safety Escalation](../playbooks/trust-safety-escalation.md) · [Launching a New Market](../playbooks/launching-new-market.md)

---

## Success Criteria

### Week 1
- [ ] Deliver all-hands or leadership sync: trust thesis in your own words
- [ ] Resolve or assign every open `TODO(decision):` in assigned domains
- [ ] Complete admin dashboard walkthrough with Ops and T&S leads

### Day 30
- [ ] Weekly trust metric review established (verification TAT, gate violations, incidents)
- [ ] One ADR authored or approved for significant strategic decision
- [ ] Zero undocumented verbal policy overrides to teams

### Day 90
- [ ] Board/investor narrative matches [Executive Summary](../internal/executive-summary.md) and product reality
- [ ] Documentation phase progress aligned to [Phased Rollout](../../roadmap/phased-rollout.md)
- [ ] Post-mortem participation on trust-impacting incident with systemic fix

---

## Related Documents

- [Employee Training](README.md) — All role guides
- [docs/internal/](../internal/)
- [company/](../../company/)
- [product/success-metrics-overview.md](../../product/success-metrics-overview.md)
- [roadmap/phased-rollout.md](../../roadmap/phased-rollout.md)
- [pages/admin/admin-dashboard.md](../../pages/admin/admin-dashboard.md)
