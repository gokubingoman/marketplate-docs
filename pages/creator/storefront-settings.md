# Creator Storefront Settings (Brand & Fulfillment)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/dashboard/storefront`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

Storefront Settings is where creators shape their **public presence** — brand name, bio, photos, slug, fulfillment defaults, pickup location, and social links. What is configured here renders on the customer-facing [Creator Storefront](../customer/creator-storefront.md) and drives discovery conversion.

A complete storefront is a trust and discovery requirement: customers decide whether to order based on this page before viewing [Catalog](./catalog.md) items. Profile completeness prompts on [Dashboard](./dashboard.md) link here.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| Present a professional, trustworthy brand to customers | Improve storefront conversion and GMV |
| Configure pickup location and fulfillment messaging | Reduce pickup confusion and no-shows |
| Manage storefront slug and shareable link | Enable creator-led marketing |
| Preview changes before publishing | Prevent embarrassing live mistakes |
| Complete profile checklist for verification standing | Improve catalog quality and trust signals |

**Primary action on this screen:** Save profile changes or "Preview storefront" when editing — contextual; onboarding creators see "Complete your profile" as primary until checklist done.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Independent Chef](../../product/personas.md#independent-chef) | Personal brand, story-driven bio |
| **Secondary** | [Baker](../../product/personas.md#baker) | Hero photos of products |
| **Secondary** | [Food Truck Operator](../../product/personas.md#food-truck-operator) | Location and schedule messaging |
| **Anti-persona** | Customer editing a profile | Customer account settings are separate surface |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Sidebar nav | "Storefront" |
| [Dashboard](./dashboard.md) | Profile completeness prompt; "Share storefront link" |
| [Catalog](./catalog.md) | "Preview storefront" |
| [Availability](./availability.md) | Pickup location cross-link |
| Onboarding checklist | Post-verification profile setup |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Creator Storefront](../customer/creator-storefront.md) | Preview / View storefront (new tab) |
| [Availability](./availability.md) | Fulfillment schedule link |
| [Catalog](./catalog.md) | Menu management |
| [Compliance](./compliance.md) | Kitchen address mismatch banner |
| [Reviews](./reviews.md) | Reviews tab preview link |

### Breadcrumbs

`Dashboard → Storefront settings`

---

## Layout

Form sections with live preview panel on desktop. Mobile: form-first with floating "Preview" action.

```
┌─────────────────────────────────────────────────────────────────┐
│ Dashboard → Storefront settings              [ Preview live ↗ ] │
├──────────────────────────────┬──────────────────────────────────┤
│ Brand                        │ Preview                          │
│ ┌──────────────────────────┐ │ ┌────────────────────────────┐ │
│ │ Store name *             │ │ │ [Cover photo]              │ │
│ │ Maria's Kitchen          │ │ │ Maria's Kitchen ✓ Verified │ │
│ │                          │ │ │ Sourdough & seasonal bakes │ │
│ │ Tagline                  │ │ │ ★ 4.8 · 124 reviews        │ │
│ │ Short bio *              │ │ │ [Menu preview...]          │ │
│ │ [textarea]               │ │ └────────────────────────────┘ │
│ │                          │ │                                │
│ │ Slug: marketplate.com/   │ │ Profile completeness: 85%      │
│ │ creators/marias-kitchen  │ │ · Add cover photo              │
│ └──────────────────────────┘ │                                │
│ Photos                       │                                │
│ [ Cover photo ] [ Profile ]  │                                │
│ [ Gallery (3/6) ]            │                                │
│ Fulfillment                  │                                │
│ Pickup location *            │                                │
│ Default type: Pickup ▾       │                                │
│ Customer instructions        │                                │
│ [ Save changes ] ← PRIMARY   │                                │
└──────────────────────────────┴──────────────────────────────────┘
```

**Sections:**

1. Brand — name, tagline, bio, slug
2. Photos — cover, profile, gallery
3. Fulfillment — location, type, customer-facing instructions
4. Links — Instagram, website (optional)
5. Completeness meter — checklist of missing trust/discovery fields

---

## Components

| Component | Usage on this page | DS reference |
|-----------|-------------------|--------------|
| **Sidebar nav** | Creator OS navigation | [Navigation — Sidebar](../../design-system/components-overview.md#navigation) |
| **Text input** | Name, tagline, slug, URLs | [Inputs](../../design-system/components-overview.md#inputs) |
| **Textarea** | Bio, pickup instructions | [Inputs — Textarea](../../design-system/components-overview.md#inputs) |
| **Image upload** | Cover, profile, gallery with crop | [File upload — Image](../../design-system/components-overview.md#file-upload) |
| **Select** | Default fulfillment type | [Selects](../../design-system/components-overview.md#selects) |
| **Address input** | Pickup location with autocomplete | [Inputs — Address](../../design-system/components-overview.md#inputs) |
| **Verification badge** | Preview shows verified state | [Badges — Verification](../../design-system/components-overview.md#badges) |
| **Progress indicator** | Profile completeness | [Progress](../../design-system/components-overview.md#progress) |
| **Primary button** | Save changes | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | Preview storefront, copy link | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Preview card** | Live-ish storefront mock | [Cards](../../design-system/components-overview.md#cards) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Save changes** | Validate required fields; POST; success toast; refresh preview |
| **Preview live** | Opens `/creators/{slug}` in new tab — current saved state |
| **Copy storefront link** | Clipboard copy with toast |
| **Slug edit** | Availability check debounced; reserved words blocked; confirm if changing live slug |
| **Image upload** | Crop modal → upload → preview update |
| **Address change** | Warning if differs from [Kitchen Verification](../auth/kitchen-verification.md) — may trigger compliance review |
| **Completeness item tap** | Scroll to relevant field |
| **Dirty state** | Warn on navigate; sticky save on mobile |

**Slug rules:** Per [Information Architecture](../information-architecture.md#canonical-slug-rules) — unique, policy-validated, creator-chosen.

---

## Animations

| Trigger | Motion | Duration |
|---------|--------|----------|
| Preview update on save | Crossfade preview content | 300ms |
| Image upload complete | Thumbnail fade in | 200ms |
| Completeness meter | Width transition | 250ms |
| Slug available check | Subtle checkmark | 150ms |

Respect `prefers-reduced-motion`: instant preview swap.

---

## Responsive Behaviour

| Breakpoint | Layout changes |
|------------|----------------|
| **Mobile (320–767px)** | Single column; preview via modal or new tab; sticky save |
| **Tablet (768–1023px)** | Preview below form |
| **Desktop (1024px+)** | Split: form ~60%, preview ~40% sticky |

All form fields accessible without horizontal scroll on 320px.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| **Initial load** | Skeleton form sections |
| **Preview panel** | Skeleton storefront mock |
| **Image upload** | Thumbnail placeholder with progress |
| **Slug check** | Inline spinner next to field |
| **Save** | Button loading state |

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| **Load failed** | "Storefront settings couldn't load" | Retry |
| **Slug taken** | "This URL is already in use" | Choose different slug |
| **Slug invalid** | "Use letters, numbers, and hyphens only" | Fix input |
| **Image upload failed** | "Photo couldn't upload. Try again." | Retry |
| **Address invalid** | "Enter a valid pickup address" | Fix address |
| **Save failed** | "Changes couldn't save" | Retry |
| **Moderation flag on bio/photo** | "This content needs review before publishing" | Edit or wait |

User-generated content subject to [Moderation Queue](../admin/moderation-queue.md) review.

---

## Empty States

| Scenario | Display | Primary action |
|----------|---------|----------------|
| **New creator, blank profile** | Completeness at 0%; guided checklist | Fill store name |
| **No photos** | Placeholder avatars in preview | [Add cover photo] |
| **No bio** | Preview shows "Add a bio to tell customers about your food" | Focus bio field |

Incomplete profile does not block verification but affects discovery ranking — `TODO(decision):`.

---

## Permissions

| Role | Access |
|------|--------|
| **Creator owner** | Full edit, slug change, photos |
| **Creator staff — catalog** | Read-only storefront preview |
| **Creator staff — orders** | No access |
| **Unverified creator** | Can edit draft profile; storefront not public until verified |
| **Suspended creator** | Read-only; storefront hidden from customers |

Public visibility requires verified status + minimum profile fields.

---

## Analytics

| Event | Properties | Purpose |
|-------|------------|---------|
| `creator_storefront_settings_viewed` | `completeness_pct` | Profile adoption |
| `creator_storefront_settings_saved` | `fields_changed[]` | Edit patterns |
| `creator_storefront_preview_clicked` | `source` (inline, header) | Validation behavior |
| `creator_storefront_link_copied` | — | Marketing activation |
| `creator_storefront_slug_changed` | — | Rebrand frequency |
| `creator_storefront_photo_uploaded` | `photo_type` | Visual completeness |

Funnel: profile complete → storefront shared → first order from direct link.

---

## Accessibility

| Requirement | Implementation |
|-------------|----------------|
| **Page title** | `<h1>Storefront settings</h1>` |
| **Form sections** | `<fieldset>` + `<legend>` for Brand, Photos, Fulfillment |
| **Required fields** | `aria-required="true"`; error summary on save failure |
| **Image uploads** | Alt text required for profile/cover before save |
| **Preview** | `aria-label="Storefront preview"` — decorative mock, not interactive |
| **Copy link** | Announces "Link copied" via live region |

---

## SEO

Creator storefront **public pages** are indexable per IA — this settings page is not.

| Element | Value |
|---------|-------|
| Settings page | `noindex, nofollow` |
| Public storefront | Controlled via creator opt-in on this page — `TODO(decision):` index toggle |

---

## Future Improvements

- SEO fields: meta description, Open Graph image override
- Storefront themes / accent colors (within brand guidelines)
- Video introduction embed
- "Featured items" picker for storefront hero
- A/B headline testing — future
- Multi-language bio support
- Vacation mode messaging synced with [Availability](./availability.md)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `GET /api/v1/creator/storefront` | GET | Current settings + completeness |
| `PATCH /api/v1/creator/storefront` | PATCH | Save profile fields |
| `POST /api/v1/creator/storefront/photos` | POST | Upload `{ type, file }` |
| `DELETE /api/v1/creator/storefront/photos/{id}` | DELETE | Remove gallery image |
| `GET /api/v1/creator/storefront/slug/check` | GET | `?slug=` availability |
| `GET /api/v1/creator/storefront/preview` | GET | Render payload for preview panel |

Public storefront served at `GET /api/v1/storefronts/{slug}` — separate customer API.

---

## Related Pages

- [Dashboard](./dashboard.md) — profile completeness prompts
- [Catalog](./catalog.md) — menu on storefront
- [Availability](./availability.md) — pickup windows and capacity
- [Reviews](./reviews.md) — rating displayed on storefront
- [Compliance](./compliance.md) — kitchen address alignment
- [Analytics](./analytics.md) — storefront conversion (future)
- Customer-facing: [Creator Storefront](../customer/creator-storefront.md)
- Onboarding: [Kitchen Verification](../auth/kitchen-verification.md)
- Admin: [Creator Admin Detail](../admin/creator-admin-detail.md) — internal profile view
- Admin: [Moderation Queue](../admin/moderation-queue.md) — content review
