# Marketplate Founding Constitution

> The single governing reference for all documentation, engineering, design, and operations at Marketplate. Every document in this repository must trace back to the principles defined here.

**Status:** Active
**Version:** 1.0
**Last updated:** 2026-07-03

---

## What This Document Is

This is not a README. This is the operating constitution of Marketplate — the set of principles, standards, and structures that govern how we design the company, build the product, operate the business, and maintain institutional memory.

Every engineer, designer, operator, executive, investor, and AI agent working on Marketplate should treat this document as authoritative context.

The verbatim bootstrap prompt lives at [`prompts/founding-constitution.md`](../prompts/founding-constitution.md).

**AI contributors** must also follow the [AI Contributor Constitution](ai-contributor-constitution.md) — how to think and reason, not how to mimic any individual.

---

## About Marketplate

Marketplate is building the **trusted marketplace and operating system for independent chefs** and local food creators.

We are **not** another Uber Eats, DoorDash, or restaurant ordering platform. We are infrastructure — the software layer that allows independent chefs, meal prep businesses, bakers, caterers, food trucks, cottage food operators, pop-up kitchens, commercial kitchens, and local food creators to build **trusted businesses**.

### Mission

Empower independent food entrepreneurs with world-class software.

### The Trust Thesis

**Trust is our product. Software enables trust.**

Customers should feel they are buying from verified creators, not anonymous sellers. Every system, screen, workflow, and policy must reinforce this thesis.

---

## Core Philosophies

### Product Philosophy

Every decision optimizes for: **Trust · Quality · Clarity · Long-term scalability · Beautiful design · Operational excellence · AI-first workflows · Documentation-first development · Maintainability · Human-centered experiences**

- Avoid complexity and feature bloat
- Build fewer things; build them exceptionally well
- Target quality bar: if Apple, Airbnb, Stripe, and Etsy collaborated on a food marketplace, the result should feel like Marketplate

→ Elaborated in [company-philosophy.md](company-philosophy.md)

### Documentation Philosophy

**Documentation is production code.** Incomplete documentation means the feature is incomplete.

| Principle | Meaning |
|-----------|---------|
| Documentation precedes implementation | Spec before code |
| Traceability | Every engineering decision links back to documentation |
| Dual audience | Understandable by humans and AI agents |
| Link, don't duplicate | Prefer cross-references over repeated content |
| Evergreen | Written for years of consumption |
| Related systems | Every page references connected systems |

Templates live in [`templates/`](../templates/).

### Engineering Philosophy

Optimize for **readability, maintainability, and modularity**. Prefer boring technology over clever technology.

- Every service owns one responsibility
- Every API documented before implementation
- Every module independently testable
- Every feature observable — logged, measurable, versioned, documented

→ Engineering docs in Phase 3: [`engineering/`](../engineering/)

### Design Philosophy

Interfaces should feel **calm**. Whitespace is a feature. Motion communicates state. Consistency builds trust.

- One primary action per screen
- Premium feel: large photography, minimal interface
- Accessibility first
- Responsive across desktop, tablet, and mobile — never design for one breakpoint

→ Design system: [`design-system/`](../design-system/)

### Operations Philosophy

Every customer interaction should **reduce uncertainty**. Every incident becomes documentation. Every SOP should eventually become partially automated.

- AI assists; humans remain accountable
- Measurable SLAs on every workflow
- Complete audit trails

→ Operations docs in Phase 4: [`operations/`](../operations/)

### Trust Philosophy

Trust is non-negotiable. Never sacrifice trust for growth.

| Pillar | Requirement |
|--------|-------------|
| Food safety | Non-negotiable compliance and verification |
| Identity verification | Creators are real, verified people |
| Kitchen verification | Production environments are verified |
| Transparency | Customers see what they need to trust |
| Reviews & community | Social proof and accountability |

→ Marketplace trust model: [`product/marketplace-mechanics.md`](../product/marketplace-mechanics.md)

### AI Philosophy

AI should **not replace people**. AI removes repetitive work, improves consistency, proactively detects problems, and assists internal teams.

**AI recommends. Humans approve.**

Every AI system must document: Purpose · Inputs · Outputs · Prompt Strategy · Evaluation · Fallbacks · Confidence Thresholds · Security · Human Review · Continuous Improvement

Template: [`templates/ai-doc-template.md`](../templates/ai-doc-template.md)

---

## Repository Purpose

This repository is Marketplate's **institutional memory**. It must eventually contain everything required to:

- Design, build, and operate the company
- Support customers and scale internationally
- Train employees and guide AI agents
- Support investors and legal reviews
- Generate engineering specs, product requirements, support docs, marketing docs, and roadmaps

---

## Required Repository Structure

```
/company          Mission, vision, values, philosophy
/brand            Brand strategy, positioning, voice
/design-system    Principles, foundations, components
/product          Product strategy, personas, mechanics
/pages            Page specifications (every screen)
/engineering      Architecture, APIs, infrastructure
/operations       SOPs, workflows
/ai               AI systems and prompts
/legal            Compliance, policies
/support          Customer support playbooks
/analytics        Metrics, dashboards
/growth           Marketing, acquisition
/research         Competitive analysis
/inspiration      Reference products
/roadmap          Product and documentation roadmaps
/decisions        Architecture Decision Records
/templates        Reusable document templates
/prompts          Agent prompts and AI context
/assets           Images, logos, media
/diagrams         Architecture and flow diagrams
```

Rollout plan: [`roadmap/phased-rollout.md`](../roadmap/phased-rollout.md)

---

## Document Standards

### Feature Documents

Must contain: Purpose · Business Context · Vision · Requirements · User Experience · Desktop/Tablet/Mobile Experience · Accessibility · Engineering Architecture · Security · Analytics · Operations · Customer Support · Future Expansion · Dependencies · Open Questions · Related Documents · Decision References

Template: [`templates/feature-doc-template.md`](../templates/feature-doc-template.md)

### Page Documents

Must contain: Purpose · Goals · Target User · Navigation · Layout · Components · Interactions · Animations · Responsive Behaviour · Loading/Error/Empty States · Permissions · Analytics · Accessibility · SEO · Future Improvements · API Requirements · Related Pages

Template: [`templates/page-doc-template.md`](../templates/page-doc-template.md)

### Standard Operating Procedures

Must contain: Purpose · Trigger · Owner · Prerequisites · Workflow · AI Responsibilities · Human Responsibilities · Escalation Rules · SLA · Audit Logging · Resolution · Post Mortem · Metrics · Future Automation

Template: [`templates/sop-template.md`](../templates/sop-template.md)

### Engineering Documents

Must contain: Purpose · Architecture · Dependencies · Services · Data Flow · Failure Modes · Monitoring · Logging · Security · Testing · Scaling Strategy · Disaster Recovery · Future Improvements

Template: [`templates/engineering-doc-template.md`](../templates/engineering-doc-template.md)

### AI System Documents

Must contain: Purpose · Problem Statement · Inputs · Outputs · Models · Prompt Strategy · Evaluation · Confidence Thresholds · Fallback Behaviour · Security · Human Approval · Monitoring · Continuous Improvement

Template: [`templates/ai-doc-template.md`](../templates/ai-doc-template.md)

### Architecture Decision Records

Every significant decision receives an ADR with: Decision · Background · Reasoning · Alternatives · Tradeoffs · Impact · Status · Date · Related Documents

Template: [`templates/adr-template.md`](../templates/adr-template.md) · Folder: [`decisions/`](../decisions/)

---

## Quality Bar

Nothing should resemble placeholder documentation or generic AI output.

Every document must read as if written by an experienced principal engineer, product leader, and technical writer working together.

| Do | Don't |
|----|-------|
| Challenge assumptions | Accept "good enough" |
| Identify missing requirements and edge cases | Optimize only for launch |
| Design for the next decade | Duplicate information across docs |
| Remove unnecessary complexity | Leave vague TODOs without `TODO(decision):` prefix |
| Cross-reference related systems | Write in isolation from other domains |

Use `TODO(decision):` **only** when blocked by an explicit business decision that requires founder or executive input.

---

## Sub-Agent Execution Model

Documentation is built in **phases** using parallel specialist agents. Each agent owns a domain, cross-references existing docs, avoids duplication, and produces implementation-ready Markdown.

| Phase | Focus | Key Agents |
|-------|-------|------------|
| 1 — Foundation | Company, brand, product | Company & Vision · Brand & Design System · Product & Marketplace |
| 2 — Design & UX | IA, every page | UX & IA · Page Specification |
| 3 — Engineering | Architecture, APIs, AI | Engineering Architecture · Backend Systems · AI Platform |
| 4 — Operations | SOPs, support, trust | Operations · Support · Trust & Safety · Super Admin |
| 5 — Launch | Legal, analytics, QA | Legal · Security · Analytics · Growth · Research · Documentation QA |

Agent prompts: [`prompts/phase-agent-prompts.md`](../prompts/phase-agent-prompts.md)

---

## Related Documents

- [Mission](mission.md)
- [Vision](vision.md)
- [Values](values.md)
- [Company Philosophy](company-philosophy.md)
- [Product Overview](../product/overview.md)
- [Phased Rollout](../roadmap/phased-rollout.md)
- [README](../README.md)
