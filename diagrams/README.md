# Architecture Diagrams

Visual reference diagrams for onboarding engineers, investors, and operators. Source of truth remains text specs in `engineering/` — update diagrams when architecture changes.

**Status:** Active  
**Last updated:** 2026-07-03

---

## Diagram index

| Diagram | Description |
|---------|-------------|
| [System Topology](system-topology.md) | Infrastructure — users, edge, compute, data, external SaaS |
| [Application Surfaces](application-surfaces.md) | Customer, Creator, Admin → API gateway → modules |
| [Trust & Commerce Flows](trust-commerce-flows.md) | Verification path + purchase path (sequence-level) |

---

## Conventions

- **Mermaid** syntax — renders in GitHub, Cursor, and most doc tools
- Diagrams are **simplified** for clarity; see linked service docs for edge cases
- Trust-critical paths marked with note: *human approval required*

---

## Related Documents

- [Architecture Overview](../engineering/architecture-overview.md)
- [Infrastructure Overview](../engineering/infrastructure-overview.md)
- [Data Flow](../engineering/data-flow.md)
- [Implementation Kickoff](../engineering/implementation-kickoff.md)
