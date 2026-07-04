# Components Overview

> Inventory of Marketplate UI components — purpose, scope, and links to full specifications.

**Status:** Active  
**Version:** 1.1  
**Last updated:** 2026-07-03

---

## Purpose

This document lists the **core component inventory** for Marketplate. Each entry defines *what the component is for* and *where it appears*, with a link to its full specification.

Full component specifications (variants, anatomy, states, tokens, accessibility, responsive behavior) live in [`components/`](components/) — built on [foundations](foundations/color.md) and [principles](principles.md).

---

## Component Principles (Summary)

All components inherit from [design principles](principles.md):

- Calm, minimal visual weight
- Token-driven styling — no hardcoded values
- WCAG 2.2 AA compliant → [accessibility standards](accessibility-standards.md)
- Responsive across mobile, tablet, desktop
- One primary action per context where applicable

---

## Inventory

### Buttons

**Purpose:** Trigger actions — submit forms, navigate, confirm decisions.

| Variant | Usage |
|---------|-------|
| **Primary** | Single main action per view — "Place order," "Submit for review" |
| **Secondary** | Supporting actions — "View menu," "Save draft" |
| **Ghost / text** | Tertiary actions — "Cancel," "Learn more" |
| **Destructive** | Irreversible actions — "Cancel order," "Delete item" — requires confirmation |

**Appears on:** Every page. Checkout, forms, dashboards, modals, empty states.

→ **Full spec:** [components/buttons.md](components/buttons.md)

---

### Inputs

**Purpose:** Collect user data — text, selections, uploads, dates.

| Type | Usage |
|------|-------|
| **Text input** | Names, emails, search, quantities |
| **Textarea** | Descriptions, special instructions |
| **Select / dropdown** | Pickup windows, categories, filters |
| **Checkbox** | Multi-select options, allergen acknowledgment, consent |
| **Radio** | Single-select from few options |
| **Date / time picker** | Pickup scheduling, menu availability |
| **File upload** | Verification documents, menu photos |
| **Search input** | Menu search, creator discovery |

**Appears on:** Registration, verification, menu management, checkout, search.

→ **Full spec:** [components/inputs.md](components/inputs.md)

---

### Cards

**Purpose:** Group related content into scannable, elevated surfaces.

| Variant | Usage |
|---------|-------|
| **Menu item card** | Food photo, name, price, dietary tags, add action |
| **Order card** | Order summary, status, pickup details |
| **Creator card** | Discovery — photo, name, verification, cuisine tags |
| **Dashboard stat card** | Metrics — orders, revenue, pending verifications |
| **Review card** | Customer review with date, rating, text |

**Appears on:** Storefronts, discovery, dashboards, order history.

→ **Full spec:** [components/cards.md](components/cards.md)

---

### Badges

**Purpose:** Compact status, category, and trust indicators.

| Variant | Usage |
|---------|-------|
| **Verification badge** | "Verified Identity," "Verified Kitchen" — trust-critical |
| **Status badge** | Order status — "Confirmed," "Ready for pickup," "Completed" |
| **Dietary badge** | "Vegan," "Gluten-free," "Contains nuts" |
| **Category badge** | Cuisine type, menu section tags |

**Appears on:** Creator profiles, menu items, order lists, checkout trust strip.

→ **Full spec:** [components/badges.md](components/badges.md)

→ Verification naming: [naming-conventions.md](../brand/naming-conventions.md#verification--trust-labels)

---

### Avatars

**Purpose:** Represent people — creators and customers — with photo or initials fallback.

| Variant | Usage |
|---------|-------|
| **Creator avatar** | Storefront header, reviews, discovery cards |
| **Customer avatar** | Review attribution, account settings |
| **Avatar group** | Multiple creators (rare — catering contexts) |

**Appears on:** Storefronts, profiles, reviews, navigation account menu.

→ **Full spec:** [components/avatars.md](components/avatars.md)

---

### Navigation

**Purpose:** Wayfinding across platform surfaces.

| Component | Usage |
|-----------|-------|
| **Top nav bar** | Global navigation — logo, search, account, cart |
| **Sidebar nav** | Creator dashboard — persistent section links |
| **Tab bar (mobile)** | Customer app bottom nav — Home, Search, Orders, Account |
| **Breadcrumbs** | Dashboard depth — Settings → Verification → Kitchen |
| **Pagination** | Order history, review lists, admin tables |
| **Segmented control** | Toggle views — "Active menu" / "Draft menu" |

**Appears on:** All authenticated surfaces. Mobile bottom nav for customer app.

→ **Full spec:** [components/navigation.md](components/navigation.md)

---

### Modals

**Purpose:** Focused overlays for decisions that interrupt the current flow.

| Variant | Usage |
|---------|-------|
| **Confirmation modal** | Destructive action confirmation — "Cancel this order?" |
| **Form modal** | Quick edits without full page navigation |
| **Detail modal** | Expanded menu item detail on mobile |
| **Verification modal** | Explain verification requirements |

**Appears on:** Checkout confirmations, dashboard actions, mobile item detail.

→ **Full spec:** [components/modals.md](components/modals.md)

→ Accessibility: [accessibility-standards.md](accessibility-standards.md#focus-management)

---

### Toasts

**Purpose:** Non-blocking feedback on completed or failed actions.

| Variant | Usage |
|---------|-------|
| **Success toast** | "Order placed," "Menu updated" |
| **Error toast** | Recoverable failures — "Payment failed. Try again." |
| **Info toast** | Neutral updates — "Pickup window changed" |
| **Warning toast** | Non-blocking caution — "Verification expires in 7 days" |

**Appears on:** Any page after async actions. Never for critical errors that require user decision — use inline errors or modals instead.

→ **Full spec:** [components/toasts.md](components/toasts.md)

→ Voice patterns: [voice-and-tone.md](../brand/voice-and-tone.md)

---

## Component Specifications

| Component | Spec |
|-----------|------|
| Buttons | [components/buttons.md](components/buttons.md) |
| Inputs | [components/inputs.md](components/inputs.md) |
| Cards | [components/cards.md](components/cards.md) |
| Badges | [components/badges.md](components/badges.md) |
| Avatars | [components/avatars.md](components/avatars.md) |
| Navigation | [components/navigation.md](components/navigation.md) |
| Modals | [components/modals.md](components/modals.md) |
| Toasts | [components/toasts.md](components/toasts.md) |

---

## Component Dependencies

```
Foundations (color, typography, spacing)
    ↓
Core (buttons, inputs, badges, avatars)
    ↓
Composite (cards, navigation)
    ↓
Overlay (modals, toasts)
    ↓
Page templates (Phase 2 — pages/)
```

Build foundations and core components before composite patterns and page templates.

---

## Out of Scope (Phase 1)

The following are **not** inventoried here — they come in Phase 2 or later:

- Data tables (creator dashboard)
- Charts and analytics visualizations
- Rich text editor (menu descriptions)
- Image gallery / carousel
- Map components (pickup location)
- Chat / messaging
- Payment form (Stripe Elements integration)
- Onboarding wizard steps

These will be added to this inventory as they enter the design system roadmap.

→ Rollout plan: [phased rollout](../roadmap/phased-rollout.md)

---

## Related Documents

- [Founding Constitution](../company/constitution.md)
- [Design Principles](principles.md)
- [Color Foundations](foundations/color.md)
- [Typography Foundations](foundations/typography.md)
- [Spacing Foundations](foundations/spacing.md)
- [Accessibility Standards](accessibility-standards.md)
- [Naming Conventions](../brand/naming-conventions.md)
- [Page Doc Template](../templates/page-doc-template.md)
- [Phased Rollout](../roadmap/phased-rollout.md)
