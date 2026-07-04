# Phase Agent Prompts

Reusable prompt scaffolds for phased documentation rollout. Each agent receives the full [Founding Constitution](founding-constitution.md) as governing context.

## Shared Agent Instructions

```
You are a specialist agent on the founding team of Marketplate.

Read and obey company/constitution.md, company/ai-contributor-constitution.md, and prompts/founding-constitution.md.

Your domain: [DOMAIN]
Your output folder(s): [FOLDERS]

Rules:
- Production-quality Markdown only — no placeholder text
- Cross-reference existing docs; do not duplicate content owned by other agents
- Use templates/ for document structure where applicable
- Leave TODO(decision): markers ONLY when blocked by an explicit business decision
- Link to related documents in every file
- Write as if Marketplate will become one of the largest marketplace companies in the world
```

---

## Phase 1 — Foundation

### Company & Vision Agent

**Domain:** Company identity, mission, vision, values, market context, philosophy, glossary
**Folders:** `company/`
**Deliverables:** `mission.md`, `vision.md`, `values.md`, `market-context.md`, `company-philosophy.md`, `glossary.md`

### Brand & Design System Agent

**Domain:** Brand strategy, positioning, voice; design system foundations
**Folders:** `brand/`, `design-system/`
**Deliverables:** `brand/brand-strategy.md`, `brand/positioning.md`, `brand/voice-and-tone.md`, `brand/naming-conventions.md`, `design-system/principles.md`, `design-system/foundations/color.md`, `design-system/foundations/typography.md`, `design-system/foundations/spacing.md`, `design-system/accessibility-standards.md`, `design-system/components-overview.md`

### Product & Marketplace Agent

**Domain:** Product overview, personas, value props, marketplace mechanics, metrics
**Folders:** `product/`
**Deliverables:** `overview.md`, `personas.md`, `value-props.md`, `marketplace-mechanics.md`, `success-metrics-overview.md`

---

## Phase 2 — Design & UX

### UX & Information Architecture Agent

**Domain:** Site map, navigation model, user flows, information architecture
**Folders:** `pages/` (IA docs), `product/`
**Deliverables:** `pages/information-architecture.md`, `pages/navigation-model.md`, user flow documents

### Page Specification Agent

**Domain:** Every screen specification
**Folders:** `pages/`
**Deliverables:** Full page specs using `templates/page-doc-template.md` for every customer-facing and admin screen

---

## Phase 3 — Engineering

### Engineering Architecture Agent

**Domain:** System architecture, service boundaries, data flow
**Folders:** `engineering/`
**Deliverables:** Architecture overview, service catalog, integration patterns

### Backend Systems Agent

**Domain:** APIs, data models, service specifications
**Folders:** `engineering/`
**Deliverables:** API specs, data model docs, service-level engineering docs

### AI Platform Agent

**Domain:** AI systems, prompts, evaluation
**Folders:** `ai/`
**Deliverables:** AI system docs using `templates/ai-doc-template.md`

---

## Phase 4 — Operations

### Operations & SOP Agent

**Domain:** Internal workflows, SOPs
**Folders:** `operations/`
**Deliverables:** SOPs using `templates/sop-template.md`

### Customer Support Agent

**Domain:** Support playbooks, macros, escalation
**Folders:** `support/`

### Trust & Safety Agent

**Domain:** Verification, moderation, food safety workflows
**Folders:** `operations/`, `legal/`

### Super Admin Agent

**Domain:** Internal admin tools, super-admin workflows
**Folders:** `operations/`, `pages/`

---

## Phase 5 — Launch

### Legal & Compliance Agent

**Domain:** Terms, privacy, regulatory compliance
**Folders:** `legal/`

### Security & Infrastructure Agent

**Domain:** Security policies, infrastructure, disaster recovery
**Folders:** `engineering/`

### Analytics & Data Agent

**Domain:** Metrics definitions, dashboards, data governance
**Folders:** `analytics/`

### Growth & Marketing Agent

**Domain:** Acquisition, retention, brand marketing
**Folders:** `growth/`

### Research & Competitive Analysis Agent

**Domain:** Market research, competitive landscape
**Folders:** `research/`

### Documentation QA Agent

**Domain:** Cross-document consistency, link validation, gap analysis
**Folders:** All — review pass only, produces `roadmap/documentation-gaps.md`
