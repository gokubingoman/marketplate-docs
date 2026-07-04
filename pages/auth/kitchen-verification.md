# Kitchen Verification

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Auth / Onboarding  
**Route:** `/creator/onboarding/kitchen`

---

## Purpose

Kitchen Verification confirms **where food is produced** and that the production environment meets Marketplate platform standards. It answers the customer question: "Where was this made?" and links every catalog SKU to a verified production location.

Per [Kitchen verification](../../product/marketplace-mechanics.md#kitchen-verification): Marketplate verifies documentation and consistency — not a substitute for government health inspection. Kitchen types include home (cottage), commercial shared, dedicated facility, commissary, and mobile unit with commissary linkage.

---

## Goals

**User goals:**
- Declare kitchen type and production address accurately
- Upload facility documentation (registration, inspection records, photos)
- Link to commercial kitchen tenant relationship or food truck commissary where applicable
- Track verification status with same clarity as identity step

**Business goals:**
- Associate creators with verifiable production locations before listings go live
- Support multi-tenant commercial kitchens (verify once, link tenants)
- Enable mobile operator commissary + unit identification flows
- Queue complete submissions for human review in [Verification Queue](../admin/verification-queue.md)

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [Cottage Food Operator](../../product/personas.md#cottage-food-operator) | Home kitchen registration |
| **Primary:** [Commercial Kitchen Operator](../../product/personas.md#commercial-kitchen-operator) | Facility verification + tenant linkage |
| **Primary:** [Food Truck Operator](../../product/personas.md#food-truck-operator) | Commissary + mobile unit |
| **Primary:** [Independent Chef](../../product/personas.md#independent-chef), [Baker](../../product/personas.md#baker), [Meal Prep Business](../../product/personas.md#meal-prep-business) | Rented or owned production space |
| **Secondary:** [Pop-Up Kitchen](../../product/personas.md#pop-up-kitchen) | Temporary kitchen per event — may add event linkage later |

---

## Navigation

**Arrival paths:**
- Onboarding step 2 after or parallel to [Identity Verification](identity-verification.md)
- Dashboard alert: "Verify your kitchen to publish listings"
- Settings → Verification → Kitchen
- Commercial kitchen invite link (pre-filled facility) — future

**Exit paths:**
- Submit → `In review` → [Compliance Center](compliance-center.md) or dashboard
- Step nav to [Identity Verification](identity-verification.md) / [Compliance Center](compliance-center.md)
- Multiple kitchens: "Add another kitchen" → same flow with kitchen list management — v1 may limit one primary kitchen `TODO(decision):`

---

## Layout

```
┌─────────────────────────────────────────────────────────────────┐
│  Onboarding   ✓ Identity — ● Kitchen — ○ Compliance             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Kitchen verification               ┌─────────────────────────┐   │
│  Where do you prepare food          │ Status: Draft           │   │
│  for customers?                     │ Kitchen type: —         │   │
│                                     └─────────────────────────┘   │
│  Kitchen type *                                                   │
│  [ Home (cottage)          ▼ ]                                    │
│                                                                 │
│  Production address *                                             │
│  Street  [________________________]                               │
│  City    [________]  State [__]  ZIP [_____]                    │
│                                                                 │
│  ┌─ Conditional: Commercial shared kitchen ─────────────────┐   │
│  │  Link to verified kitchen  [Search facilities...      ]  │   │
│  │  OR register new facility below                          │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─ Conditional: Food truck ────────────────────────────────┐   │
│  │  Commissary kitchen  [Search...                       ]  │   │
│  │  Unit ID / plate     [________________________]          │   │
│  │  Unit photo upload   [ Upload ]                          │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Documentation                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │ Facility registration or inspection record (if available)│    │
│  │ Kitchen photos (prep area, storage)                      │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                 │
│  [        Submit for review        ]                              │
│  Save and continue later                                          │
└─────────────────────────────────────────────────────────────────┘
```

---

## Components

| Component | Usage |
|-----------|-------|
| **Step indicator** | Onboarding progress |
| **Select** | Kitchen type enum |
| **Text input** | Address fields, unit ID |
| **Search input** | Commercial kitchen / commissary lookup |
| **File upload** | Registration, inspection, photos |
| **Radio** | Primary vs. additional kitchen (future) |
| **Status badge** | Same state machine as identity |
| **Cards** | Conditional sections per kitchen type |
| **Verification badge** | "Verified Kitchen" preview — pending until approved |
| **Primary / secondary buttons** | Submit, save draft |

Kitchen type drives conditional fields — progressive disclosure per [calm interfaces](../../design-system/principles.md#1-calm-interfaces).

---

## Interactions

| Action | Behavior |
|--------|----------|
| Kitchen type select | Reveal relevant conditional block; update required docs list in status panel |
| Address entry | Address validation API; geocode for jurisdiction rules feed to [Compliance Center](compliance-center.md) |
| Facility search | Autocomplete verified commercial kitchens; selecting pre-fills address and reduces doc requirements |
| Photo upload | Minimum 2 photos for commercial; 1 for cottage where policy allows |
| Submit | Validate; status → `In review`; queue item type `kitchen` |
| Admin needs info | Inline checklist from reviewer |

**Product linkage invariant:** Every SKU must associate with verified kitchen before paid listing — enforced at catalog publish time.

---

## Animations

| Element | Motion |
|---------|--------|
| Conditional section expand | 300ms height transition |
| Kitchen type change | Crossfade required docs list |
| Upload complete | Checkmark on file row 200ms |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Address fields stacked; photo upload full-width; facility search full-screen modal |
| **Desktop** | Two-column with sticky status panel |

Map preview of pin location optional future — not v1 blocker.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Page load | Skeleton + restore draft |
| Facility search | Inline search loading spinner |
| Geocode validation | Subtle field-level validating state |
| Submit | Primary button loading |

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Invalid address | "We couldn't verify this address. Check and try again." | Fix fields |
| Unsupported kitchen type for jurisdiction | "Home kitchen sales aren't permitted for your selected products in [state]. See compliance requirements." | Link to compliance |
| Missing required photo | "Upload at least one photo of your prep area." | Upload |
| Facility not found | "Can't find your kitchen? Register it below or contact support." | Register or support |
| Rejected | "We couldn't verify this kitchen: [reason]." | Re-submit |

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| No kitchen on file | Empty form with kitchen type prompt |
| No documentation uploaded | Upload zones with plain-language examples: "Cottage food registration from your county health department" |
| In review | "Our team is reviewing your kitchen. You'll be notified when complete." |

---

## Permissions

| Role | Access |
|------|--------|
| Creator owner | CRUD on own kitchen verification draft/submit |
| Kitchen admin (commercial) | Facility-level verification; tenant linkage — `TODO(decision):` role matrix |
| Operator | Review via admin queue only |
| Customer | Sees verified kitchen badge on storefront — not this page |

---

## Analytics

| Event | Properties |
|-------|------------|
| `onboarding.kitchen.page_view` | `status`, `kitchen_type` |
| `onboarding.kitchen.type_selected` | `kitchen_type` |
| `onboarding.kitchen.facility_linked` | `facility_id`, `link_type` |
| `onboarding.kitchen.document_upload` | `document_type` |
| `onboarding.kitchen.submit` | `kitchen_type`, `jurisdiction` |
| `onboarding.kitchen.approved` | `time_to_approval_hours` |

---

## Accessibility

- Conditional sections announced when expanded (`aria-expanded`)
- Address form uses autocomplete attributes
- Photo uploads require text alternative descriptions from creator optional field for ops
- Status panel `aria-live` updates
- Search results list keyboard navigable

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Kitchen verification — Marketplate Creator |
| `meta robots` | `noindex, nofollow` |

---

## Future Improvements

- Map pin confirmation for production address
- Inspection partner API integrations
- Multi-kitchen management for creators operating at several facilities
- Pop-up event temporary kitchen linkage
- "Produced at [Kitchen Name]" badge automation for commercial tenants

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/creators/me/verification/kitchen` | GET | Status, draft, linked facility |
| `/api/v1/creators/me/verification/kitchen` | PATCH | Save draft |
| `/api/v1/creators/me/verification/kitchen/submit` | POST | Submit for review |
| `/api/v1/creators/me/verification/kitchen/documents` | POST | Upload artifacts |
| `/api/v1/kitchens/search` | GET | Search verified commercial kitchens / commissaries |
| `/api/v1/meta/kitchen-types` | GET | Types + jurisdiction rules |

**Kitchen types:** `home_cottage | commercial_shared | dedicated | commissary | mobile_unit`

Links to compliance jurisdiction rules based on geocoded address.

---

## Related Pages

- [Identity Verification](identity-verification.md)
- [Compliance Center](compliance-center.md)
- [Creator Signup](creator-signup.md)
- [Verification Queue](../admin/verification-queue.md)
- [Creator Admin Detail](../admin/creator-admin-detail.md)
