# Employee Training

> Role-based onboarding for Marketplate employees. Every guide explains **what to do** and **why** the company operates that way — grounded in the [Founding Constitution](../../company/constitution.md) and [Company Philosophy](../../company/company-philosophy.md).

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** People & Operations

---

## Purpose

This folder is the canonical entry point for new hires. It connects company principles to daily work: which docs to read, which systems to access, how to decide, when to escalate, and what success looks like in the first 30 days.

Training docs complement — not duplicate — [internal documentation](../internal/), [company standards](../standards/), and domain specs in [engineering/](../../engineering/), [product/](../../product/), and [ai/](../../ai/).

---

## Before You Start (All Roles)

Every employee reads these in Week 1, regardless of function:

| Priority | Document | Why |
|----------|----------|-----|
| 1 | [Founding Constitution](../../company/constitution.md) | Governing principles for product, engineering, design, operations, trust, and AI |
| 2 | [Company Philosophy](../../company/company-philosophy.md) | Decision frameworks when philosophies apply or conflict |
| 3 | [Values](../../company/values.md) | Behavioral norms — trust wins when values conflict |
| 4 | [Mission](../../company/mission.md) · [Vision](../../company/vision.md) | Why Marketplate exists and where it is going |
| 5 | [Glossary](../../company/glossary.md) | Canonical terminology — use it in tickets, docs, and customer communication |
| 6 | [Product Overview](../../product/overview.md) | What we build and what we explicitly do not build |
| 7 | [Marketplace Mechanics](../../product/marketplace-mechanics.md) | How trust, discovery, transactions, and fulfillment work as a system |

Optional but recommended for context: [Company Overview](../internal/company-overview.md) · [Partner Handbook](../internal/partner-handbook.md) · [Marketplate Standards](../standards/marketplate-standards.md)

---

## Role Onboarding Guides

| Role | Guide | Primary surfaces |
|------|-------|------------------|
| **Customer Support** | [Support Onboarding](support-onboarding.md) | Help center, tickets, creator/customer context |
| **Marketplace Operations** | [Operations Onboarding](operations-onboarding.md) | Admin dashboard, queues, SLAs, creator lifecycle |
| **Product** | [Product Onboarding](product-onboarding.md) | Specs, personas, page docs, roadmap |
| **Engineering** | [Engineering Onboarding](engineering-onboarding.md) | Services, APIs, data model, observability |
| **Design** | [Design Onboarding](design-onboarding.md) | Design system, page specs, accessibility |
| **Marketplace Moderation** | [Moderation Onboarding](marketplace-moderation-onboarding.md) | Moderation queue, enforcement ladder |
| **Trust & Safety** | [Trust & Safety Onboarding](trust-safety-onboarding.md) | Verification queue, disputes, compliance |
| **Executive / Leadership** | [Executive Onboarding](executive-onboarding.md) | Strategy, metrics, governance, escalation |
| **AI Systems** | [AI Systems Onboarding](ai-systems-onboarding.md) | AI platform, eval pipeline, human-in-the-loop |

---

## Role × Domain Matrix

Use this to see which repo areas matter most in your first month.

| Domain | Support | Ops | Product | Eng | Design | Moderation | T&S | Executive | AI |
|--------|:-------:|:---:|:-------:|:---:|:------:|:----------:|:---:|:---------:|:--:|
| [company/](../../company/) | ●● | ●● | ●● | ●● | ●● | ●● | ●● | ●● | ●● |
| [product/](../../product/) | ● | ●● | ●● | ● | ●● | ● | ●● | ●● | ● |
| [engineering/](../../engineering/) | ● | ● | ● | ●● | ● | ● | ● | ● | ●● |
| [ai/](../../ai/) | ● | ● | ● | ● | ○ | ●● | ●● | ● | ●● |
| [pages/admin/](../../pages/admin/) | ● | ●● | ● | ● | ● | ●● | ●● | ● | ● |
| [design-system/](../../design-system/) | ● | ○ | ● | ● | ●● | ○ | ○ | ● | ○ |
| [docs/standards/](../standards/) | ●● | ●● | ● | ● | ●● | ●● | ●● | ●● | ●● |
| [docs/playbooks/](../playbooks/) | ●● | ●● | ●● | ● | ● | ●● | ●● | ●● | ● |

Legend: ●● = Week 1 priority · ● = read within 30 days · ○ = reference as needed

---

## Shared Operating Principles

These apply to every role. Your onboarding guide shows how they manifest in your work.

### Trust is the product

**Why:** One food safety incident or verification failure damages the entire platform thesis — not just one creator. Generic marketplaces optimize for listings; Marketplate optimizes for **verified, trustworthy supply**.

**What to do:** When unsure, apply the [Trust Decision Tree](../../company/company-philosophy.md#trust-philosophy). Escalate rather than guess on trust-impacting decisions.

### AI recommends; humans approve

**Why:** False-positive verification approvals are food safety risks. False-negative rejections damage livelihoods. AI scales capacity; humans own accountability.

**What to do:** Never bypass human review on verification, moderation, suspension, or policy enforcement. See [AI Philosophy](../../company/constitution.md#ai-philosophy).

### Documentation is production code

**Why:** This repository is institutional memory. Undocumented systems become single points of failure in people, not code.

**What to do:** Spec before build. Link decisions to [ADRs](../../decisions/). Update affected docs when you change behavior.

### Operational excellence is respect

**Why:** Creators bet their livelihood on Marketplate. A delayed verification or silent outage is a business emergency.

**What to do:** Every workflow needs an owner, SLA, and audit trail. Incidents become documentation.

---

## Escalation Overview

| Scenario | First contact | Escalate to |
|----------|---------------|-------------|
| Food safety report or illness allegation | Support or Moderation | [Trust & Safety Escalation](../playbooks/trust-safety-escalation.md) → T&S lead |
| Verification fraud or identity mismatch | Verification reviewer | T&S lead + [Fraud Response](../playbooks/fraud-response.md) |
| Creator payout or payment dispute | Support or Ops | Ops lead → [Dispute Detail](../../pages/admin/dispute-detail.md) workflow |
| Policy edge case (moderation) | Moderator | T&S lead; legal consult if jurisdiction-specific |
| Product/trust conflict | Any role | T&S + Product; founder if unresolved (`TODO(decision):`) |
| Platform outage or data incident | Engineering on-call | Incident commander → post-mortem doc |
| AI threshold or model promotion | AI Platform | T&S sign-off for trust systems |

Full playbooks: [docs/playbooks/](../playbooks/)

---

## 30-Day Success (All Roles)

By day 30, every employee should be able to:

- [ ] Explain Marketplate's trust thesis in one sentence without reading notes
- [ ] Name their primary persona(s) and anti-persona(s) from [Personas](../../product/personas.md)
- [ ] Navigate their role guide's systems with supervisor oversight
- [ ] Apply their role's decision framework to at least one real scenario
- [ ] Know when and how to escalate — and have done so at least once in training
- [ ] Contribute one documentation improvement (typo fix, link, or SOP gap) to this repo

Role-specific success criteria live in each guide below.

---

## Related Documents

- [Documentation Hub](../README.md) — All extended docs workstreams
- [Onboarding a New Employee](../playbooks/onboarding-new-employee.md) — Cross-functional hire activation playbook
- [Phased Rollout](../../roadmap/phased-rollout.md) — When domain documentation is built
- [Templates](../../templates/) — SOP, feature, page, AI, and ADR templates
