# Identity Verification

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Auth / Onboarding  
**Route:** `/creator/onboarding/identity`

---

## Purpose

Identity Verification confirms that a creator is a real person or legal entity authorized to operate a food business on Marketplate. It is the first gate in the trust onboarding pipeline and establishes accountability before kitchen and compliance verification.

Customers see the outcome as **Verified Creator** identity assurance — not raw document details. Per [Trust Model — Identity verification](../../product/marketplace-mechanics.md#identity-verification): AI extracts and flags mismatches; **human approves** final status.

---

## Goals

**User goals:**
- Complete identity verification with clear document requirements
- Understand current status at every stage (not started, in review, approved, needs info, rejected)
- Upload government ID and business entity documentation where applicable
- Resume incomplete submissions without losing progress

**Business goals:**
- Collect minimum viable identity signals for fraud prevention and accountability
- Reduce back-and-forth via upfront validation and persona-aware requirements
- Feed [Verification Queue](../admin/verification-queue.md) with complete, review-ready submissions
- Display honest status — never imply verification before human approval

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** All creator personas post-[Creator Signup](creator-signup.md) | Especially [Cottage Food Operator](../../product/personas.md#cottage-food-operator) and sole proprietors |
| **Secondary:** Creators re-verifying after material identity change | Name change, entity conversion LLC → corp |
| **Anti-persona:** Customers | No access |

---

## Navigation

**Arrival paths:**
- Post [Creator Signup](creator-signup.md) redirect
- Creator dashboard banner: "Complete identity verification"
- Email reminder for stalled onboarding
- Settings → Verification → Identity section

**Exit paths:**
- Submit success → status "In review" → continue to [Kitchen Verification](kitchen-verification.md) (allowed in parallel) or dashboard
- All steps complete + approved → next onboarding step or dashboard
- [Compliance Center](compliance-center.md) / [Kitchen Verification](kitchen-verification.md) via onboarding step nav
- Help / support article

**Onboarding step nav (persistent):**
1. **Identity** ← current
2. [Kitchen Verification](kitchen-verification.md)
3. [Compliance Center](compliance-center.md)

---

## Layout

Creator onboarding shell: step progress header + main form + status panel.

```
┌─────────────────────────────────────────────────────────────────┐
│  Onboarding   ● Identity — ○ Kitchen — ○ Compliance             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Identity verification              ┌─────────────────────────┐ │
│  Confirm who operates this          │ Status                  │ │
│  business.                          │ ○ Not submitted         │ │
│                                     │                         │ │
│  Entity type                        │ Last updated: —         │ │
│  ○ Individual  ○ LLC  ○ Other       │                         │ │
│                                     │ What we're checking     │ │
│  Legal name                         │ • Government ID         │ │
│  [________________________]         │ • Name match            │ │
│                                     │ • Business registration │ │
│  Government ID                      │   (if applicable)       │ │
│  ┌─────────────────────────┐        └─────────────────────────┘ │
│  │  Upload front & back    │                                      │
│  │  JPG, PNG, PDF · 10MB   │                                      │
│  └─────────────────────────┘                                      │
│                                                                 │
│  Business registration (LLC/other)                              │
│  ┌─────────────────────────┐                                    │
│  │  Upload document        │                                    │
│  └─────────────────────────┘                                    │
│                                                                 │
│  Tax ID / EIN (secure field)                                    │
│  [________________________]                                     │
│                                                                 │
│  [        Submit for review        ]  ← primary                 │
│  Save and continue later                                        │
└─────────────────────────────────────────────────────────────────┘
```

**Status panel** updates in real time from server — source of truth for creator-facing status.

---

## Components

| Component | Usage |
|-----------|-------|
| **Step indicator / progress** | Onboarding steps 1–3 with current step highlighted |
| **Radio** | Entity type selection |
| **Text input** | Legal name, tax ID (masked) |
| **File upload** | Government ID, business registration |
| **Status badge** | `Not started`, `Draft`, `In review`, `Needs information`, `Approved`, `Rejected` |
| **Primary button** | "Submit for review" |
| **Secondary button** | "Save and continue later" |
| **Cards** | Status panel; document upload zones |
| **Toast** | Save confirmation, submit confirmation |
| **Verification badge** (preview) | Grayed until approved — tooltip explains pending state |

---

## Interactions

| Action | Behavior |
|--------|----------|
| Entity type change | Show/hide business registration fields with 200ms expand |
| File upload | Drag-drop or click; client-side type/size validation; upload progress per file |
| Save draft | PATCH partial progress; no queue submission |
| Submit for review | Validate completeness; lock editable fields; status → `In review`; create queue item |
| Needs information | Admin request surfaces inline checklist of missing items + free-text note from reviewer |
| Approved | Status badge green; step marked complete; unlock next onboarding emphasis |
| Rejected | Show reason (plain language); allow re-upload; link to support |

**Human approval gate:** Submitting does **not** change public verification badge. Only admin approval via [Verification Queue](../admin/verification-queue.md) sets `Approved`.

---

## Animations

| Element | Motion |
|---------|--------|
| Step progress | Completed step checkmark animates 200ms on approval webhook/poll |
| Upload progress | Linear progress bar per file |
| Status change | Status badge color transition 300ms; `aria-live` announcement |
| Field reveal (entity type) | Height animate 300ms ease-out |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Status panel collapses below form or sticky bottom bar with current status |
| **Tablet** | Single column; status panel above form |
| **Desktop** | Two-column: form 65%, status 35% sticky |

Upload zones remain large touch targets on mobile (min 120px height).

---

## Loading States

| State | Treatment |
|-------|-----------|
| Page load | Skeleton for status panel + saved draft fields |
| File upload | Per-file progress bar; disable submit until complete |
| Submit | Full-form loading on primary button |
| Status polling | Subtle refresh indicator when `In review` — poll or websocket every 60s |

Show last known status immediately; refresh in background.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| File too large | "Each file must be under 10 MB." | Re-upload |
| Unsupported format | "Upload JPG, PNG, or PDF." | Re-upload |
| Blurry ID (AI flag, pre-submit) | "We couldn't read this image. Upload a clearer photo." | Re-upload |
| Missing required doc | "Upload the front of your government ID to continue." | Upload |
| Submit while incomplete | Inline summary at top | Complete fields |
| Rejected submission | "We couldn't verify your identity: [reason]. Update your documents and submit again." | Re-submit |
| Session expired | Redirect to [Login](login.md) with return URL | Sign in |

Never expose internal fraud scores to creators.

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| First visit, no draft | Form empty; status `Not started`; sidebar explains requirements |
| No files uploaded yet | Upload zone placeholder: "Upload the front of your ID" |
| In review, no action needed | Primary CTA hidden; message: "Our team is reviewing your submission. Most reviews complete within 2 business days." |

Empty is not error — calm whitespace per [design principles](../../design-system/principles.md).

---

## Permissions

| Role | Access |
|------|--------|
| Creator (owner) | Full read/write until submitted; read-only when `In review`; edit when `Needs information` or `Rejected` |
| Creator team member | `TODO(decision):` delegate upload permissions |
| Customer | No access |
| Platform operator | Review via [Verification Queue](../admin/verification-queue.md) — not this page |

Approved identity required before paid orders; draft catalog permitted.

---

## Analytics

| Event | Properties |
|-------|------------|
| `onboarding.identity.page_view` | `status`, `entity_type` |
| `onboarding.identity.entity_type_selected` | `entity_type` |
| `onboarding.identity.document_upload` | `document_type`, `success` |
| `onboarding.identity.draft_save` | — |
| `onboarding.identity.submit` | `entity_type` |
| `onboarding.identity.approved` | `time_to_approval_hours` |
| `onboarding.identity.rejected` | `reason_category` |

Trust metrics: submission completeness rate, time to approval — [Trust Metrics](../../product/success-metrics-overview.md#trust-metrics).

---

## Accessibility

- Step progress: `nav` with `aria-current="step"` on Identity
- Status changes: `aria-live="polite"` region for "Status: In review"
- File upload: keyboard accessible button alternative to drag-drop; announce upload success/failure
- Masked tax ID field with proper `autocomplete` off
- Error summary at form top with focus jump on submit failure
- Document preview images have alt text: "Uploaded government ID — front"

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Identity verification — Marketplate Creator |
| `meta robots` | `noindex, nofollow` |

---

## Future Improvements

- Third-party identity verification integration (Stripe Identity, etc.) with same human approval gate
- Real-time document quality feedback during capture (mobile camera guidance)
- Multi-language document support with translated reviewer tools
- Automatic entity lookup from business registration number — `TODO(decision):` jurisdiction

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/creators/me/verification/identity` | GET | Current status, draft data, reviewer notes |
| `/api/v1/creators/me/verification/identity` | PATCH | Save draft |
| `/api/v1/creators/me/verification/identity/submit` | POST | Submit for human review |
| `/api/v1/creators/me/verification/identity/documents` | POST | Upload document (presigned URL flow) |
| `/api/v1/creators/me/verification/identity/documents/:id` | DELETE | Remove draft document |

**Status enum:** `not_started | draft | in_review | needs_information | approved | rejected`

**Webhook/poll:** Status changes emit events for UI update and [Verification Queue](../admin/verification-queue.md).

AI assist endpoint (internal): document extraction + mismatch flags — not creator-facing.

Audit: every submit, approval, rejection logged with actor, timestamp, rationale per [Audit everything](../../product/marketplace-mechanics.md#marketplace-model-overview).

---

## Related Pages

- [Creator Signup](creator-signup.md)
- [Kitchen Verification](kitchen-verification.md)
- [Compliance Center](compliance-center.md)
- [Verification Queue](../admin/verification-queue.md)
- [Creator Admin Detail](../admin/creator-admin-detail.md)
