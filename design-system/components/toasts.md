# Toasts

> Non-blocking feedback for completed or failed async actions — success, error, info, and warning messages.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Toasts confirm actions without interrupting workflow. They implement [motion communicates state](../principles.md#3-motion-communicates-state) — brief appearance, optional dismiss, automatic expiry for non-critical messages.

**Never use toasts for critical errors requiring user decisions** — use inline errors or [modals](modals.md) instead.

### Variants

| Variant | Usage | Duration | Politeness |
|---------|-------|----------|------------|
| **Success toast** | "Order placed," "Menu updated" | 5s | polite |
| **Error toast** | Recoverable failures — "Payment failed. Try again." | Persistent until dismiss | assertive |
| **Info toast** | Neutral updates — "Pickup window changed" | 5s | polite |
| **Warning toast** | Non-blocking caution — "Verification expires in 7 days" | 8s | polite |

**Appears on:** Any page after async actions.

→ Voice patterns: [voice and tone](../../brand/voice-and-tone.md)  
→ Inventory context: [components-overview.md](../components-overview.md#toasts)

---

## Anatomy

```
┌─────────────────────────────────────────────┐
│ [Icon]  Message text              [Dismiss] │
│         Optional action link                │
└─────────────────────────────────────────────┘
```

| Part | Required | Description |
|------|----------|-------------|
| **Container** | Yes | Fixed-position notification |
| **Icon** | Yes | Variant-specific; `aria-hidden="true"` |
| **Message** | Yes | Concise — max 2 lines |
| **Action link** | No | "Undo," "Retry" — single action max |
| **Dismiss button** | Yes (error); optional (auto-dismiss) | `aria-label="Dismiss notification"` |

---

## Sizes & Layout

| Property | Value |
|----------|-------|
| **Min width** | 320px |
| **Max width** | 420px (desktop), calc(100vw - 32px) (mobile) |
| **Padding** | `space-4` |
| **Border radius** | `radius-lg` (12px) |
| **Icon size** | 20px |
| **Gap (icon to text)** | `space-3` |
| **Stack gap** | `space-3` between multiple toasts |

**Position:**

| Breakpoint | Position |
|------------|----------|
| **Mobile** | Bottom center, 16px above tab bar / safe area |
| **Tablet+** | Top right, 24px from edge, below top nav |

**Z-index:** `z-toast` (400).

---

## Variant Specifications

| Variant | Background | Border (left 4px) | Icon color | Text |
|---------|------------|-------------------|------------|------|
| **Success** | `color-success-subtle` | `color-success-default` | `color-success-default` | `text-primary` |
| **Error** | `color-error-subtle` | `color-error-default` | `color-error-default` | `text-primary` |
| **Info** | `color-trust-subtle` | `color-trust-default` | `color-trust-default` | `text-primary` |
| **Warning** | `color-warning-subtle` | `color-warning-default` | `color-warning-default` | `text-primary` |

Left border provides non-color-dependent variant identification alongside icon.

---

## States

| State | Behavior |
|-------|----------|
| **Entering** | Slide in from bottom (mobile) or right (desktop); fade; 200ms ease-out |
| **Visible** | Displayed; countdown for auto-dismiss variants |
| **Hover** | Pause auto-dismiss timer (pointer devices) |
| **Focus (dismiss/action)** | `border-focus` on focused control |
| **Exiting** | Fade out 150ms ease-in |
| **Stacked** | Max 3 visible; oldest dismissed when 4th arrives |

No loading state inside toasts — show toast after action completes. In-progress: use button loading state or inline indicator.

**Reduced motion:** Instant appear at final position; no slide animation.

---

## Duration & Dismiss

| Variant | Auto-dismiss | Dismiss button |
|---------|--------------|----------------|
| **Success** | 5 seconds | Optional |
| **Error** | Never | Required |
| **Info** | 5 seconds | Optional |
| **Warning** | 8 seconds | Recommended |

**Pause on hover/focus:** Timer pauses while user hovers toast or focuses dismiss/action.

**Action link:** Single text button (ghost style). "Retry" for error toasts when recovery is one click.

---

## Component Tokens

| Token | Maps to | Context |
|-------|---------|---------|
| `toast-success-background` | `color-success-subtle` | Success fill |
| `toast-success-accent` | `color-success-default` | Border, icon |
| `toast-error-background` | `color-error-subtle` | Error fill |
| `toast-error-accent` | `color-error-default` | Border, icon |
| `toast-info-background` | `color-trust-subtle` | Info fill |
| `toast-info-accent` | `color-trust-default` | Border, icon |
| `toast-warning-background` | `color-warning-subtle` | Warning fill |
| `toast-warning-accent` | `color-warning-default` | Border, icon |
| `toast-text` | `text-primary` | Message body |
| `toast-shadow` | `0 4px 16px rgba(26,26,26,0.10)` | Elevation |

→ Semantic source: [color foundations](../foundations/color.md)

---

## Token Usage Summary

| Property | Token |
|----------|-------|
| Message typography | `text-body-sm`, `text-primary` |
| Action link | `text-ui-md`, `text-link` |
| Padding | `space-4` |
| Icon gap | `space-3` |
| Dismiss button | 44×44px hit area |

→ Typography: [typography foundations](../foundations/typography.md)  
→ Spacing: [spacing foundations](../foundations/spacing.md)

---

## Accessibility

Target: **WCAG 2.2 AA** → [accessibility standards](../accessibility-standards.md)

| Requirement | Implementation |
|-------------|----------------|
| **Live region** | Container: `role="status"` + `aria-live="polite"` (success, info, warning) |
| **Error toasts** | `role="alert"` + `aria-live="assertive"` |
| **Focus** | Toasts do **not** steal focus on appear |
| **Dismiss** | Keyboard accessible; `Escape` dismisses topmost toast if focused |
| **Message text** | Full message in text — not icon-only |
| **Action** | Action link is focusable; descriptive label — "Retry payment" |
| **Stacking** | New toasts announced; avoid rapid-fire duplicates |
| **Timeout** | Provide dismiss for persistent-sensitive users; error always dismissible |

Screen reader announces toast message on appear. Do not announce every cart count change if user is actively interacting with cart — debounce announcements.

→ Live region patterns: [accessibility standards — screen reader](../accessibility-standards.md#live-regions)

---

## Responsive Behavior

| Breakpoint | Position | Width | Notes |
|------------|----------|-------|-------|
| **Mobile (320–767px)** | Bottom center, above tab bar + safe area | Full width minus `space-8` margins | Avoid covering sticky CTAs |
| **Tablet (768–1023px)** | Top right | max 420px | Below top nav (64px + 24px) |
| **Desktop (1024px+)** | Top right | max 420px | Same as tablet |

**Tab bar offset:** Mobile toasts sit 72px from bottom (56px tab bar + 16px gap) plus `env(safe-area-inset-bottom)`.

**Stack direction:** Newest toast on top (desktop) or bottom (mobile, nearest thumb).

---

## Do / Don't

### Do

- Keep messages **concise** — one sentence
- Use **success toasts** for confirmed async actions
- Use **error toasts** only for recoverable failures with retry path
- Include **icon + text** for variant identification
- **Pause dismiss timer** on hover/focus
- Limit visible stack to **3 toasts**

### Don't

- Use toasts for **critical errors** requiring decisions — use modal or inline error
- Use toasts for **form validation** — use inline field errors
- Steal **focus** when toast appears
- Show toasts for **every** cart add on mobile — use micro-animation on cart icon instead
- Stack more than 3 toasts
- Use toasts for **allergen warnings** — allergens belong inline on item detail
- Auto-dismiss **error** toasts

---

## Related Documents

- [Design Principles](../principles.md)
- [Components Overview](../components-overview.md#toasts)
- [Color Foundations](../foundations/color.md)
- [Typography Foundations](../foundations/typography.md)
- [Spacing Foundations](../foundations/spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Modals](modals.md) — critical error pattern
- [Buttons](buttons.md) — action loading states
- [Voice and Tone](../../brand/voice-and-tone.md)
