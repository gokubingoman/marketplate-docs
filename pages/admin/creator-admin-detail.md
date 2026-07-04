# Creator Admin Detail

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Admin (Internal)  
**Route:** `/admin/creators/:id`

---

## Purpose

Creator Admin Detail is the internal single view of a creator account — verification history, compliance status, trust metrics, enforcement actions, orders summary, and operator tools. It is the system of record for human decisions affecting a creator's ability to sell on Marketplate.

Operators use this page to understand full context before approval in [Verification Queue](verification-queue.md), coaching from Creator Success, or enforcement after [Moderation Queue](moderation-queue.md) / [Dispute Detail](dispute-detail.md) findings.

---

## Goals

**User goals (operators):**
- See complete creator lifecycle in one place without switching tools
- Review verification and compliance history with audit trail
- Take authorized actions (suspend, reinstate, reset verification, add internal notes)
- Link to open queues and disputes involving this creator

**Business goals:**
- Single audit trail visibility for all trust-impacting creator actions
- Reduce duplicate investigations across teams
- Enable pattern detection (repeat disputes, compliance lapses)
- Support creator activation and retention with data-informed outreach

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [Platform Operations (Internal)](../../product/personas.md#platform-operations-internal) | Trust & Safety, Creator Success |
| **Secondary:** Leadership | Read-only executive view |
| **Anti-persona:** Creators | Customer-facing profile is separate; this page contains internal notes and PII |

---

## Navigation

**Arrival paths:**
- [Verification Queue](verification-queue.md) → creator name link
- [Moderation Queue](moderation-queue.md) → subject creator
- [Dispute Detail](dispute-detail.md) → creator link
- [Admin Dashboard](admin-dashboard.md) → creator activation list
- Search: `/admin/creators/search?q=`

**Exit paths:**
- Open verification item → [Verification Queue](verification-queue.md)?creator=:id
- Open dispute → [Dispute Detail](dispute-detail.md)
- Moderation history → [Moderation Queue](moderation-queue.md)?creator=:id
- Impersonate/view storefront (logged) — `TODO(decision):` support impersonation policy
- [Platform Settings](platform-settings.md) unrelated — sidebar nav

---

## Layout

Profile header + tabbed sections.

```
┌──────────┬──────────────────────────────────────────────────────────────┐
│ Admin    │  Maria's Kitchen · Creator #4821          [Actions ▼]        │
│ nav      │  maria@example.com · Joined Jun 12, 2026 · Los Angeles, CA   │
│          │  Badges: Identity ✓  Kitchen ✓  Compliance ⚠ Expiring          │
│          │  Account: Active · GMV 30d: $4,280 · Dispute rate: 0.4%      │
│          ├──────────────────────────────────────────────────────────────┤
│          │  [Overview] [Verification] [Compliance] [Orders] [Trust]     │
│          │            [Disputes] [Notes & audit]                        │
│          ├──────────────────────────────────────────────────────────────┤
│          │  Verification history                                         │
│          │  ┌────────────────────────────────────────────────────────┐  │
│          │  │ Jul 1 · Identity · Approved · Jane · "ID verified"     │  │
│          │  │ Jun 28 · Identity · Submitted                          │  │
│          │  │ Jun 25 · Kitchen · Approved · Mike · "Commercial link" │  │
│          │  └────────────────────────────────────────────────────────┘  │
│          │  [Open in verification queue →]                             │
│          │                                                              │
│          │  Internal notes (not visible to creator)                     │
│          │  [ Add note ]                                                │
│          │  Jun 30 · Creator Success · "Called re: cottage food cap"    │
└──────────┴──────────────────────────────────────────────────────────────┘
```

**Actions dropdown:** Suspend account, Reinstate, Request re-verification, Send platform message — role-gated.

---

## Components

| Component | Usage |
|-----------|-------|
| **Avatar** | Creator photo |
| **Verification badge** | Identity, kitchen, compliance status |
| **Status badge** | Account state: active, restricted, suspended |
| **Tab bar** | Section navigation |
| **Data table** | Orders summary, dispute list, audit log |
| **Cards** | KPI stats, verification timeline |
| **Dashboard stat card** | GMV, order count, review score |
| **Textarea** | Internal notes |
| **Primary / destructive buttons** | Actions with confirmation modals |
| **Modal** | Suspend, reinstate confirmations |
| **Search within page** | Audit log filter |
| **Pagination** | Orders, audit entries |
| **Breadcrumbs** | Admin → Creators → Maria's Kitchen |

---

## Interactions

| Action | Behavior |
|--------|----------|
| Tab switch | Load section async; URL hash update `#verification` |
| Verification timeline item | Expand to show documents (signed URLs), AI flags, operator rationale |
| Add internal note | Append-only; author + timestamp; never shown to creator |
| Suspend account | Modal: reason, duration, notify creator; enforcement ladder step |
| Reinstate | Requires senior role if fraud suspected; audit entry |
| Request re-verification | Sets creator status; opens new queue items |
| Open in queue | Deep link filtered verification queue |
| Export audit | CSV for legal — logged export event |

All actions write to immutable audit trail with `{ actor, action, rationale, timestamp, before, after }`.

---

## Animations

| Element | Motion |
|---------|--------|
| Tab switch | Content crossfade 200ms |
| Timeline expand | Accordion 300ms |
| Action success toast | 3s toast — internal only |
| Badge update on action | Subtle color transition |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Desktop** | Full tabs + tables |
| **Tablet** | Tabs scroll horizontal |
| **Mobile** | Supported for lookup; complex actions desktop-preferred |

PII-heavy — discourage mobile screenshot policies via training, not UI block.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Profile header | Skeleton |
| Tab content | Section skeleton on first load; cache on revisit |
| Document preview in timeline | Inline spinner |
| Action submit | Button loading + disable actions dropdown |

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Creator not found | "No creator with this ID." | Back to search |
| Action permission denied | "You don't have permission to suspend accounts." | — |
| Suspend missing reason | "Enter a reason for suspension." | Modal field |
| Document expired URL | "Document link expired. Refresh." | Refresh |
| Concurrent account change | "Account was updated by another operator. Reload." | Reload |

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| No disputes | "No disputes on record." |
| No moderation history | "No moderation actions." |
| No internal notes | "No internal notes yet." |
| Unverified creator | Verification tab shows pending steps with links to creator-facing status |
| No orders yet | "No orders — creator not yet activated." |

---

## Permissions

| Role | Access |
|------|--------|
| **Trust & Safety** | Full read; suspend, reinstate, re-verification |
| **Creator Success** | Read; internal notes; no suspend |
| **Verification reviewer** | Read verification tab; queue links |
| **Read-only leadership** | Read all tabs except document download — `TODO(decision):` |
| **PII access** | All roles logged; export restricted |

Document downloads audit-logged per view.

---

## Analytics

| Event | Properties |
|-------|------------|
| `admin.creator.view` | `creator_id`, `tab` |
| `admin.creator.action` | `action_type` |
| `admin.creator.note_add` | — |
| `admin.creator.document_view` | `document_type` |
| `admin.creator.audit_export` | — |

Not customer-facing analytics.

---

## Accessibility

- Tab panel: `aria-selected`, keyboard arrow navigation
- Timeline: semantic ordered list with datetime
- Actions dropdown: keyboard accessible; destructive items require confirmation
- Tables: sortable headers announced
- PII fields: mark sensitive sections for screen reader context

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | {Creator name} — Marketplate Admin |
| `meta robots` | `noindex, nofollow` |

Contains PII — strict access controls.

---

## Future Improvements

- Risk score dashboard per creator (dispute rate, compliance, review authenticity)
- Side-by-side comparison with platform averages
- Creator Success playbook tasks integrated (checklist CRM)
- Team member list and permissions for multi-person operations
- Automated flags: "3 disputes in 30 days"
- Integration with payout holds

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/admin/creators/:id` | GET | Profile summary + KPIs |
| `/api/v1/admin/creators/:id/verification` | GET | Verification history |
| `/api/v1/admin/creators/:id/compliance` | GET | Compliance items |
| `/api/v1/admin/creators/:id/orders` | GET | Paginated order summary |
| `/api/v1/admin/creators/:id/disputes` | GET | Dispute list |
| `/api/v1/admin/creators/:id/trust` | GET | Moderation + metrics |
| `/api/v1/admin/creators/:id/notes` | POST | Internal note |
| `/api/v1/admin/creators/:id/actions/suspend` | POST | Suspend with rationale |
| `/api/v1/admin/creators/:id/actions/reinstate` | POST | Reinstate |
| `/api/v1/admin/creators/:id/actions/request-reverification` | POST | Trigger re-verification |
| `/api/v1/admin/creators/:id/audit` | GET | Full audit log |

Syncs with creator-facing pages: status changes push notifications to [Identity Verification](../auth/identity-verification.md), [Kitchen Verification](../auth/kitchen-verification.md), [Compliance Center](../auth/compliance-center.md).

---

## Related Pages

- [Admin Dashboard](admin-dashboard.md)
- [Verification Queue](verification-queue.md)
- [Moderation Queue](moderation-queue.md)
- [Dispute Detail](dispute-detail.md)
- [Platform Settings](platform-settings.md)
- [Creator Signup](../auth/creator-signup.md)
- [Identity Verification](../auth/identity-verification.md)
- [Kitchen Verification](../auth/kitchen-verification.md)
- [Compliance Center](../auth/compliance-center.md)
