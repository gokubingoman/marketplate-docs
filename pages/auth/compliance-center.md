# Compliance Center

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Auth / Onboarding (ongoing)  
**Route:** `/creator/compliance`

---

## Purpose

The Compliance Center is the creator-facing hub for permits, licenses, food handler certificates, cottage food registrations, liability insurance, and jurisdiction-specific requirements. It completes the trust onboarding trilogy after [Identity Verification](identity-verification.md) and [Kitchen Verification](kitchen-verification.md), and remains the ongoing home for renewals and expiration tracking.

Per [Compliance verification](../../product/marketplace-mechanics.md#compliance-verification): rules vary by jurisdiction; expired compliance triggers listing suspension after grace — not silent continuation.

---

## Goals

**User goals:**
- See all required and optional compliance documents in one checklist
- Understand jurisdiction-specific rules (especially cottage food categories and sales caps)
- Upload, renew, and track expiration dates with proactive reminders
- Know exactly what's blocking publication or paid orders

**Business goals:**
- Enforce category restrictions per jurisdiction at catalog level
- Track document expiration with automated suspension workflows
- Reduce support tickets via plain-language requirement descriptions
- Feed compliance review items to [Verification Queue](../admin/verification-queue.md) where human approval required

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [Cottage Food Operator](../../product/personas.md#cottage-food-operator) | Jurisdiction-heavy requirements |
| **Primary:** [Caterer](../../product/personas.md#caterer) | Insurance, business license |
| **Primary:** [Meal Prep Business](../../product/personas.md#meal-prep-business), [Baker](../../product/personas.md#baker) | Food handler certs, commercial permits |
| **Secondary:** All verified creators | Ongoing renewal management |
| **Anti-persona:** Customers | No access — compliance status surfaced as badges on creator profile only |

---

## Navigation

**Arrival paths:**
- Onboarding step 3 after identity/kitchen progress
- Dashboard nav: "Compliance" persistent item
- Email: "Your [permit] expires in 14 days"
- Listing blocked banner: "Complete compliance to publish"
- Settings → Compliance

**Exit paths:**
- Item submitted → remains on page with updated checklist status
- All required items approved → onboarding complete → creator dashboard catalog setup
- Individual requirement detail expand/collapse inline — no separate route v1
- Help articles per requirement type

---

## Layout

Dashboard-style layout within creator shell — checklist primary, detail secondary.

```
┌─────────────────────────────────────────────────────────────────┐
│  Compliance Center                                              │
│  [Kitchen: 123 Main St · Los Angeles, CA ▼]  ← jurisdiction   │
├─────────────────────────────────────────────────────────────────┤
│  Overall status: 2 of 5 required · Action needed                │
│                                                                 │
│  ┌─ Required ─────────────────────────────────────────────────┐ │
│  │ ● Business license          Approved · Expires Dec 2026    │ │
│  │ ○ Food handler certificate  Not submitted                  │ │
│  │ ○ Cottage food registration Needs review                     │ │
│  │ ○ Liability insurance       Expired · Upload renewal       │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                 │
│  ┌─ Expanded: Food handler certificate ───────────────────────┐ │
│  │  Required in California for all food handlers.             │ │
│  │  Upload your ServSafe or county-issued certificate.         │ │
│  │  [ Upload document ]  Expiration date [ MM / DD / YYYY ]  │ │
│  │  [ Submit for review ]                                      │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                 │
│  ┌─ Category eligibility (cottage food) ──────────────────────┐ │
│  │  Allowed: baked goods, jams, dry mixes                     │ │
│  │  Not allowed: refrigerated meals, meat products            │ │
│  │  Learn how this affects your catalog →                     │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                 │
│  ┌─ Optional ─────────────────────────────────────────────────┐ │
│  │  Organic certification · Kosher certification · …           │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

## Components

| Component | Usage |
|-----------|-------|
| **Step indicator** | Onboarding mode only — step 3 of 3 |
| **Status badge** | Per-item: `Not submitted`, `In review`, `Approved`, `Expiring soon`, `Expired`, `Rejected` |
| **Cards** | Requirement rows; category eligibility summary |
| **File upload** | Per requirement |
| **Date picker** | Expiration date |
| **Select** | Kitchen/jurisdiction selector if multiple locations |
| **Primary button** | "Submit for review" per item |
| **Warning toast** | Expiration reminders |
| **Segmented control** | Required / Optional tabs (optional) |
| **Verification badge** | Platform compliance status on creator profile linkage |

---

## Interactions

| Action | Behavior |
|--------|----------|
| Expand requirement row | Show description, upload, expiration, submit |
| Upload + submit | Item → `In review`; queue if human approval needed |
| Expiration date entry | Drives renewal reminders at 30/14/7 days |
| Jurisdiction switch | Reload requirement template from rule engine |
| Approved item | Row collapses to summary; green approved badge |
| Expired item | Red badge; listing restriction banner at top of page |
| Category eligibility panel | Links to catalog restrictions — SKUs in prohibited categories blocked |

**Enforcement:** Expired compliance → auto-suspend listings after grace period per [Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder).

---

## Animations

| Element | Motion |
|---------|--------|
| Row expand | 300ms accordion |
| Status badge update | Color transition + `aria-live` |
| Progress summary | Count animates on approval 200ms |
| Expiring soon | Subtle pulse on badge — disabled with `prefers-reduced-motion` |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Mobile** | Full-width checklist; expanded item takes full screen sheet |
| **Tablet/Desktop** | Master-detail: list left, detail right OR inline accordion |

Overall status banner sticky on mobile when action required.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Page load | Skeleton checklist rows |
| Jurisdiction rules fetch | Spinner on kitchen selector change |
| Document upload | Row-level progress |
| Submit item | Button spinner on expanded row |

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Missing expiration | "Enter the expiration date on your certificate." | Fix date |
| Expired on upload | "This certificate expired on [date]. Upload a current document." | New upload |
| Wrong document type | "This doesn't match the required document. Upload your [specific doc]." | Re-upload |
| Rejected | "We couldn't approve this document: [reason]." | Re-submit |
| Catalog conflict | "Your menu includes [item type] not permitted under cottage food rules in [jurisdiction]." | Edit catalog link |

Voice: actionable, non-judgmental — [Cottage food operator frustrations](../../product/personas.md#cottage-food-operator) inform copy.

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| Jurisdiction not yet determined | "Complete kitchen verification to see your compliance requirements." + link to [Kitchen Verification](kitchen-verification.md) |
| All requirements approved | "You're compliant. We'll remind you before documents expire." + next steps to publish |
| No optional docs | Optional section hidden or "No optional documents for your jurisdiction" |

---

## Permissions

| Role | Access |
|------|--------|
| Creator owner | Full compliance CRUD |
| Creator team (compliance role) | Upload and submit — `TODO(decision):` |
| Operator | Review compliance items in [Verification Queue](../admin/verification-queue.md) |
| System | Auto-suspend on expiration — logged in audit trail |

---

## Analytics

| Event | Properties |
|-------|------------|
| `compliance.center.page_view` | `jurisdiction`, `completion_pct` |
| `compliance.item.expand` | `requirement_type` |
| `compliance.item.submit` | `requirement_type` |
| `compliance.item.approved` | `requirement_type`, `time_to_approval` |
| `compliance.item.expired` | `requirement_type` |
| `compliance.renewal_reminder_click` | `days_until_expiry` |

---

## Accessibility

- Checklist uses semantic list with status text, not color alone
- Expiring/expired badges include text: "Expires in 7 days"
- Date picker keyboard accessible
- Expand/collapse with `aria-expanded` and focus management into expanded panel
- Category eligibility section readable as plain list — critical for legal understanding

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Compliance — Marketplate Creator |
| `meta robots` | `noindex, nofollow` |

---

## Future Improvements

- Automated expiration extraction from uploaded PDFs (AI assist + human confirm)
- Sales cap tracking for cottage food operators
- Integration with state cottage food registries
- Bulk upload for multi-location operators
- Customer-facing compliance summary on creator profile (approved docs as badges, not raw files)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/creators/me/compliance` | GET | Checklist, statuses, jurisdiction |
| `/api/v1/creators/me/compliance/items/:type` | PATCH | Save draft |
| `/api/v1/creators/me/compliance/items/:type/submit` | POST | Submit for review |
| `/api/v1/creators/me/compliance/items/:type/documents` | POST | Upload |
| `/api/v1/compliance/rules` | GET | Jurisdiction rule templates — `jurisdiction_id`, `kitchen_type` |
| `/api/v1/creators/me/compliance/eligibility` | GET | Allowed/prohibited product categories |

Renewal job: scheduled checks emit reminders and enforcement actions — config in [Platform Settings](../admin/platform-settings.md).

---

## Related Pages

- [Identity Verification](identity-verification.md)
- [Kitchen Verification](kitchen-verification.md)
- [Creator Signup](creator-signup.md)
- [Verification Queue](../admin/verification-queue.md)
- [Creator Admin Detail](../admin/creator-admin-detail.md)
- [Admin Dashboard](../admin/admin-dashboard.md) — compliance expiration metrics
