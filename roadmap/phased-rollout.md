# Phased Documentation Rollout

This roadmap governs how Marketplate's institutional memory is built. Work proceeds in five phases. Each phase uses parallel specialist agents within its domain before moving to the next.

**Governing document:** [Founding Constitution](../company/constitution.md)

---

## Phase Overview

| Phase | Name | Status | Agents |
|-------|------|--------|--------|
| 1 | Foundation | **Complete** | Company & Vision, Brand & Design System, Product & Marketplace |
| 2 | Design & UX | **Complete** | UX & IA, Page Specification |
| 3 | Engineering | **Complete** | Engineering Architecture, Backend Systems, AI Platform |
| 4 | Operations | Not started | Operations & SOP, Customer Support, Trust & Safety, Super Admin |
| 5 | Launch | Not started | Legal & Compliance, Security & Infrastructure, Analytics & Data, Growth & Marketing, Research & Competitive Analysis, Documentation QA |

---

## Phase 1 — Foundation

**Goal:** Establish company identity, brand foundations, design system primitives, and product strategy.

**Status:** Complete

### Deliverables

| Agent | Folder | Documents |
|-------|--------|-----------|
| Company & Vision | `company/` | mission, vision, values, market-context, company-philosophy, glossary |
| Brand & Design System | `brand/`, `design-system/` | brand strategy, positioning, voice, naming; design principles, color, typography, spacing, accessibility, components overview |
| Product & Marketplace | `product/` | overview, personas, value-props, marketplace-mechanics, success-metrics-overview |

### Exit Criteria

- [x] All Phase 1 documents published and cross-linked
- [x] No contradictions between company, brand, and product docs
- [x] Glossary covers core terms used across Phase 1
- [x] README phase status updated

### Next: Phase 2 Kickoff

Phase 2 requires:

1. **UX & Information Architecture Agent** — site map, navigation model, user flows in `pages/`
2. **Page Specification Agent** — full page specs for every customer-facing and admin screen using `templates/page-doc-template.md`
3. **Design system expansion** — component specs building on `design-system/components-overview.md`

See [prompts/phase-agent-prompts.md](../prompts/phase-agent-prompts.md) for agent prompt scaffolds.

---

## Phase 2 — Design & UX

**Goal:** Complete information architecture and every page specification.

**Status:** Complete

### Deliverables

| Agent | Folder | Documents |
|-------|--------|-----------|
| UX & Information Architecture | `pages/`, `product/` | Site map, navigation model, user flows |
| Page Specification | `pages/` | Full page specs for every customer-facing and admin screen |

### Prerequisites

- Phase 1 complete
- Design system foundations stable enough to reference in page specs

### Exit Criteria

- [x] Every screen has a page spec using `templates/page-doc-template.md`
- [x] IA doc covers all user types and primary journeys
- [x] Components overview expanded into full component specs where needed

### Next: Phase 3 Kickoff

Phase 3 requires:

1. **Engineering Architecture Agent** — system architecture, service catalog, integration patterns in `engineering/`
2. **Backend Systems Agent** — API specs, data models, service docs
3. **AI Platform Agent** — AI system docs per `templates/ai-doc-template.md`

Page specs define API requirements; marketplace mechanics define trust/transaction boundaries.

See [prompts/phase-agent-prompts.md](../prompts/phase-agent-prompts.md).

---

## Phase 3 — Engineering

**Goal:** Architecture, APIs, services, and AI platform documentation.

**Status:** Complete

### Deliverables

| Agent | Folder | Documents |
|-------|--------|-----------|
| Engineering Architecture | `engineering/` | System architecture, service catalog, integration patterns |
| Backend Systems | `engineering/` | API specs, data models, service docs |
| AI Platform | `ai/` | AI system docs per `templates/ai-doc-template.md` |

### Exit Criteria

- [x] Architecture overview, service catalog, integration patterns, infrastructure, data flows documented
- [x] API specs consolidated from page requirements (customer, creator, admin)
- [x] Data model and core entities documented
- [x] Seven service specifications published
- [x] Four AI systems documented with human-approval gates

### Next: Phase 4 Kickoff

Phase 4 requires Operations & SOP, Customer Support, Trust & Safety, and Super Admin agents. Engineering docs define observable systems and audit trails for SOPs.

See [prompts/phase-agent-prompts.md](../prompts/phase-agent-prompts.md).

---

## Phase 4 — Operations

**Goal:** SOPs, support playbooks, trust & safety workflows, admin tooling.

**Status:** Not started

### Deliverables

| Agent | Folder | Documents |
|-------|--------|-----------|
| Operations & SOP | `operations/` | Internal workflow SOPs |
| Customer Support | `support/` | Support playbooks, macros, escalation |
| Trust & Safety | `operations/`, `legal/` | Verification, moderation, food safety |
| Super Admin | `operations/`, `pages/` | Admin tool workflows |

### Prerequisites

- Phase 3 engineering docs define observable systems and audit trails
- Product trust model from Phase 1 informs verification workflows

---

## Phase 5 — Launch

**Goal:** Legal, security, analytics, growth, research, and documentation QA.

**Status:** Not started

### Deliverables

| Agent | Folder | Documents |
|-------|--------|-----------|
| Legal & Compliance | `legal/` | Terms, privacy, regulatory compliance |
| Security & Infrastructure | `engineering/` | Security policies, infrastructure, DR |
| Analytics & Data | `analytics/` | Metrics definitions, dashboards, data governance |
| Growth & Marketing | `growth/` | Acquisition, retention, brand marketing |
| Research & Competitive Analysis | `research/` | Market research, competitive landscape |
| Documentation QA | All | Gap analysis, consistency review |

### Exit Criteria

- [ ] Documentation QA pass complete
- [ ] All cross-links validated
- [ ] Gap report published to `roadmap/documentation-gaps.md`
- [ ] Repository ready as primary context source for implementation

---

## Agent Prompt Reference

See [prompts/phase-agent-prompts.md](../prompts/phase-agent-prompts.md) for reusable prompt scaffolds for each agent.

---

## Related Documents

- [Founding Constitution](../company/constitution.md)
- [Product Overview](../product/overview.md)
- [README](../README.md)
