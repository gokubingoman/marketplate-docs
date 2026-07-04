# Creator Compliance

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/compliance`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

Compliance is the **trust and eligibility center** — where creators manage identity verification, kitchen verification, licenses, permits, and food safety documentation. Verification status is prominently displayed because [verified creators cannot accept paid orders](../../product/marketplace-mechanics.md#marketplace-model-overview) until requirements are met.

This page is especially critical for [Cottage Food Operators](../../product/personas.md#cottage-food-operator) and any creator navigating jurisdiction-specific rules.

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| Understand verification status at a glance | Increase verification completion rate |
| Upload and renew licenses and permits | Prevent expired-doc suspensions |
| Know exactly what's blocking going live | Reduce creator support tickets |
| Track compliance deadlines proactively | Maintain marketplace trust integrity |

**Primary action:** Complete the next incomplete verification step — "Upload food handler certificate," "Submit kitchen photos," etc.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Cottage Food Operator](../../product/personas.md#cottage-food-operator) | Jurisdiction rules, category limits |
| **Secondary** | [Commercial Kitchen Operator](../../product/personas.md#commercial-kitchen-operator) | Facility docs, tenant linkage |
| **Secondary** | [Food Truck Operator](../../product/personas.md#food-truck-operator) | Commissary + unit identification |
| **Anti-persona** | Customer | Trust signals visible on storefront, not raw documents |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Sidebar nav | "Compliance" |
| [Dashboard](./dashboard.md) | Verification banner, action items |
| [Catalog](./catalog.md) | Blocked listing remediation |
| Onboarding flow | Post-signup verification wizard |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Catalog](./catalog.md) | Return after unblocking publish |
| [Storefront Settings](./storefront-settings.md) | Profile complete after identity verified |
| [Dashboard](./dashboard.md) | Verification complete celebration |

### Breadcrumbs

`Dashboard → Compliance`

---

## Layout

Trust layer checklist as hero — three layers from [trust model](../../product/marketplace-mechanics.md#trust-layers). Document vault below.

```
┌─────────────────────────────────────────────────────────────────┐
│ Compliance                                                      │
├─────────────────────────────────────────────────────────────────┤
│ VERIFICATION STATUS                                             │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ Identity          Kitchen           Compliance              │ │
│ │ [✓ Verified]      [⏳ In review]    [⚠ Action needed]       │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ ┌─ Primary action card ───────────────────────────────────────┐ │
│ │ Upload your food handler certificate (expires in 14 days)   │ │
│ │                    [ Upload document ]  ← PRIMARY           │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ DOCUMENTS                                                       │
│ ┌ Document row ───────────────────────────────────────────────┐ │
│ │ Food Handler Certificate · Approved · Expires Aug 2026      │ │
│ │ [ View ] [ Replace ]                                        │ │
│ └─────────────────────────────────────────────────────────────┘ │
│ ┌ Document row ───────────────────────────────────────────────┐ │
│ │ Cottage Food Registration · Required · Not submitted        │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ KITCHEN VERIFICATION                                            │
│ Main Kitchen · 123 Commerce St · [Verified Kitchen badge]       │
│ [ Manage kitchen details ]                                      │
│                                                                 │
│ JURISDICTION: California · Cottage food rules summary [Learn]   │
└─────────────────────────────────────────────────────────────────┘
```

---

## Components

| Component | Usage | DS reference |
|-----------|-------|--------------|
| **Verification badge** | Per-layer status in hero strip | [Badges — Verification](../../design-system/components-overview.md#badges) |
| **Status badge** | Document states: Approved, In review, Expired, Required | [Badges — Status](../../design-system/components-overview.md#badges) |
| **Cards** | Primary action, document rows, kitchen block | [Cards](../../design-system/components-overview.md#cards) |
| **File upload** | Document submission | [Inputs — File upload](../../design-system/components-overview.md#inputs) |
| **Primary button** | Upload / complete next step | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Secondary button** | Manage kitchen details | [Buttons — Secondary](../../design-system/components-overview.md#buttons) |
| **Ghost button** | View document, Learn more | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |
| **Verification modal** | Explain requirements per layer | [Modals — Verification modal](../../design-system/components-overview.md#modals) |
| **Warning toast** | Expiration reminders on load | [Toasts — Warning](../../design-system/components-overview.md#toasts) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Trust layer tile** | Tap opens detail accordion or modal for that layer |
| **Primary action card** | Always surfaces highest-priority incomplete item |
| **Upload document** | File picker + document type selector; shows processing state |
| **Document row** | View preview (PDF/image); Replace triggers re-review |
| **Kitchen management** | Sub-form: address, photos, inspection docs, commissary link |
| **Jurisdiction summary** | Expandable rules; links to legal docs — not legal advice |
| **Submit for review** | Batch submit when multiple docs ready; confirmation modal |

AI assists document extraction; **human approves** final status per [trust model](../../product/marketplace-mechanics.md#identity-verification).

Status transitions: Required → Submitted → In review → Approved / Rejected (with reason + resubmit).

---

## Animations

| Trigger | Motion |
|---------|--------|
| Status approved (realtime/poll) | Badge checkmark draw | 300ms |
| Upload complete | Progress → success on row | 250ms |
| Layer complete | Subtle confetti-free success banner slide | 300ms |
| Rejection | No harsh motion — static alert banner |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Trust layers stack vertically; document rows full-width |
| **Tablet** | Trust layers 3-across compact |
| **Desktop** | Side-by-side: checklist left, document vault right |

Primary action card always above fold.

---

## Loading States

- Trust layer skeleton badges
- Document list skeleton rows
- Upload: progress bar per file
- "In review" states poll every 30s or websocket update

---

## Error States

| Error | Recovery |
|-------|----------|
| Upload failed | Retry with file size/format guidance |
| Rejected document | Inline rejection reason + resubmit CTA |
| Expired document | Warning banner; listings suspended message + grace period countdown |
| Kitchen verification failed | Detailed checklist of missing artifacts |
| API unavailable | Read-only last-known status + retry |

Suspended account: full-page blocked state with support contact — not editable compliance.

---

## Empty States

| Scenario | Message | Action |
|----------|---------|--------|
| **New creator, nothing submitted** | "Complete verification to start selling" | Primary action on first required doc |
| **All complete** | "You're fully verified" calm success state | [Go to Catalog](./catalog.md) |
| **Awaiting review only** | "We're reviewing your documents — usually within 2 business days" | — |

---

## Permissions

| Role | Access |
|------|--------|
| Owner | Full upload and manage |
| Staff — delegated | View status only by default |
| Kitchen admin (commercial) | Facility-level docs; tenant linkage |
| Platform ops | Admin console — not this surface |

---

## Analytics

| Event | Properties |
|-------|------------|
| `creator_compliance_viewed` | `identity_status`, `kitchen_status`, `compliance_status` |
| `creator_compliance_primary_action_clicked` | `document_type`, `days_until_expiry` |
| `creator_compliance_document_uploaded` | `document_type`, `file_size_kb` |
| `creator_compliance_submitted_for_review` | `document_count` |
| `creator_compliance_layer_completed` | `layer` (identity/kitchen/compliance) |
| `creator_compliance_rejection_resubmit` | `document_type`, `rejection_reason_code` |

Funnel: signup → first doc upload → fully verified → first live listing.

---

## Accessibility

- Trust layer status: text + icon; not color-only
- Document upload: keyboard accessible; announces upload progress
- Rejection reasons: `role="alert"` when first displayed
- PDF preview: accessible download link always available
- Expiration dates: machine-readable `<time datetime>`

---

## SEO

Not applicable — authenticated route.

---

## Future Improvements

- Automated renewal reminders via email/SMS
- Integration with jurisdiction databases (where available)
- Multi-kitchen management for expanding operators
- Insurance certificate verification partners
- Compliance score timeline
- Tenant invitation flow for commercial kitchens

---

## API Requirements

| Endpoint | Purpose |
|----------|---------|
| `GET /api/v1/creator/verification/status` | Three-layer summary for hero |
| `GET /api/v1/creator/compliance/documents` | Document list with status, expiry |
| `POST /api/v1/creator/compliance/documents` | Upload document |
| `GET /api/v1/creator/compliance/documents/{id}` | Preview URL |
| `POST /api/v1/creator/compliance/submit-review` | Batch submit |
| `GET /api/v1/creator/kitchens` | Kitchen verification details |
| `PATCH /api/v1/creator/kitchens/{id}` | Update kitchen artifacts |
| `GET /api/v1/creator/compliance/jurisdiction-rules` | Applicable rules summary |
| `GET /api/v1/creator/compliance/next-action` | Primary action card content |

Human review queue is admin API — out of scope for creator page.

---

## Related Pages

- [Dashboard](./dashboard.md) — verification banner source
- [Catalog](./catalog.md) — listing eligibility
- [Menu Item Editor](./menu-item-editor.md) — kitchen selector dependency
- [Storefront Settings](./storefront-settings.md) — identity/branding after verification
- [Payouts](./payouts.md) — tax identity linkage
- [Orders](./orders.md) — blocked until verified
