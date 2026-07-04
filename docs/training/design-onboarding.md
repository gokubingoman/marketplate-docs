# Design Onboarding

> Onboarding guide for Product Designers and Brand Designers. **What to do** and **why** Marketplate interfaces look and behave this way.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Design  
**Reports to:** Head of Design

Index: [Employee Training](README.md)

---

## Role Purpose

Design makes **trust visible**. Calm, premium, accessible interfaces signal that Marketplate takes creators and food safety seriously — cluttered interfaces signal a cluttered operation.

**Why this role exists:** Food is emotional. Customers make trust decisions with their eyes before they read compliance details. Creators need tools that work on phones during service. Design implements [Design Philosophy](../../company/company-philosophy.md#design-philosophy): one primary action per screen, whitespace as a feature, motion that communicates state, accessibility first, responsive across all breakpoints.

The design system governs execution; philosophy governs intent.

---

## Week 1 Priorities

| Day | Focus | Outcome |
|-----|-------|---------|
| **1** | Shared foundation + [Design Principles](../../design-system/principles.md) | Internalize calm/whitespace/motion rules |
| **1–2** | [Brand Strategy](../../brand/brand-strategy.md) + [Voice & Tone](../../brand/voice-and-tone.md) | Visual + verbal consistency |
| **2** | [Foundations](../../design-system/foundations/) — color, typography, spacing | Token usage |
| **2–3** | [Components Overview](../../design-system/components-overview.md) + buttons, inputs, cards | No one-off components when system exists |
| **3–4** | [Accessibility Standards](../../design-system/accessibility-standards.md) | WCAG AA minimum workflow |
| **4** | 3 [page specs](../../pages/) in your assigned surface | Spec ↔ design alignment |
| **5** | [Creator Dashboard](../../pages/creator/dashboard.md) + [Browse](../../pages/customer/browse.md) | Creator mobile vs customer discovery patterns |

---

## Key Documents to Read

### Week 1 (required)

| Document | Why |
|----------|-----|
| [Company Philosophy — Design](../../company/company-philosophy.md#design-philosophy) | Decision framework table |
| [Design System Principles](../../design-system/principles.md) | Calm, trust-visible execution |
| [Accessibility Standards](../../design-system/accessibility-standards.md) | Non-negotiable quality bar |
| [Personas](../../product/personas.md) | Who you design for — including Platform Ops |
| [Product Overview — Pillars](../../product/overview.md) | Trust, discovery, commerce, operations |
| [Navigation Model](../../pages/navigation-model.md) | Cross-surface consistency |

### Week 2–4 (role depth)

| Document | Why |
|----------|-----|
| [Marketplace Mechanics — Trust layers](../../product/marketplace-mechanics.md#trust-model) | What trust signals must be visible |
| [Page doc template](../../templates/page-doc-template.md) | Required spec sections you partner on |
| [Information Architecture](../../pages/information-architecture.md) | Full surface map |
| [Chef Quality Standards](../standards/chef-quality-standards.md) | Creator-facing quality expectations |
| [Trust & Safety Standards](../standards/trust-and-safety-standards.md) | Compliance display requirements |

### Admin design (internal product quality)

| Document | Why |
|----------|-----|
| [Admin Dashboard](../../pages/admin/admin-dashboard.md) | Ops tooling deserves same quality bar |
| [Verification Queue](../../pages/admin/verification-queue.md) | Dense but calm — checklist UX |
| [Moderation Queue](../../pages/admin/moderation-queue.md) | Context-rich enforcement UI |

### Component library

| Document | Why |
|----------|-----|
| [Buttons](../../design-system/components/buttons.md) | Primary action hierarchy |
| [Inputs](../../design-system/components/inputs.md) | Forms for verification, checkout |
| [Cards](../../design-system/components/cards.md) | Creator listings, menu items |
| [Badges](../../design-system/components/badges.md) | Verification status — meaningful, not decorative |
| [Modals](../../design-system/components/modals.md) | Confirm destructive actions |
| [Toasts](../../design-system/components/toasts.md) | State feedback |

---

## Systems Access

| System | Access level | Purpose |
|--------|--------------|---------|
| **Design system (Figma/library)** | Editor | Components and patterns |
| **Documentation repo** | Write | Page spec updates, design decisions |
| **Staging / preview** | View | Design QA |
| **Analytics** | View | UX metric validation |
| **Admin console** | Read | Internal UX research |

---

## Decision Framework

Apply [Design Philosophy questions](../../company/company-philosophy.md#design-philosophy):

| Question | Guidance |
|----------|----------|
| What is the one primary action? | Unclear → split or simplify screen |
| Are trust signals visible? | Verification, allergens, fulfillment above the fold |
| Mobile, tablet, desktop? | Design all three — creators manage orders on phones |
| Does motion communicate state? | Loading, success, error — never decorate |
| Accessible? | Keyboard, screen reader, reduced motion |

### Trust signal design rules

**Why badges matter:** Decorative trust icons without meaningful status erode trust faster than no badge — customers learn not to believe them.

| Element | Requirement |
|---------|-------------|
| Verification badge | Maps to real verification state from [Trust Service](../../engineering/services/trust-service.md) |
| Allergen disclosure | Visible before add-to-cart |
| Kitchen/production location | Transparent on storefront and item detail |
| Error states | Explicit — never blank or ambiguous |

### Anti-patterns (do not ship)

- Dense admin-style UI on customer surfaces
- Desktop-only creator workflows
- Custom components duplicating [design-system/](../../design-system/)
- Trust badges as decoration

---

## Escalation

| Scenario | Escalate to | Why |
|----------|-------------|-----|
| Trust signal placement conflict with visual minimalism | Product + T&S | Trust wins over aesthetics |
| New component needed | Design system lead | Maintain consistency |
| Accessibility exception request | Head of Design | WCAG AA is default |
| Copy/legal in UI | Product + Legal | Compliance text is not design-owned |
| Engineering feasibility breaks responsive spec | Product + Eng | Find alternative — do not drop mobile |

---

## Success Criteria

### Week 1
- [ ] Audit one existing page against design principles checklist
- [ ] Prototype one screen mobile + desktop with system components only
- [ ] Accessibility review (keyboard + screen reader) on assigned surface

### Day 30
- [ ] Ship design + page spec update for one feature with trust signals validated by T&S
- [ ] Zero one-off components where system components exist
- [ ] Contribute one design-system improvement (doc or component)

### Day 90
- [ ] Lead design critique using philosophy framework
- [ ] Partner on admin UX improvement — ops tooling quality bar
- [ ] Mentor new designer on persona × pillar matrix

---

## Related Documents

- [Employee Training](README.md)
- [Product Onboarding](product-onboarding.md) — Spec partnership
- [design-system/](../../design-system/)
- [pages/](../../pages/)
- [brand/](../../brand/)
- [docs/standards/](../standards/)
