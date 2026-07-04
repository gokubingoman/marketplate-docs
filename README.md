# Marketplate Docs

The institutional memory of Marketplate — the **operating system and trusted commerce platform for independent food businesses**. The marketplace is Phase 1; the company is much larger. See [Company Phases](roadmap/company-phases.md).

This repository is not a passive documentation archive. It is the operating system of the company: the canonical knowledge base for engineers, designers, operators, executives, investors, and AI agents.

## Start Here

| Document | Purpose |
|----------|---------|
| [Founding Constitution](company/constitution.md) | Governing principles, quality bar, and required structure for all documentation |
| [AI Contributor Constitution](company/ai-contributor-constitution.md) | How AI agents must think and reason on this project |
| [Phased Rollout](roadmap/phased-rollout.md) | Documentation roadmap across five phases |
| [Company Phases](roadmap/company-phases.md) | **15-phase company roadmap** — marketplace is Phase 1 only |
| [Product Roadmap](roadmap/product-roadmap.md) | Supplementary future capability detail |
| [Build Readiness](roadmap/build-readiness.md) | What's ready vs missing before launch |
| [Documentation Gaps](roadmap/documentation-gaps.md) | Phase 5 QA — completeness audit and readiness scores |
| [Architecture Decisions](decisions/) | 8 Proposed ADRs — founder decisions with options analysis |
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

### Playbook Expansion (`docs/`)

| Folder | Index |
|--------|-------|
| [Docs Hub](docs/) | Onboarding, internal, standards, help center, CS, training, playbooks |
| [Creator Onboarding](docs/onboarding/) | Welcome package, checklist, success guide |
| [Internal](docs/internal/) | Company overview, executive summary, partner handbook |
| [Standards](docs/standards/) | Master standards, chef quality, trust & safety |
| [Help Center](docs/help-center/) | 22 production articles + architecture |
| [Customer Success](docs/customer-success/) | Lifecycle, retention, education, metrics |
| [Training](docs/training/) | 9 role-based employee onboarding guides |
| [Playbooks](docs/playbooks/) | 8 cross-functional operational playbooks |

### Phase 2 Documents

| Folder | Index |
|--------|-------|
| [Pages](pages/) | IA, navigation, 4 user flows, 37 page specs |
| [Design System](design-system/) | Foundations + 8 component specifications |

### Phase 5 Documents

| Folder | Index |
|--------|-------|
| [Legal](legal/) | ToS, privacy, creator agreement, food commerce compliance, refund policy |
| [Analytics](analytics/) | Metrics definitions, event taxonomy, dashboards, data governance |
| [Growth](growth/) | GTM strategy, acquisition channels, brand marketing, launch plan |
| [Research](research/) | Competitive landscape, market analysis |

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
| `roadmap/` | Product roadmap, build readiness, documentation phases | Ongoing |
| `decisions/` | Architecture Decision Records (ADRs) | Ongoing |
| `templates/` | Reusable document templates | Ongoing |
| `prompts/` | Agent prompts and AI context | Ongoing |
| `assets/` | Images, logos, media | Ongoing |
| `docs/` | Onboarding, standards, help center, training, playbooks | Expansion |

## Phase Status

| Phase | Name | Status |
|-------|------|--------|
| 1 | Foundation — company, brand, product | **Complete** |
| 2 | Design & UX — design system, IA, pages | **Complete** |
| 3 | Engineering — architecture, APIs, infrastructure | **Complete** |
| 4 | Operations — SOPs, support, trust & safety | **Complete** |
| 5 | Launch — legal, security, analytics, growth, research, QA | **Complete** |

## Documentation Philosophy

- Documentation is production code. Incomplete documentation means the feature is incomplete.
- Documentation precedes implementation.
- Prefer linking between documents over duplicating information.
- Every document must be understandable by humans and AI agents.

## Contributing

All documentation must conform to the [Founding Constitution](company/constitution.md) and use the appropriate template from [`templates/`](templates/).

Significant decisions require an ADR in [`decisions/`](decisions/) using [`templates/adr-template.md`](templates/adr-template.md).
