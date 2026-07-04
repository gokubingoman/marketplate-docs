# Inputs

> Form controls for collecting text, selections, dates, and files across registration, checkout, and dashboard flows.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Inputs collect user data — text, selections, uploads, and dates. They are the primary interaction surface for trust-critical flows: identity verification, allergen acknowledgment, pickup scheduling, and payment-adjacent information.

### Types

| Type | Usage | HTML element |
|------|-------|--------------|
| **Text input** | Names, emails, search, quantities | `<input type="text">` |
| **Textarea** | Descriptions, special instructions | `<textarea>` |
| **Select / dropdown** | Pickup windows, categories, filters | `<select>` or custom listbox |
| **Checkbox** | Multi-select, allergen acknowledgment, consent | `<input type="checkbox">` |
| **Radio** | Single-select from few options (≤ 5) | `<input type="radio">` |
| **Date / time picker** | Pickup scheduling, menu availability | `<input type="date/time">` or custom |
| **File upload** | Verification documents, menu photos | `<input type="file">` |
| **Search input** | Menu search, creator discovery | `<input type="search">` |

**Appears on:** Registration, verification, menu management, checkout, search.

→ Inventory context: [components-overview.md](../components-overview.md#inputs)

---

## Anatomy

### Text input / textarea / search

```
Label *                          ← Label (required indicator)
┌────────────────────────────────┐
│ [Icon]  Placeholder / value    │  ← Input field
└────────────────────────────────┘
Helper text                      ← Helper (default state)
Error message                    ← Error (invalid state only)
```

| Part | Required | Description |
|------|----------|-------------|
| **Label** | Yes | Visible `<label for="id">` — never placeholder-only |
| **Required indicator** | Conditional | Asterisk + "Required" in sr-only for required fields |
| **Field** | Yes | Input element with consistent height and padding |
| **Leading icon** | No | Search, email — decorative when label present |
| **Helper text** | No | Format hints, character limits — `text-tertiary` |
| **Error message** | Conditional | Shown on invalid; linked via `aria-describedby` |

### Checkbox / radio group

```
Group label (legend)
  ☐ Option label
     Optional description
  ☐ Option label
```

Use `<fieldset>` + `<legend>` for groups of 2+ related options.

---

## Sizes

| Size | Height | Horizontal padding | Typography | Usage |
|------|--------|-------------------|------------|-------|
| **md** | 44px | `space-4` | `text-body-md` | Default — all forms |
| **sm** | 36px | `space-3` | `text-body-sm` | Dashboard tables, inline filters |

**Textarea min-height:** 120px (≈ 5 lines at `text-body-md`). Resizable vertically only.

**Border radius:** `radius-md` (8px).

**Label spacing:** `space-2` below label to field; `space-1` below field to helper/error.

---

## States

### Text input / textarea / select

| State | Background | Border | Text | Helper/error |
|-------|------------|--------|------|--------------|
| **Default** | `surface-default` / `neutral-0` | `border-default` 1px | `text-primary` | `text-tertiary` helper |
| **Hover** | `surface-default` | `color-neutral-400` 1px | `text-primary` | — |
| **Focus** | `surface-default` | `border-focus` 2px | `text-primary` | — |
| **Filled** | `surface-default` | `border-default` | `text-primary` | — |
| **Disabled** | `color-neutral-100` | `border-default` | `text-disabled` | — |
| **Read-only** | `surface-subtle` | `border-subtle` | `text-primary` | — |
| **Error** | `color-error-subtle` | `border-error` 1px | `text-primary` | `color-error-default` |
| **Error + focus** | `color-error-subtle` | `border-error` 2px + focus ring | `text-primary` | `color-error-default` |

**Placeholder color:** `text-tertiary` (`color-neutral-600`). Placeholders are supplementary — never replace labels.

### Checkbox / radio

| State | Control | Label |
|-------|---------|-------|
| **Default** | `border-default` border, `surface-default` fill | `text-primary` |
| **Hover** | `color-trust-muted` border | `text-primary` |
| **Focus** | `border-focus` outline on control | `text-primary` |
| **Checked** | `color-trust-default` fill + check/dot | `text-primary` |
| **Disabled** | `color-neutral-200` | `text-disabled` |
| **Error** | `border-error` | `text-primary` + group error message |

### File upload

| State | Drop zone border | Background |
|-------|------------------|------------|
| **Default** | `border-default` dashed 2px | `surface-subtle` |
| **Hover/dragover** | `color-trust-default` dashed | `color-trust-subtle` |
| **Error** | `border-error` dashed | `color-error-subtle` |
| **Disabled** | `border-default` | `color-neutral-100` |

---

## Validation Patterns

| Pattern | When | Behavior |
|---------|------|----------|
| **Inline on blur** | Field-level format errors (email, phone) | Show error below field; `aria-invalid="true"` |
| **Inline on change** | Checkbox acknowledgment (allergens) | Error clears when checked |
| **Summary on submit** | Form-level failure | Focus moves to error summary (`role="alert"`) at form top |
| **Success** | Rare — verification approved | Inline success text in `color-success-default`; no green field borders |

Error copy: specific, actionable, calm → [voice and tone — error messages](../../brand/voice-and-tone.md#error-messages).

**Allergen acknowledgment:** Required checkbox, not pre-checked, with explicit label — [accessibility standards](../accessibility-standards.md#allergen--food-safety-critical).

---

## Component Tokens

| Token | Maps to | Context |
|-------|---------|---------|
| `input-background` | `surface-default` | Field fill |
| `input-border` | `border-default` | Default border |
| `input-border-focus` | `border-focus` | Focus ring |
| `input-border-error` | `border-error` | Invalid state |
| `input-text` | `text-primary` | Value text |
| `input-placeholder` | `text-tertiary` | Placeholder |
| `input-label` | `text-ui-md` + `text-primary` | Field labels |
| `input-helper` | `text-body-sm` + `text-tertiary` | Helper text |
| `input-error-text` | `text-body-sm` + `color-error-default` | Error messages |

→ Semantic source: [color foundations](../foundations/color.md)

---

## Token Usage Summary

| Property | Token |
|----------|-------|
| Label | `text-ui-md`, weight 500, `text-primary` |
| Input text | `text-body-md`, `text-primary` |
| Helper / error | `text-body-sm` |
| Vertical padding | `space-3` |
| Horizontal padding | `space-4` |
| Field group gap | `space-6` |
| Section gap | `space-10` |
| Submit button top margin | `space-8` |

→ Typography: [typography foundations](../foundations/typography.md)  
→ Spacing: [spacing foundations](../foundations/spacing.md)

---

## Accessibility

Target: **WCAG 2.2 AA** → [accessibility standards](../accessibility-standards.md)

| Requirement | Implementation |
|-------------|----------------|
| **Visible labels** | Every input has associated `<label>` |
| **Required fields** | Visible indicator + `aria-required="true"` |
| **Error association** | `aria-invalid="true"` + `aria-describedby` → error element ID |
| **Error summary** | On submit failure, focus first error or summary with `role="alert"` |
| **Group labels** | `<fieldset>` + `<legend>` for checkbox/radio groups |
| **Autocomplete** | `autocomplete` attributes on personal data fields |
| **Search** | `<input type="search">` with accessible name "Search menu" etc. |
| **Custom select** | ARIA listbox pattern: `role="listbox"`, `aria-expanded`, keyboard per [keyboard patterns](../accessibility-standards.md#keyboard-patterns) |
| **File upload** | Expose file name and size after selection; error for invalid type/size |
| **Touch target** | 44px height for md size; checkbox/radio hit area includes label text |

Date/time pickers must be operable by keyboard. Native inputs preferred until custom picker meets full ARIA pattern.

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| **Mobile (320–767px)** | Full-width fields (`width: 100%`). Labels above inputs (never inline). Select opens native picker where supported. Date/time uses native controls. Form sections stack with `space-6` gap. |
| **Tablet (768–1023px)** | Two-column layout for related short fields (first name / last name) when container ≥ `container-sm`. |
| **Desktop (1024px+)** | Multi-column form grids in dashboard. Max form width: `container-sm` (640px) for customer-facing flows. |

**Search input:** Full-width on mobile storefront; fixed width (280–320px) in desktop nav bar.

**Inline vs. summary errors:** Always show inline error below field. Summary at top for 3+ errors or on submit failure.

---

## Do / Don't

### Do

- Put **labels above** fields for scannability
- Validate **on blur** for format; validate **on submit** for required
- Use **helper text** for format expectations — "MM/DD/YYYY"
- Group related fields with **fieldset/legend**
- Use **native inputs** when they meet design and a11y requirements
- Require **explicit allergen acknowledgment** at checkout

### Don't

- Use placeholder as the only label
- Pre-check consent or allergen acknowledgment checkboxes
- Show green success borders on valid fields — unnecessary noise
- Disable submit without explaining what's incomplete
- Use radio buttons for more than 5 options — use select instead
- Hide required field indicators — mark all required fields consistently

---

## Related Documents

- [Design Principles](../principles.md)
- [Components Overview](../components-overview.md#inputs)
- [Color Foundations](../foundations/color.md)
- [Typography Foundations](../foundations/typography.md)
- [Spacing Foundations](../foundations/spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Buttons](buttons.md) — form submit actions
- [Voice and Tone — Error Messages](../../brand/voice-and-tone.md#error-messages)
