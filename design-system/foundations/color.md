# Color Foundations

> Semantic color tokens for Marketplate — trust-forward, accessible, and calm.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Color in Marketplate serves **clarity and trust**, not decoration. The palette is restrained: neutrals carry most interfaces; semantic colors appear only when they communicate meaning.

These tokens implement [design principles](../principles.md) and meet [accessibility standards](../accessibility-standards.md) for WCAG 2.2 AA contrast.

**Theme scope (Phase 1):** Light theme foundation. Dark theme tokens deferred to Phase 2.

---

## Design Intent

| Quality | Color expression |
|---------|------------------|
| Calm | Warm neutrals, low saturation UI chrome |
| Premium | Deep text on soft backgrounds; no harsh pure black/white |
| Trust | Stable, cool-leaning primary; verification uses distinct trust hue |
| Food-forward | Photography and creator content provide color; UI stays neutral |

TODO(decision): Final brand primary hue — current foundation uses a deep teal-blue direction aligned with trust and freshness. Confirm against logo development in [`assets/`](../assets/).

---

## Token Architecture

Tokens use a three-layer model:

| Layer | Example | Usage |
|-------|---------|-------|
| **Primitive** | `blue-600` | Raw palette values — not used directly in UI |
| **Semantic** | `color-trust-default` | Intended meaning — used in components |
| **Component** | `button-primary-background` | Maps semantic tokens to component contexts |

Phase 1 documents **semantic tokens**. Component-level mappings come in Phase 2.

---

## Semantic Tokens — Light Theme

### Trust

Used for verification badges, trust strips, primary brand actions, and links.

| Token | Hex | Usage |
|-------|-----|-------|
| `color-trust-default` | `#1A6B6B` | Primary brand, verification badges, primary links |
| `color-trust-hover` | `#145656` | Hover state for trust/primary elements |
| `color-trust-subtle` | `#E8F4F4` | Trust badge backgrounds, highlighted trust zones |
| `color-trust-muted` | `#4A8F8F` | Secondary trust indicators, icons |

**Contrast notes:** `color-trust-default` on white = **5.8:1** (passes AA for normal text). Use white text on trust-default for buttons.

---

### Success

Order confirmations, verification approved, completed states.

| Token | Hex | Usage |
|-------|-----|-------|
| `color-success-default` | `#2D6A4F` | Success text, icons, borders |
| `color-success-hover` | `#245A42` | Hover on success actions |
| `color-success-subtle` | `#E9F5EE` | Success banner backgrounds |
| `color-success-muted` | `#52A372` | Progress indicators, secondary success |

**Contrast notes:** `color-success-default` on white = **6.2:1** (passes AA).

---

### Warning

Pickup deadline approaching, incomplete verification, non-blocking cautions.

| Token | Hex | Usage |
|-------|-----|-------|
| `color-warning-default` | `#9A6700` | Warning text, icons (amber-brown for calm, not alarm red) |
| `color-warning-hover` | `#7A5200` | Hover state |
| `color-warning-subtle` | `#FEF7E6` | Warning banner backgrounds |
| `color-warning-muted` | `#C48A00` | Secondary warning indicators |

**Contrast notes:** `color-warning-default` on white = **4.6:1** (passes AA for normal text). Do not use `color-warning-muted` for small text on white — use for icons and large text only.

---

### Error

Payment failures, form validation errors, blocking issues. Used sparingly.

| Token | Hex | Usage |
|-------|-----|-------|
| `color-error-default` | `#B42318` | Error text, destructive confirmation |
| `color-error-hover` | `#912018` | Hover on destructive actions |
| `color-error-subtle` | `#FEF3F2` | Error banner and field backgrounds |
| `color-error-muted` | `#D92D20` | Error icons, focus rings on invalid fields |

**Contrast notes:** `color-error-default` on white = **5.9:1** (passes AA).

---

### Neutral

The primary palette for UI chrome, text, borders, and backgrounds.

| Token | Hex | Usage |
|-------|-----|-------|
| `color-neutral-950` | `#1A1A1A` | Primary text, headings |
| `color-neutral-800` | `#3D3D3D` | Secondary text |
| `color-neutral-600` | `#6B6B6B` | Tertiary text, placeholders |
| `color-neutral-400` | `#A3A3A3` | Disabled text, decorative borders |
| `color-neutral-200` | `#E5E5E5` | Dividers, input borders |
| `color-neutral-100` | `#F5F5F4` | Subtle backgrounds, cards on white |
| `color-neutral-50` | `#FAFAF9` | Page background (warm off-white) |
| `color-neutral-0` | `#FFFFFF` | Card surfaces, modals, input fills |

**Contrast notes:**

| Combination | Ratio | Passes AA |
|-------------|-------|-----------|
| `neutral-950` on `neutral-0` | 16.1:1 | ✓ |
| `neutral-800` on `neutral-0` | 9.7:1 | ✓ |
| `neutral-600` on `neutral-0` | 5.0:1 | ✓ (normal text) |
| `neutral-600` on `neutral-50` | 4.7:1 | ✓ (normal text) |
| `neutral-400` on `neutral-0` | 2.6:1 | ✗ — decorative/disabled only |

---

## Surface & Background Tokens

| Token | Maps to | Usage |
|-------|---------|-------|
| `surface-page` | `neutral-50` | Default page background |
| `surface-default` | `neutral-0` | Cards, panels, modals |
| `surface-subtle` | `neutral-100` | Nested containers, table stripes |
| `surface-overlay` | `neutral-950` @ 40% opacity | Modal scrims |

---

## Text Tokens

| Token | Maps to | Usage |
|-------|---------|-------|
| `text-primary` | `neutral-950` | Headings, body, labels |
| `text-secondary` | `neutral-800` | Supporting text |
| `text-tertiary` | `neutral-600` | Captions, metadata, helper text |
| `text-disabled` | `neutral-400` | Disabled fields and buttons |
| `text-inverse` | `neutral-0` | Text on dark/trust/success backgrounds |
| `text-link` | `trust-default` | Interactive text links |
| `text-link-hover` | `trust-hover` | Link hover state |

---

## Border Tokens

| Token | Maps to | Usage |
|-------|---------|-------|
| `border-default` | `neutral-200` | Input borders, card outlines |
| `border-subtle` | `neutral-100` | Internal dividers |
| `border-focus` | `trust-default` | Focus rings (2px, see accessibility doc) |
| `border-error` | `error-default` | Invalid field borders |

---

## Usage Rules

### Do

- Use **neutrals for 90%+** of any screen
- Reserve **trust color** for primary actions and verification
- Pair semantic colors with **icon + text** — never color alone
- Test all text/background combinations against WCAG AA before shipping

### Don't

- Use success/warning/error as decorative accents
- Place saturated colors on large background areas
- Use pure `#000000` or `#FFFFFF` for body text/backgrounds — use warm neutrals
- Rely on red/green alone for status — always include text or icon

---

## Photography & Color

Food photography provides natural color richness. UI neutrals intentionally **recede** so photography and creator branding lead.

Creator storefronts may use **creator-defined accent colors** within guardrails (Phase 2). Platform chrome remains neutral.

---

## Accessibility Contrast Requirements

| Element | Minimum contrast | Standard |
|---------|------------------|----------|
| Normal text (< 18px / < 14px bold) | 4.5:1 | WCAG 2.2 AA |
| Large text (≥ 18px / ≥ 14px bold) | 3:1 | WCAG 2.2 AA |
| UI components & graphical objects | 3:1 | WCAG 2.2 AA |
| Focus indicators | 3:1 against adjacent colors | WCAG 2.2 AA |

→ Full accessibility requirements: [accessibility-standards.md](../accessibility-standards.md)

---

## Related Documents

- [Founding Constitution](../../company/constitution.md)
- [Design Principles](../principles.md)
- [Typography Foundations](typography.md)
- [Spacing Foundations](spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Components Overview](../components-overview.md)
- [Brand Strategy](../../brand/brand-strategy.md)
