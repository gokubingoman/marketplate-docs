# Marketplate Docs

The institutional memory of Marketplate — the trusted marketplace and operating system for independent chefs and local food creators.

This repository is not a passive documentation archive. It is the operating system of the company: the canonical knowledge base for engineers, designers, operators, executives, investors, and AI agents.

## Start Here

| Document | Purpose |
|----------|---------|
| [Founding Constitution](company/constitution.md) | Governing principles, quality bar, and required structure for all documentation |
| [Phased Rollout](roadmap/phased-rollout.md) | Documentation roadmap across five phases |
| [Product Overview](product/overview.md) | What Marketplate is — and what it is not |
| [Information Architecture](pages/information-architecture.md) | Site map and page inventory (37 screens) |

### Phase 1 Documents

| Folder | Index |
|--------|-------|
| [Company](company/) | Mission, vision, values, philosophy, glossary |
| [Brand](brand/) | Strategy, positioning, voice, naming |
| [Product](product/) | Overview, personas, marketplace mechanics, metrics |

### Phase 3 Documents

| Folder | Index |
|--------|-------|
| [Engineering](engineering/) | Architecture, 5 API docs, data model, 7 service specs |
| [AI](ai/) | 4 AI systems + platform overview |

### Phase 2 Documents

| Folder | Index |
|--------|-------|
| [Pages](pages/) | IA, navigation, 4 user flows, 37 page specs |
| [Design System](design-system/) | Foundations + 8 component specifications |

## Repository Structure

| Folder | Purpose | Phase |
|--------|---------|-------|
| `company/` | Mission, vision, values, philosophy, glossary | 1 — Foundation |
| `brand/` | Brand strategy, positioning, voice and tone | 1 — Foundation |
| `design-system/` | Design principles, foundations, components | 1–2 |
| `product/` | Product overview, personas, marketplace mechanics | 1 — Foundation |
| `pages/` | Page specifications (every screen) | 2 — Design & UX |
| `engineering/` | Architecture, APIs, infrastructure | 3 — Engineering |
| `operations/` | SOPs, workflows, internal tooling | 4 — Operations |
| `ai/` | AI systems, prompts, evaluation | 3–4 |
| `legal/` | Compliance, policies, terms | 5 — Launch |
| `support/` | Customer support playbooks | 4 — Operations |
| `analytics/` | Metrics, dashboards, data definitions | 5 — Launch |
| `growth/` | Marketing, acquisition, retention | 5 — Launch |
| `research/` | Competitive analysis, user research | 5 — Launch |
| `inspiration/` | Reference products, design inspiration | Ongoing |
| `roadmap/` | Product and documentation roadmaps | Ongoing |
| `decisions/` | Architecture Decision Records (ADRs) | Ongoing |
| `templates/` | Reusable document templates | Ongoing |
| `prompts/` | Agent prompts and AI context | Ongoing |
| `assets/` | Images, logos, media | Ongoing |
| `diagrams/` | Architecture and flow diagrams | Ongoing |

## Phase Status

| Phase | Name | Status |
|-------|------|--------|
| 1 | Foundation — company, brand, product | **Complete** |
| 2 | Design & UX — design system, IA, pages | **Complete** |
| 3 | Engineering — architecture, APIs, infrastructure | **Complete** |
| 4 | Operations — SOPs, support, trust & safety | Not started |
| 5 | Launch — legal, analytics, roadmap, QA | Not started |

## Documentation Philosophy

- Documentation is production code. Incomplete documentation means the feature is incomplete.
- Documentation precedes implementation.
- Prefer linking between documents over duplicating information.
- Every document must be understandable by humans and AI agents.

## Contributing

All documentation must conform to the [Founding Constitution](company/constitution.md) and use the appropriate template from [`templates/`](templates/).

Significant decisions require an ADR in [`decisions/`](decisions/) using [`templates/adr-template.md`](templates/adr-template.md).
