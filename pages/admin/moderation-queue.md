# Moderation Queue

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Admin (Internal)  
**Route:** `/admin/moderation`

---

## Purpose

The Moderation Queue handles content and trust moderation items — flagged reviews, listing policy violations, inappropriate imagery, harassment in messages, suspected fraud signals, and community reports. Operators investigate context and take enforcement actions with documented rationale.

Per [Reviews & community moderation](../../product/marketplace-mechanics.md#reviews--community) and [Trust enforcement ladder](../../product/marketplace-mechanics.md#trust-enforcement-ladder): progressive enforcement from education through permanent removal. **No pay-to-remove reviews.**

AI classifiers recommend priority and category; **human decides** enforcement action.

---

## Goals

**User goals (operators):**
- Triage moderation items by severity and type
- View full context (content, reporter, history, related orders)
- Apply consistent enforcement actions with audit trail
- Escalate edge cases without losing case continuity

**Business goals:**
- Protect review integrity and customer safety
- Maintain marketplace trust signals quality
- Track moderation SLA and appeal outcomes
- Feed platform health metrics on [Admin Dashboard](admin-dashboard.md)

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [Platform Operations (Internal)](../../product/personas.md#platform-operations-internal) — Trust & Safety | Content moderators |
| **Secondary:** Legal/compliance consult on edge cases | Read + comment — `TODO(decision):` |
| **Anti-persona:** Creators reviewing competitors | Creators report via in-product flow; no queue access |

---

## Navigation

**Arrival paths:**
- [Admin Dashboard](admin-dashboard.md) moderation stat
- Sidebar → "Moderation"
- Automated alert: high-severity flag
- Filter URLs: `/admin/moderation?type=review&severity=high`

**Exit paths:**
- Item detail → related [Creator Admin Detail](creator-admin-detail.md)
- Order-linked items → [Dispute Detail](dispute-detail.md) if dispute opened
- [Verification Queue](verification-queue.md) if identity fraud suspected
- Dashboard return

---

## Layout

Similar master-detail to [Verification Queue](verification-queue.md) with moderation-specific context panel.

```
┌──────────┬────────────────────────────────────────────────────────────┐
│ Admin    │  Moderation queue                      [Filters ▼] [Search] │
│ nav      ├──────────────────────────────┬─────────────────────────────┤
│          │  ┌──────────────────────────┐│  Review report #M-9281      │
│          │  │ Sev  Type      Subject Age││  Reported: inappropriate    │
│          │  │ HIGH Review    Maria's  2h││  language in review         │
│          │  │ MED  Listing   Joe's   1d││                             │
│          │  │ LOW  Message   Order #…  ││  ┌─ Content under review ──┐│
│          │  └──────────────────────────┘│  │ [quoted review text]      ││
│          │                              │  └─────────────────────────┘│
│          │                              │  Reporter · Order · History │
│          │                              │  AI: 87% policy match       │
│          │                              │  Policy: Harassment §4.2    │
│          │                              │  Action:                    │
│          │                              │  ○ Dismiss  ○ Warn creator  │
│          │                              │  ○ Remove content           │
│          │                              │  ○ Suspend account          │
│          │                              │  Rationale (required)       │
│          │                              │  [ Submit decision ]        │
└──────────┴──────────────────────────────┴─────────────────────────────┘
```

---

## Components

| Component | Usage |
|-----------|-------|
| **Data table** | Queue with severity, type, age |
| **Status badge** | Severity (high/med/low), status (open/in progress/resolved) |
| **Cards** | Content preview, context, policy reference |
| **Radio** | Enforcement action selection |
| **Textarea** | Rationale (required for non-dismiss) |
| **Primary button** | "Submit decision" |
| **Modal** | Confirm suspend / permanent removal |
| **Avatar** | Reporter and subject |
| **Review card** | Full review context |
| **Pagination** | Table |
| **Search / filters** | Type, severity, status, creator |

---

## Interactions

| Action | Behavior |
|--------|----------|
| Open item | Load content + history; auto-mark in progress |
| Dismiss | False positive — require brief internal note; close item |
| Warn creator | Send templated warning; log on [Creator Admin Detail](creator-admin-detail.md) |
| Remove content | Hide review/listing/message; notify affected parties per policy |
| Suspend account | Progressive enforcement step — modal confirmation; duration selector |
| Escalate | Assign to senior / legal; status `escalated` |
| Link to dispute | Create or link [Dispute Detail](dispute-detail.md) |

Enforcement actions sync to trust ladder — education → warning → restriction → suspension → removal.

---

## Animations

| Element | Motion |
|---------|--------|
| Severity badge | No animation — static |
| Detail panel | Slide in 300ms |
| Submit success | Row removal fade 200ms |
| Escalate | Status badge transition |

---

## Responsive Behaviour

Desktop-primary like verification queue. Mobile: read-only triage possible; enforcement actions desktop-recommended.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Queue table | Skeleton |
| Content preview | Spinner — never show wrong content flash |
| Submit decision | Disable form + button spinner |

Sensitive content: blur preview until operator clicks "Show content" — log view event.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Missing rationale | "Enter a rationale for this action." | Complete field |
| Content already removed | "This content was already actioned by [operator]." | Refresh |
| Concurrent resolution | "Case updated by another moderator." | Reload |
| Suspend without confirmation | Modal blocks until confirmed | Confirm |

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| Queue empty | "No open moderation items." |
| Filters no match | Clear filters prompt |
| No selection | "Select an item to review." |

---

## Permissions

| Role | Access |
|------|--------|
| **Moderator** | Dismiss, warn, remove content |
| **Senior Trust & Safety** | Account suspension, permanent removal |
| **Legal** | Escalated items read + annotate |
| **Creator Success** | No access by default |

Permanent removal requires senior role + dual approval — `TODO(decision):` two-person rule.

---

## Analytics

| Event | Properties |
|-------|------------|
| `admin.moderation.queue_view` | `filters` |
| `admin.moderation.item_open` | `type`, `severity`, `ai_score` |
| `admin.moderation.decision` | `action`, `type`, `time_to_resolve_hours` |
| `admin.moderation.escalate` | `type` |
| `admin.moderation.content_view` | `item_id` — sensitive audit |

Appeal rate tracked separately — future appeals queue.

---

## Accessibility

- Sensitive content warning before display
- Blurred content not read aloud until revealed
- Action radio group fully labeled
- Policy references are links with descriptive text
- High severity not indicated by red alone — icon + label

Moderator wellbeing: limit auto-play media; static previews default.

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Moderation queue — Marketplate Admin |
| `meta robots` | `noindex, nofollow` |

---

## Future Improvements

- Appeals queue linked to moderation decisions
- Bulk dismiss for obvious spam clusters (with audit batch ID)
- Creator response workflow for removed reviews
- Image ML overlays highlighting policy regions
- Moderator assignment by specialization (food safety vs. harassment)
- SLA auto-escalation for high-severity unactioned items

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/admin/moderation/queue` | GET | Paginated moderation items |
| `/api/v1/admin/moderation/items/:id` | GET | Full context + history |
| `/api/v1/admin/moderation/items/:id/decide` | POST | `{ action, rationale, duration? }` |
| `/api/v1/admin/moderation/items/:id/escalate` | POST | Escalate to senior/legal |
| `/api/v1/admin/moderation/policies` | GET | Policy snippets for UI reference |

Actions emit audit events and customer/creator notifications per policy templates.

---

## Related Pages

- [Admin Dashboard](admin-dashboard.md)
- [Verification Queue](verification-queue.md)
- [Dispute Detail](dispute-detail.md)
- [Creator Admin Detail](creator-admin-detail.md)
- [Platform Settings](platform-settings.md)
