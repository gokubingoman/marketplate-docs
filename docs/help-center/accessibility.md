# Accessibility

> Help Center · Accessibility  
> Route: `/help/accessibility`  
> Last updated: 2026-07-03

## Overview

Marketplate is committed to making the marketplace usable by everyone — including people who use screen readers, keyboard navigation, voice control, magnification, and reduced-motion preferences. Accessibility is built into product requirements, not added afterward.

This article describes accessibility features, how to use them, known limitations, and how to request accommodation or report barriers.

---

## Step-by-step guidance

### Step 1: Navigate with keyboard

1. Use **Tab** to move between interactive elements in logical order.
2. **Enter** or **Space** activates buttons and toggles FAQ accordions on Help.
3. **Escape** closes modals and dropdowns.
4. Skip link at page top jumps to main content — first Tab on most pages.

[Screenshot: Visible skip link "Skip to main content" focused with keyboard focus ring on Home page]

Help page keyboard behavior per [Help spec](../../pages/customer/help.md): accordion headers use arrow keys; support form logical tab order.

### Step 2: Use a screen reader

1. Landmarks identify regions: banner (nav), main, search, contentinfo (footer).
2. Headings structure content — h1 "Help center" on Help; nested h2/h3 in articles.
3. Verification badges include text labels — not icon-only.
4. Order status timelines announce current step via aria-current.

[Screenshot: Screen reader rotor showing landmark list — banner, main, search, contentinfo]

Form errors use `role="alert"` summaries. Search announces result count via live region.

### Step 3: Enable reduced motion

1. Enable **Reduce motion** in OS settings (iOS, Android, macOS, Windows).
2. Marketplate respects `prefers-reduced-motion`: instant accordion toggles, no crossfade animations on Help search.
3. Essential state changes remain visible without animation.

[Screenshot: iOS Accessibility settings Reduce Motion toggle enabled]

### Step 4: Adjust visual display

1. Browser zoom to 200% — layouts reflow without horizontal scroll on core flows (checkout, order detail, help).
2. Dark mode follows system preference where supported.
3. Text meets contrast standards per [Accessibility Standards](../../design-system/accessibility-standards.md).

[Screenshot: Checkout page at 200% browser zoom showing reflowed single-column layout with readable text]

### Step 5: Report an accessibility barrier

1. Note page URL, feature, assistive technology (NVDA, VoiceOver, etc.), and description of barrier.
2. Contact support → **Accessibility** or **General inquiry** with subject "Accessibility barrier."
3. We track reports and prioritize fixes affecting core purchase and order flows.

[Screenshot: Contact support form with Accessibility barrier description field and assistive technology dropdown]

---

## Feature reference

| Feature | Support |
|---------|---------|
| Keyboard navigation | Core flows — browse, cart, checkout, orders, help, account |
| Screen reader labels | Buttons, forms, badges, status badges, accordions |
| Focus indicators | Visible focus rings on interactive elements |
| Color contrast | WCAG 2.1 AA target for text and UI components |
| Reduced motion | OS setting respected |
| Touch targets | Minimum 44×44pt on mobile |
| Alt text | Menu photos and storefront images require creator alt text field |
| Captions | Video content (future) — captions required before publish |

---

## Common issues

| Issue | Likely cause | What to do |
|-------|--------------|------------|
| Focus trapped in modal | Modal open | Press Escape; report if cannot exit |
| Screen reader skips content | Missing heading structure | Report URL — engineering fix |
| Low contrast in creator photo overlay | User-generated content | Report specific storefront |
| Keyboard cannot reach element | Bug or custom overlay | Report with browser and AT version |
| Notification not announced | OS notification settings | Enable accessible notifications in device settings |

---

## FAQs

### Does Marketplate meet WCAG 2.1 AA?

WCAG 2.1 AA is our target standard for platform-controlled UI. Creator-uploaded content (photos, PDF menus) is creator responsibility with platform fields for alt text.

### Can I complete checkout with VoiceOver alone?

Yes — checkout designed for screen reader completion. Report specific failures — we treat as priority defects.

### Are allergen warnings accessible?

Allergen acknowledgment at checkout uses text labels, not color alone. Allergen lists structured for screen reader readout on menu items.

### How do I request an accommodation not yet supported?

Contact support describing needed accommodation. We review for reasonable implementation timeline.

---

## Related articles

- [Getting started](getting-started.md) — Core flows
- [Contact support](contact-support.md) — Report barriers
- [Help page spec — Accessibility section](../../pages/customer/help.md#accessibility)
- [Accessibility Standards](../../design-system/accessibility-standards.md)
- [Design System Principles](../../design-system/principles.md)

---

## Escalation guidance

Report accessibility barriers via support:

**Support category:** General inquiry (Accessibility barrier in subject)  
**Expected response:** Within 24 hours; critical purchase-flow blockers prioritized for engineering  
**Include:**

- Page URL or flow step
- Assistive technology name and version (e.g., VoiceOver on iOS 17)
- Browser and OS if web
- Description of expected vs. actual behavior
- Screenshot or screen recording if helpful

We do not require disclosure of disability to report barriers. Feedback improves the platform for everyone.
