# Modals

> Focused overlays for decisions that interrupt the current flow — confirmations, quick edits, and mobile detail views.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Modals capture attention for decisions that cannot happen inline. They support [one primary action](../principles.md#4-one-primary-action-per-screen) per dialog and implement strict focus management per [accessibility standards](../accessibility-standards.md#focus-management).

### Variants

| Variant | Usage | Size |
|---------|-------|------|
| **Confirmation modal** | Destructive action confirmation — "Cancel this order?" | sm |
| **Form modal** | Quick edits without full page navigation | md |
| **Detail modal** | Expanded menu item detail on mobile | lg / full-screen |
| **Verification modal** | Explain verification requirements | md |

**Appears on:** Checkout confirmations, dashboard actions, mobile item detail.

→ Inventory context: [components-overview.md](../components-overview.md#modals)

---

## Anatomy

```
     ┌─ Scrim (surface-overlay) ─────────────────────────┐
     │                                                    │
     │    ┌──────────────────────────────────────┐       │
     │    │  Title                           [×] │       │  ← Header
     │    ├──────────────────────────────────────┤       │
     │    │                                      │       │
     │    │  Body content                        │       │  ← Body (scrollable)
     │    │                                      │       │
     │    ├──────────────────────────────────────┤       │
     │    │              [Secondary] [Primary]   │       │  ← Footer
     │    └──────────────────────────────────────┘       │
     │                                                    │
     └────────────────────────────────────────────────────┘
```

| Part | Required | Description |
|------|----------|-------------|
| **Scrim** | Yes | `surface-overlay` — 40% `neutral-950`; click closes non-destructive modals only if explicitly allowed |
| **Dialog container** | Yes | `role="dialog"` or `role="alertdialog"` |
| **Header** | Yes | Title (`h2` id referenced by `aria-labelledby`) |
| **Close button** | Yes | Icon "×" with `aria-label="Close dialog"` |
| **Body** | Yes | Content; scrolls independently when overflow |
| **Footer** | Conditional | Action buttons — primary rightmost |

Use `role="alertdialog"` for destructive confirmations requiring explicit acknowledgment.

---

## Sizes

| Size | Width | Max height | Usage |
|------|-------|------------|-------|
| **sm** | 400px | 80vh | Confirmations, simple alerts |
| **md** | 480px | 85vh | Forms, verification explainer |
| **lg** | 640px | 90vh | Complex forms, detail with image |
| **full-screen** | 100vw × 100vh | 100vh | Mobile detail modal only (< 768px) |

**Padding:** Header/footer: `space-6` horizontal, `space-4` vertical. Body: `space-6`.

**Border radius:** `radius-lg` (12px) on desktop/tablet; `0` on full-screen mobile.

**Gap (footer buttons):** `space-3`; footer buttons right-aligned, full-width stack on mobile for primary flows.

---

## States

Modals do not have hover/active states on the container. Internal elements follow [buttons](buttons.md) and [inputs](inputs.md) specs.

| State | Scrim | Dialog | Behavior |
|-------|-------|--------|----------|
| **Opening** | Fade in 200ms | Scale 98%→100% or slide up on mobile | Focus moves to dialog |
| **Open** | Visible | Visible | Focus trapped; body scroll locked |
| **Closing** | Fade out 150ms | Reverse entrance | Focus returns to trigger |
| **Loading (body)** | — | `aria-busy="true"` on body | Primary action shows loading state |
| **Error (form)** | — | Inline errors in body | Focus moves to first error |

**Scroll lock:** `overflow: hidden` on `<body>` while modal open. Preserve scroll position on close.

**Reduced motion:** Instant appear/disappear — no scale or slide.

---

## Focus & Interaction

| Behavior | Rule |
|----------|------|
| **Open** | Focus first focusable element (close button or primary field) |
| **Tab cycle** | Focus trapped within dialog |
| **Escape** | Closes modal unless destructive confirmation requires explicit button |
| **Scrim click** | Closes informational modals; does NOT close destructive confirmations |
| **Close** | Focus returns to element that opened modal |
| **Route change** | Close modal and proceed |

Destructive confirmation: Escape disabled OR shows "Use Cancel to close" pattern — prefer allowing Escape as equivalent to Cancel (secondary action).

→ Full spec: [accessibility standards — focus management](../accessibility-standards.md#focus-management)

---

## Component Tokens

| Token | Maps to | Context |
|-------|---------|---------|
| `modal-scrim` | `surface-overlay` | Backdrop |
| `modal-background` | `surface-default` | Dialog fill |
| `modal-border` | `border-subtle` | Optional header/footer divider |
| `modal-title` | `text-display-sm` + `text-primary` | Dialog title |
| `modal-body` | `text-body-md` + `text-primary` | Body copy |
| `modal-shadow` | `0 8px 32px rgba(26,26,26,0.12)` | Elevation |
| `modal-z-index` | `z-modal` (300) | Stacking |

→ Semantic source: [color foundations](../foundations/color.md)

---

## Token Usage Summary

| Property | Token |
|----------|-------|
| Title | `text-display-sm`, weight 600, `text-primary` |
| Body text | `text-body-md`, `text-primary` |
| Header/footer padding | `space-6` |
| Body padding | `space-6` |
| Header/body divider | `border-subtle` 1px |
| Footer button gap | `space-3` |
| Close button hit area | 44×44px |

→ Typography: [typography foundations](../foundations/typography.md)  
→ Spacing: [spacing foundations](../foundations/spacing.md)

---

## Accessibility

Target: **WCAG 2.2 AA** → [accessibility standards](../accessibility-standards.md)

| Requirement | Implementation |
|-------------|----------------|
| **Role** | `role="dialog"` + `aria-modal="true"` |
| **Labeling** | `aria-labelledby` → title ID; `aria-describedby` → body ID if needed |
| **Alert dialog** | `role="alertdialog"` for destructive confirmations |
| **Focus trap** | Tab cycles within modal; no focus escape to background |
| **Focus return** | Restore focus to trigger on close |
| **Escape** | Closes modal (maps to Cancel for confirmations) |
| **Background inert** | `inert` attribute on main content OR `aria-hidden="true"` on background |
| **Scroll lock** | Body scroll prevented; modal body scrolls independently |
| **Close button** | Visible, keyboard accessible, `aria-label="Close"` |
| **Primary action** | One primary button per modal footer |
| **Destructive confirm** | Destructive action uses [destructive button](buttons.md) — never primary filled |

Screen readers announce dialog title on open. Do not steal focus repeatedly during modal lifetime.

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| **Mobile (320–767px)** | Detail modals: **full-screen** (100vw, no radius). Confirmations: bottom sheet optional (slides up, 90% width max) OR centered sm modal with 16px margin. Footer buttons: **full-width stack** — primary on top. |
| **Tablet (768–1023px)** | Centered modals at defined widths. md/lg sizes. |
| **Desktop (1024px+)** | Centered with max widths. lg for detail modals. |

**Mobile item detail:** Menu item [card](cards.md) tap opens full-screen detail modal with image, description, allergens, and "Add to order" sticky footer.

**Keyboard on mobile:** Virtual keyboard must not obscure primary action — footer sticky above keyboard where possible.

**Stacking:** One modal at a time. Nested modals prohibited — replace content or use stepped flow within single modal.

---

## Do / Don't

### Do

- Use modals for **focused decisions** that interrupt flow
- Include **clear title** stating the decision
- Provide **explicit Cancel** alongside destructive confirm
- Return **focus to trigger** on close
- Use **full-screen on mobile** for content-heavy detail
- Lock **background scroll** while open

### Don't

- Stack multiple modals
- Use modals for non-critical information — use inline content or [toasts](toasts.md)
- Close destructive confirmations on scrim click
- Omit close button or Escape handling
- Put more than one primary button in footer
- Auto-open modals on page load (except cookie consent at `z-max`)
- Use modals for entire multi-step flows — use dedicated pages

---

## Related Documents

- [Design Principles](../principles.md)
- [Components Overview](../components-overview.md#modals)
- [Color Foundations](../foundations/color.md)
- [Typography Foundations](../foundations/typography.md)
- [Spacing Foundations](../foundations/spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Buttons](buttons.md)
- [Inputs](inputs.md)
- [Cards](cards.md)
- [Toasts](toasts.md)
