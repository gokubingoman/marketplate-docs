# Verification Queue

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Admin (Internal)  
**Route:** `/admin/verification`

---

## Purpose

The Verification Queue is the human approval gate for creator identity, kitchen, and compliance submissions. Operators review documents, AI-assisted extraction flags, and checklist items — then approve, reject, or request additional information with full audit trail visibility.

Per [Human approval on high stakes](../../product/marketplace-mechanics.md#marketplace-model-overview) and [Humans Decide; AI Assists](../../company/values.md#7-humans-decide-ai-assists): AI recommends; operator decides. No auto-approval of verification.

---

## Goals

**User goals (operators):**
- Process verification items efficiently with complete context in one view
- See AI flags and mismatch warnings without being overridden by them
- Approve, reject, or request info with mandatory rationale on negative actions
- Filter by type, age, SLA status, and risk signals

**Business goals:**
- Maintain verification integrity and turnaround SLAs
- Reduce false positives/negatives through structured review checklists
- Immutable audit log for every decision
- Sync decisions to creator-facing status on [Identity Verification](../auth/identity-verification.md), [Kitchen Verification](../auth/kitchen-verification.md), [Compliance Center](../auth/compliance-center.md)

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [Platform Operations (Internal)](../../product/personas.md#platform-operations-internal) — Trust & Safety | Identity and kitchen reviewers |
| **Secondary:** Creator Success | View-only or assist on incomplete submissions — `TODO(decision):` |
| **Anti-persona:** Creators | Cannot access queue; see status on their verification pages only |

---

## Navigation

**Arrival paths:**
- [Admin Dashboard](admin-dashboard.md) → Verification queue stat card
- Sidebar → "Verification"
- Direct link with filters: `/admin/verification?type=identity&status=in_review`
- Notification deep link from Slack/email ops alert — future

**Exit paths:**
- Row click → detail panel or `/admin/verification/:id`
- Creator name link → [Creator Admin Detail](creator-admin-detail.md)
- Back to [Admin Dashboard](admin-dashboard.md)
- Adjacent queue: [Moderation Queue](moderation-queue.md)

---

## Layout

Master-detail: filterable table + review panel.

```
┌──────────┬────────────────────────────────────────────────────────────┐
│ Admin    │  Verification queue                    [Filters ▼] [Search] │
│ nav      ├──────────────────────────────┬─────────────────────────────┤
│          │  Queue (47)                  │  Review: Identity           │
│          │  ┌──────────────────────────┐│  Creator: Maria's Kitchen   │
│          │  │ Type    Creator   Age SLA││  Submitted: Jul 1, 2026     │
│          │  │ Identity  Maria K.  2d ⚠ ││                             │
│          │  │ Kitchen   Batch Prep 4h ✓││  ┌─ AI assist ─────────────┐│
│          │  │ Compliance Joe's B.  1d ✓││  │ Name match: OK          ││
│          │  │ ...                      ││  │ ID expiry: Flag — review  ││
│          │  └──────────────────────────┘│  └─────────────────────────┘│
│          │  [pagination]                │  Documents [preview pane]   │
│          │                              │  □ ID verified              │
│          │                              │  □ Name matches entity      │
│          │                              │  Internal notes             │
│          │                              │  [Request info] [Reject]    │
│          │                              │  [ Approve ]  ← primary     │
└──────────┴──────────────────────────────┴─────────────────────────────┘
```

**Mobile/tablet:** Table full screen → tap row opens full-screen review sheet.

---

## Components

| Component | Usage |
|-----------|-------|
| **Data table** | Queue list with sort/filter |
| **Status badge** | Item type, SLA, AI flag severity |
| **Cards** | AI assist summary, checklist |
| **File preview** | Inline PDF/image viewer for documents |
| **Checkbox** | Review checklist items |
| **Textarea** | Internal notes, creator-visible request-info message |
| **Primary button** | "Approve" |
| **Secondary buttons** | "Request information", "Reject" |
| **Destructive button** | "Reject" — requires confirmation modal |
| **Select / filters** | Type, status, SLA, jurisdiction |
| **Search input** | Creator name, ID |
| **Modal** | Reject confirmation with rationale required |
| **Pagination** | Table pages |
| **Avatar** | Creator thumbnail in detail panel |

---

## Interactions

| Action | Behavior |
|--------|----------|
| Select row | Load detail panel; mark item as "in progress" for operator — `TODO(decision):` locking |
| Approve | Validate checklist complete; confirm modal if AI flags unresolved; write audit; update creator status → `Approved`; remove from queue |
| Request info | Require creator-visible message; status → `Needs information`; notify creator |
| Reject | Require rationale (creator-visible + internal); status → `Rejected`; audit log |
| AI flag dismiss | Operator notes reason — logged in audit |
| Document preview | Zoom, rotate, download (logged) |
| Bulk actions | Not v1 — future for compliance expirations |

**Audit trail:** Every action records `{ operator_id, action, rationale, timestamp, item_id, before_status, after_status }` visible in [Creator Admin Detail](creator-admin-detail.md).

---

## Animations

| Element | Motion |
|---------|--------|
| Row select | Detail panel slide in 300ms |
| Approve success | Row fades out 200ms; next item auto-select optional |
| AI flag expand | Accordion 200ms |
| Modal | Standard 300ms fade + scale |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Desktop** | Master-detail side by side |
| **Tablet** | Stacked; detail as overlay |
| **Mobile** | List only; full-screen review on tap |

Document preview critical on desktop — minimum 1024px recommended for reviewers.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Table load | Skeleton rows |
| Detail load | Skeleton in panel while fetching documents |
| Document preview | Spinner in preview pane |
| Action submit | Disable buttons; spinner on Approve/Reject |

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Concurrent review lock | "Another operator is reviewing this item." | View read-only or skip |
| Approve with unresolved required checklist | "Complete the review checklist before approving." | Check items |
| Missing reject rationale | "Enter a reason the creator will see." | Fill field |
| Document load failure | "Document couldn't load. Download or retry." | Retry/download |
| API failure on action | "Action failed. Your notes were saved locally." — `TODO(decision):` draft save | Retry |

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| Queue empty (filtered) | "No items match these filters." + clear filters |
| Queue completely empty | "All verification items reviewed." + link to dashboard celebration-free message |
| No row selected | Detail panel: "Select an item to review." |

---

## Permissions

| Role | Access |
|------|--------|
| **Trust & Safety reviewer** | Full approve/reject/request |
| **Senior reviewer** | Override rejected items; escalate |
| **Creator Success** | View queue; add internal notes only — `TODO(decision):` |
| **Read-only** | View without actions |

Separation of duties: operator cannot review own test accounts in production.

---

## Analytics

| Event | Properties |
|-------|------------|
| `admin.verification.queue_view` | `filters` |
| `admin.verification.item_open` | `type`, `age_hours`, `ai_flag_count` |
| `admin.verification.approve` | `type`, `time_in_queue_hours`, `ai_flags_dismissed` |
| `admin.verification.reject` | `type`, `reason_category` |
| `admin.verification.request_info` | `type` |

Quality metrics: false positive/negative rates sampled via QA review process.

---

## Accessibility

- Table: proper headers, sort announced
- Detail panel: focus trap when modal on mobile
- Document viewer keyboard shortcuts documented
- Checklist checkboxes labeled with requirement text
- Approve/Reject: distinct focus order; destructive action not default
- Color-blind safe SLA indicators (icon + text)

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Verification queue — Marketplate Admin |
| `meta robots` | `noindex, nofollow` |

---

## Future Improvements

- Side-by-side document comparison (ID vs. selfie)
- Queue assignment and workload balancing
- QA sampling workflow for approved items
- Integration with third-party identity verification results
- Bulk compliance expiration review
- Keyboard shortcuts for power reviewers (j/k navigate, a approve)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/admin/verification/queue` | GET | Paginated list with filters |
| `/api/v1/admin/verification/items/:id` | GET | Full item + documents + AI flags |
| `/api/v1/admin/verification/items/:id/approve` | POST | Approve with checklist |
| `/api/v1/admin/verification/items/:id/reject` | POST | Reject with rationale |
| `/api/v1/admin/verification/items/:id/request-info` | POST | Request info message |
| `/api/v1/admin/verification/items/:id/notes` | POST | Internal note |
| `/api/v1/admin/verification/items/:id/documents/:docId/url` | GET | Signed preview URL |

Webhook to creator status on decision. AI flags from internal ML service — not editable, only dismissable with note.

---

## Related Pages

- [Admin Dashboard](admin-dashboard.md)
- [Creator Admin Detail](creator-admin-detail.md)
- [Identity Verification](../auth/identity-verification.md)
- [Kitchen Verification](../auth/kitchen-verification.md)
- [Compliance Center](../auth/compliance-center.md)
- [Platform Settings](platform-settings.md) — SLA thresholds
