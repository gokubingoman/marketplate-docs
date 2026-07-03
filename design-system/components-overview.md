# Components Overview

> Inventory of Marketplate UI components — purpose and scope. Full specifications deferred to Phase 2.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

This document lists the **core component inventory** for Marketplate. Each entry defines *what the component is for* and *where it appears* — not anatomy, props, states, or code.

Full component specifications (variants, sizes, states, accessibility details, code APIs) are **Phase 2 deliverables**, built on top of [foundations](foundations/color.md) and [principles](principles.md).

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

**Phase 2 spec will define:** Sizes (sm, md, lg), loading state, icon placement, disabled state, full-width mobile behavior.

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

**Phase 2 spec will define:** Validation states, helper text placement, label anatomy, inline vs. summary errors.

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

**Phase 2 spec will define:** Padding tokens, image aspect ratios, interactive vs. static cards, hover/focus states.

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

**Phase 2 spec will define:** Color mappings per badge type, icon pairings, tooltip behavior for verification detail.

→ Verification naming: [naming-conventions.md](../../brand/naming-conventions.md#verification--trust-labels)

---

### Avatars

**Purpose:** Represent people — creators and customers — with photo or initials fallback.

| Variant | Usage |
|---------|-------|
| **Creator avatar** | Storefront header, reviews, discovery cards |
| **Customer avatar** | Review attribution, account settings |
| **Avatar group** | Multiple creators (rare — catering contexts) |

**Appears on:** Storefronts, profiles, reviews, navigation account menu.

**Phase 2 spec will define:** Sizes (xs–xl), fallback initials logic, online/status indicators (if applicable).

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

**Phase 2 spec will define:** Active state styling, responsive collapse behavior, sticky positioning.

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

**Phase 2 spec will define:** Focus trap, escape behavior, scroll locking, size variants, mobile full-screen behavior.

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

**Phase 2 spec will define:** Duration, dismiss behavior, stacking, `aria-live` politeness levels, mobile positioning.

→ Voice patterns: [voice-and-tone.md](../../brand/voice-and-tone.md)

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

→ Rollout plan: [phased rollout](../../roadmap/phased-rollout.md)

---

## Related Documents

- [Founding Constitution](../../company/constitution.md)
- [Design Principles](principles.md)
- [Color Foundations](foundations/color.md)
- [Typography Foundations](foundations/typography.md)
- [Spacing Foundations](foundations/spacing.md)
- [Accessibility Standards](accessibility-standards.md)
- [Naming Conventions](../../brand/naming-conventions.md)
- [Page Doc Template](../../templates/page-doc-template.md)
- [Phased Rollout](../../roadmap/phased-rollout.md)
