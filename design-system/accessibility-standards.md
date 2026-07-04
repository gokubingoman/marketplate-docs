# Accessibility Standards

> WCAG 2.2 AA targets, focus management, motion reduction, and screen reader patterns for Marketplate.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Accessibility is a **trust requirement**. Customers ordering food — especially those with dietary restrictions, visual impairments, or motor disabilities — must be able to browse menus, review allergen information, and complete orders with confidence.

Marketplate targets **WCAG 2.2 Level AA** compliance across all customer- and creator-facing surfaces. Accessibility is designed in from the start per [design principles](principles.md), not audited at the end.

---

## Compliance Target

| Standard | Level | Scope |
|----------|-------|-------|
| [WCAG 2.2](https://www.w3.org/TR/WCAG22/) | **AA** | All public and authenticated product UI |
| [WAI-ARIA 1.2](https://www.w3.org/TR/wai-aria-1.2/) | Best practices | Custom components, dynamic content |
| Section 508 | Aligned with WCAG 2.2 AA | US government-adjacent partnerships |

AAA is aspirational for critical flows (checkout, allergen disclosure) but not a blanket requirement at launch.

---

## Core Requirements

### Perceivable

| Requirement | Implementation |
|-------------|----------------|
| **Text alternatives** | All meaningful images have descriptive `alt` text. Decorative images use `alt=""`. |
| **Color contrast** | Minimum 4.5:1 normal text, 3:1 large text and UI components → [color foundations](foundations/color.md) |
| **Resize text** | Content readable at 200% zoom without horizontal scroll or loss of functionality |
| **Non-text contrast** | Icons, input borders, focus rings meet 3:1 against adjacent colors |
| **Captions & transcripts** | Required for any video/audio content in marketing or creator profiles |

### Operable

| Requirement | Implementation |
|-------------|----------------|
| **Keyboard accessible** | All functionality available via keyboard — see Keyboard section |
| **No keyboard traps** | Focus can always move away from any component |
| **Skip navigation** | "Skip to main content" link on every page |
| **Focus visible** | Custom focus ring on all interactive elements — see Focus section |
| **Target size (2.5.8)** | Minimum 44×44 CSS pixels for touch targets |
| **Motion** | Respect `prefers-reduced-motion` — see Motion section |

### Understandable

| Requirement | Implementation |
|-------------|----------------|
| **Page language** | `<html lang="en">` (or appropriate locale) |
| **Consistent navigation** | Predictable nav placement across pages |
| **Error identification** | Errors described in text, associated with fields |
| **Labels & instructions** | All form fields have visible labels; allergen fields require explicit acknowledgment |

### Robust

| Requirement | Implementation |
|-------------|----------------|
| **Valid HTML** | Semantic elements, valid nesting |
| **Name, role, value** | Custom components expose correct ARIA attributes |
| **Status messages** | Dynamic updates announced to screen readers — see Screen Reader section |

---

## Focus Management

### Focus ring specification

| Property | Value |
|----------|-------|
| Color | `border-focus` (`color-trust-default`) |
| Width | 2px |
| Offset | 2px from element edge |
| Style | Solid outline (use `outline`, not `box-shadow` alone) |
| Contrast | ≥ 3:1 against adjacent background |

**Never remove focus indicators** (`outline: none`) without providing a visible replacement.

### Focus order

- Follow logical DOM order — no positive `tabindex` values
- Modal opens → focus moves to first focusable element inside modal
- Modal closes → focus returns to trigger element
- Route changes → focus moves to `<h1>` or main landmark
- Toast appears → use `aria-live` (see Screen Reader section); do not steal focus for non-critical toasts

### Skip link

```html
<a href="#main-content" class="skip-link">Skip to main content</a>
```

Visible on keyboard focus only. First focusable element on every page.

---

## Keyboard Patterns

All components in [components-overview.md](./components-overview.md) must support these patterns:

| Component | Keys |
|-----------|------|
| **Button** | `Enter`, `Space` to activate |
| **Link** | `Enter` to navigate |
| **Text input** | Standard text entry |
| **Checkbox / radio** | `Space` to toggle/select |
| **Select / dropdown** | `Enter`/`Space` open; `Arrow` navigate; `Enter` select; `Escape` close |
| **Modal** | `Escape` close; focus trap while open |
| **Tabs** | `Arrow` switch tabs; `Tab` exits tab list |
| **Toast** | Not focus-stealing; dismissible via keyboard if persistent |

**No keyboard-only hover menus.** All dropdown content must be activatable and dismissible via keyboard.

---

## Motion Reduction

Per [design principles](principles.md), motion communicates state — but must not harm vestibular-sensitive users.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

| With motion | Reduced motion alternative |
|-------------|---------------------------|
| Slide-in panel | Instant appear |
| Fade transition | Instant swap |
| Loading spinner | Static loading text: "Loading menu…" |
| Success checkmark animation | Static success icon + text |
| Skeleton pulse | Static skeleton or spinner |

**Never auto-play** video, animation, or carousels. User must initiate playback.

---

## Screen Reader Patterns

### Landmarks

Every page includes:

```html
<header role="banner">       <!-- Global nav -->
<nav role="navigation">      <!-- Primary nav (may be inside header) -->
<main id="main-content">     <!-- Primary content — skip link target -->
<footer role="contentinfo">  <!-- Footer links -->
```

One `<main>` per page. One `<h1>` per page matching the page title.

### Live regions

| Event | ARIA | Politeness |
|-------|------|------------|
| Form validation error | `role="alert"` on error summary | Assertive |
| Inline field error | `aria-describedby` linking to error text | — |
| Toast notification | `role="status"` or `aria-live="polite"` | Polite |
| Critical failure (payment) | `role="alert"` | Assertive |
| Loading complete | `aria-live="polite"`: "Menu loaded" | Polite |
| Cart update | `aria-live="polite"`: "2 items in cart" | Polite |

**Do not over-announce.** Loading spinners do not need live regions unless loading completes after a delay (> 3 seconds).

### Hidden content

| Technique | Usage |
|-----------|-------|
| `aria-hidden="true"` | Decorative icons adjacent to visible text |
| `.sr-only` / visually hidden class | Screen-reader-only supplementary text |
| `aria-expanded` | Toggle buttons, accordion headers |
| `aria-current="page"` | Active nav item |
| `aria-busy="true"` | Content area loading |

### Allergen & food safety (critical)

Allergen information must be:

- **Visible** — not hidden behind hover or collapsed by default on item detail
- **Programmatically associated** — `aria-describedby` linking menu item to allergen list
- **Readable** — not icon-only; text labels required alongside any allergen icons

Checkout flows include an explicit allergen acknowledgment checkbox with associated label — not pre-checked.

---

## Form Accessibility

| Rule | Detail |
|------|--------|
| Visible labels | Every input has a `<label>` — no placeholder-only labels |
| Required fields | `aria-required="true"` + visible "Required" indicator |
| Error association | `aria-invalid="true"` + `aria-describedby` pointing to error message |
| Error summary | On submit failure, focus moves to error summary at top of form |
| Group labels | Related fields use `<fieldset>` + `<legend>` |
| Autocomplete | Use appropriate `autocomplete` attributes (name, email, address) |

Error copy follows [voice and tone](../brand/voice-and-tone.md#error-messages): specific, actionable, calm.

---

## Image & Media

| Content type | Requirement |
|--------------|-------------|
| Creator photo | Alt: "[Creator name], [business name]" |
| Food photo | Alt: descriptive — "Sourdough loaf with golden crust" not "Image" or "Food" |
| Verification badge | Alt: "Verified Identity" / "Verified Kitchen" — match visible label |
| Decorative photography | `alt=""` |
| Icons with text | Icon `aria-hidden="true"`, text provides meaning |
| Icons without text | `aria-label` on button |

---

## Testing Requirements

### Automated (CI)

- axe-core or equivalent on all page templates
- Color contrast validation on token combinations
- HTML validation

### Manual (each release)

- Full keyboard navigation of checkout flow
- VoiceOver (macOS/iOS) and NVDA (Windows) smoke test
- 200% zoom test on mobile and desktop
- `prefers-reduced-motion` verification

### Assistive technology matrix

| AT | Platform | Priority |
|----|----------|----------|
| VoiceOver | macOS, iOS | P0 |
| NVDA | Windows | P0 |
| TalkBack | Android | P1 |
| Keyboard only | All | P0 |

Document test results in page specs → [`pages/`](../pages/) *(Phase 2)*.

---

## Accessibility in Page Specs

Every page document must include an Accessibility section per [page doc template](../templates/page-doc-template.md):

- Heading structure
- Focus management on load and interaction
- Screen reader announcements
- Keyboard shortcuts (if any)
- Known limitations

---

## Related Documents

- [Founding Constitution](../company/constitution.md)
- [Design Principles](principles.md)
- [Color Foundations](foundations/color.md)
- [Typography Foundations](foundations/typography.md)
- [Spacing Foundations](foundations/spacing.md)
- [Components Overview](./components-overview.md)
- [Voice and Tone — Error Messages](../brand/voice-and-tone.md#error-messages)
- [Page Doc Template](../templates/page-doc-template.md)
