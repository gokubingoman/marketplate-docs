# Design System Principles

> The foundational rules that govern every Marketplate interface — calm, premium, trust-building, and accessible.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

The Marketplate design system exists to make **trust visible**. Consistent, calm, accessible interfaces signal that the platform is reliable — that creators are professional and customers can buy with confidence.

These principles implement the [design philosophy](../company/constitution.md#design-philosophy) and express the [brand personality](../brand/brand-strategy.md#brand-personality) in product form.

**Quality bar:** If Apple, Airbnb, Stripe, and Etsy collaborated on a food marketplace, the result should feel like Marketplate.

---

## Core Principles

### 1. Calm interfaces

Reduce noise. Every element earns its place.

- Prefer **fewer components** over crowded layouts
- Use **neutral backgrounds** and let content — especially food photography — carry visual weight
- Avoid competing colors, badges, and banners on a single view
- Progressive disclosure: show detail when the user asks for it

**Test:** Squint at the screen. Is there one clear focal point?

---

### 2. Whitespace is a feature

Space communicates confidence and premium quality.

- Generous **padding and margins** — see [spacing foundations](foundations/spacing.md)
- **Breathing room** around trust signals (verification badges, order summaries)
- Do not fill empty space with decorative elements
- Empty states use whitespace intentionally — they are not errors

Whitespace is not "wasted space." It reduces cognitive load and increases comprehension.

---

### 3. Motion communicates state

Animation is functional, not decorative.

| Use motion for | Do not use motion for |
|----------------|----------------------|
| Loading and progress | Attention-grabbing loops |
| State transitions (open/close, expand/collapse) | Decorative parallax |
| Confirming actions (success, added to cart) | Blocking unrelated content |
| Drawing focus to changed content | Auto-playing carousels |

**Defaults:**

- Duration: 150–300ms for micro-interactions; 300–500ms for layout changes
- Easing: ease-out for entrances, ease-in for exits
- Respect `prefers-reduced-motion` — see [accessibility standards](accessibility-standards.md)

Motion should answer: *What just changed?*

---

### 4. One primary action per screen

Every screen has a single obvious next step.

- **One filled/primary button** per view hierarchy level
- Secondary actions use ghost or text button treatment
- Destructive actions require explicit confirmation — never primary styling
- Navigation provides wayfinding; the primary CTA provides commitment

**Examples:**

| Screen | Primary action |
|--------|----------------|
| Menu page | Add to order (on item detail) |
| Cart | Place order |
| Verification upload | Submit for review |
| Empty storefront | Share storefront link |

→ Component patterns: [components-overview.md](components-overview.md)

---

### 5. Premium feel

Quality in every pixel reinforces trust in the platform and the creators on it.

- **Large, high-quality photography** — real food, real creators, real kitchens
- **Minimal chrome** — UI recedes; content leads
- **Refined typography** — clear hierarchy, comfortable reading sizes → [typography](foundations/typography.md)
- **Subtle depth** — soft shadows and borders, not heavy skeuomorphism
- **Consistent polish** — no rough edges, misaligned elements, or placeholder styling in production

Premium does not mean luxury excess. It means **care**.

---

### 6. Accessibility first

Accessibility is a requirement, not a retrofit.

- Target **WCAG 2.2 Level AA** minimum → [accessibility standards](accessibility-standards.md)
- Design for keyboard, screen reader, and voice control from the start
- Color is never the sole indicator of meaning → [color foundations](foundations/color.md)
- Touch targets minimum **44×44 CSS pixels**
- Test with real assistive technology, not checklists alone

Accessible design is calm design: clear labels, predictable structure, readable text.

---

### 7. Responsive across all breakpoints

Never design for one breakpoint. Design **one system** that adapts.

| Breakpoint | Range | Design intent |
|------------|-------|---------------|
| Mobile | 320–767px | Primary customer ordering context; thumb-friendly |
| Tablet | 768–1023px | Creator dashboard and menu management |
| Desktop | 1024px+ | Creator operations, analytics, multi-column layouts |

**Rules:**

- Content parity across breakpoints — no hiding critical information on mobile
- Layout adapts; hierarchy stays consistent
- Typography scales responsively → [typography](foundations/typography.md)
- Touch and pointer inputs both supported

---

## Trust in Design

Trust signals are designed into the system, not bolted on.

| Signal | Design treatment |
|--------|------------------|
| Verification badges | Consistent icon + label; tooltip with credential detail |
| Creator identity | Photo, name, and verification visible above the fold on storefronts |
| Order summary | Full price breakdown before payment; no surprise fees |
| Allergen info | Prominent, scannable, not collapsed by default on item detail |
| Reviews | Authentic, dated, with context — not star-only aggregates |

Visual consistency in trust elements builds recognition: customers learn what "Verified Kitchen" looks like once and trust it everywhere.

---

## Design Tokens Over Hardcoded Values

All visual properties flow from **semantic tokens** defined in foundations:

- [Color](foundations/color.md) — trust, success, warning, error, neutral
- [Typography](foundations/typography.md) — display, body, UI roles
- [Spacing](foundations/spacing.md) — scale, grid, rhythm

Components reference tokens, not raw hex or pixel values. This enables theming, consistency, and accessibility auditing.

---

## Component Philosophy

Phase 1 defines **principles and foundations**. Component specifications (anatomy, states, props, code) are deferred to Phase 2.

The [component inventory](components-overview.md) lists what exists and why — not full specs.

**Build order:** Foundations → Core components (buttons, inputs, cards) → Composite patterns (checkout, storefront) → Page templates

→ Rollout: [phased rollout](../roadmap/phased-rollout.md)

---

## Anti-Patterns

| Anti-pattern | Why we avoid it |
|--------------|-----------------|
| Dark patterns (hidden fees, trick questions) | Violates trust thesis |
| Infinite scroll without structure | Disorienting; bad for accessibility |
| Auto-playing video/audio | Disrupts calm; accessibility issue |
| Multiple competing CTAs | Violates one-primary-action rule |
| Skeleton screens that never resolve | Erodes trust; prefer honest loading states |
| Generic stock food photography | Undermines authenticity |
| Dense dashboard defaults | Overwhelms creators; progressive disclosure instead |

---

## Decision Framework

When evaluating a design decision, ask in order:

1. **Does this build or erode trust?**
2. **Is the primary action obvious?**
3. **Is it accessible to WCAG 2.2 AA?**
4. **Does it work on mobile, tablet, and desktop?**
5. **Does it feel calm and premium?**
6. **Can it be built from design tokens?**

If any answer is no, revise before shipping.

---

## Related Documents

- [Founding Constitution](../company/constitution.md)
- [Brand Strategy](../brand/brand-strategy.md)
- [Voice and Tone](../brand/voice-and-tone.md)
- [Color Foundations](foundations/color.md)
- [Typography Foundations](foundations/typography.md)
- [Spacing Foundations](foundations/spacing.md)
- [Accessibility Standards](accessibility-standards.md)
- [Components Overview](components-overview.md)
- [Page Doc Template](../templates/page-doc-template.md)
