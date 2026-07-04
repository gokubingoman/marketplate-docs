# Dispute Detail

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Admin (Internal)  
**Route:** `/admin/disputes/:id`

---

## Purpose

Dispute Detail is the case management view for order dispute investigation and resolution. When creator and customer cannot resolve an issue through messaging, Trust & Safety mediates with full order context, policies, communication history, and financial impact — producing a logged outcome.

Per [Disputes](../../product/marketplace-mechanics.md#disputes): platform mediation when unresolved; outcomes include refund, partial refund, credit, or no action — all logged with SLA targets.

---

## Goals

**User goals (operators):**
- Understand dispute facts quickly from order, messages, and photos
- Apply platform policy consistently with visible precedent links
- Record resolution with rationale visible in audit trail
- Communicate outcome to both parties with calm, precise copy

**Business goals:**
- Fair resolution protecting customers and non-abusive creators
- Reduce repeat disputes via pattern detection on [Creator Admin Detail](creator-admin-detail.md)
- Meet dispute resolution SLA
- Maintain complete immutable case record for legal/compliance review

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [Platform Operations (Internal)](../../product/personas.md#platform-operations-internal) — Trust & Safety | Dispute investigators |
| **Secondary:** Creator Success | View-only for coaching — `TODO(decision):` |
| **Anti-persona:** Either party unilaterally editing case | Parties interact via messaging; resolution is operator action |

---

## Navigation

**Arrival paths:**
- [Admin Dashboard](admin-dashboard.md) urgent dispute alert
- Disputes list (future `/admin/disputes`) filtered views
- [Moderation Queue](moderation-queue.md) escalation
- [Creator Admin Detail](creator-admin-detail.md) → disputes tab
- Order support escalation from customer/creator support tools

**Exit paths:**
- Creator name → [Creator Admin Detail](creator-admin-detail.md)
- Related moderation → [Moderation Queue](moderation-queue.md)
- Case closed → disputes list or dashboard
- Order detail external tool — `TODO(decision):` deep link to order admin view

---

## Layout

Case header + three-column content on desktop; stacked on mobile.

```
┌──────────┬──────────────────────────────────────────────────────────────┐
│ Admin    │  Dispute #D-10482                    Status: Open · Urgent    │
│ nav      │  Order #92847 · $47.50 · Jul 1, 2026                          │
│          ├──────────────────────────────────────────────────────────────┤
│          │  Summary                                                      │
│          │  Customer claims: wrong items / allergen concern              │
│          │  Creator response: prepared per order ticket                  │
│          ├───────────────┬────────────────────┬───────────────────────────┤
│          │ Order details │ Message thread     │ Resolution panel          │
│          │ Line items    │ [chronological]    │ Policy: Refund §3.2       │
│          │ Fulfillment   │ Customer · Creator │ Outcome:                  │
│          │ Payment       │ System             │ ○ Full refund               │
│          │ Photos        │                    │ ○ Partial refund $[__]     │
│          │               │                    │ ○ Credit                    │
│          │               │                    │ ○ No action                 │
│          │               │                    │ Rationale (required)        │
│          │               │                    │ Notify parties □            │
│          │               │                    │ [ Resolve dispute ]         │
│          ├───────────────┴────────────────────┴───────────────────────────┤
│          │  Audit trail                                                  │
│          │  Jul 2 10:04 · Jane opened case                               │
│          │  Jul 2 10:15 · Jane requested photos from customer            │
│          │  Jul 2 14:30 · Customer uploaded photo                        │
└──────────┴──────────────────────────────────────────────────────────────┘
```

---

## Components

| Component | Usage |
|-----------|-------|
| **Status badge** | Open, pending info, resolved, appealed |
| **Cards** | Order summary, line items, fulfillment timeline |
| **Review card** | Customer claim summary |
| **Data display** | Payment breakdown |
| **Radio** | Resolution outcome |
| **Text input** | Partial refund amount |
| **Textarea** | Rationale, internal notes, party messages |
| **Primary button** | "Resolve dispute" |
| **Secondary button** | "Request information", "Escalate" |
| **Checkbox** | Notify customer/creator on resolution |
| **Modal** | Confirm financial resolution |
| **Pagination** | Message thread load more |
| **Avatar** | Customer and creator in thread |

Chat/messaging composite component — Phase 2 design system.

---

## Interactions

| Action | Behavior |
|--------|----------|
| Request information | Send templated message to customer and/or creator; status → `pending_info` |
| Upload review (operator) | Internal attachment to case |
| Select outcome | Enable resolve; partial refund shows amount field with validation ≤ order total |
| Resolve dispute | Confirm modal with financial summary; execute refund/credit via payments API; close case |
| Escalate | Assign senior reviewer; flag urgent |
| Reopen | Senior role only — new audit entry |
| Message thread scroll | Load historical messages read-only; operator can send official platform message |

**Financial actions:** Double confirmation for refunds; audit includes payment transaction IDs.

---

## Animations

| Element | Motion |
|---------|--------|
| Status change | Badge transition 300ms |
| New message in thread | Highlight 2s fade — if live refresh |
| Resolve success | Redirect or banner — no celebration |
| Panel expand | Accordion for order details on mobile |

---

## Responsive Behaviour

| Breakpoint | Layout |
|------------|--------|
| **Desktop** | Three-column case view |
| **Tablet** | Tabs: Order | Messages | Resolution |
| **Mobile** | Single column accordion sections |

Resolution panel always reachable — financial decisions not hidden on mobile.

---

## Loading States

| State | Treatment |
|-------|-----------|
| Case load | Skeleton header + panels |
| Messages | Thread skeleton |
| Payment data | Shimmer on totals until loaded |
| Resolve in progress | Full-panel loading overlay on resolution section |

Never show resolve button until order payment data loaded.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Partial refund > order total | "Refund cannot exceed order total of $47.50." | Fix amount |
| Missing rationale | "Enter a rationale for this resolution." | Complete field |
| Payment refund failed | "Refund failed: [processor message]. Case remains open." | Retry or manual ops |
| Case already resolved | "This dispute was resolved on [date] by [operator]." | View audit |
| Unauthorized | Access denied page | — |

Customer/creator notification failures logged — operator sees warning but case can close.

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| No customer photos | "No photos attached. Request information to collect evidence." |
| No creator response yet | Thread shows customer claim only; prompt to request creator statement |
| Empty internal notes | Notes section collapsed with "Add internal note" |

---

## Permissions

| Role | Access |
|------|--------|
| **Dispute investigator** | Full case access; resolve up to $X — `TODO(decision):` refund limits |
| **Senior Trust & Safety** | Unlimited refund; reopen cases |
| **Creator Success** | Read-only |
| **Finance** | Read + payment reconciliation export — future |

Refund limits enforced server-side.

---

## Analytics

| Event | Properties |
|-------|------------|
| `admin.dispute.view` | `dispute_id`, `status`, `urgent` |
| `admin.dispute.request_info` | — |
| `admin.dispute.resolve` | `outcome`, `amount`, `time_to_resolve_hours` |
| `admin.dispute.escalate` | — |
| `admin.dispute.reopen` | `original_outcome` |

Platform metric: dispute rate, resolution time — [Trust Metrics](../../product/success-metrics-overview.md#trust-metrics).

---

## Accessibility

- Case status in page title: "Dispute D-10482 — Open — Marketplate Admin"
- Message thread: accessible list with sender and timestamp announced
- Financial inputs: clear labels; errors associated with fields
- Audit trail: chronological list readable by screen readers
- Resolution radios: full outcome text, not codes alone

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Dispute {id} — Marketplate Admin |
| `meta robots` | `noindex, nofollow` |

---

## Future Improvements

- Disputes list page with bulk assign
- Policy precedent search from past cases
- Customer/creator satisfaction survey post-resolution
- Integration with payment processor dispute/chargeback flow
- Allergen-specific investigation checklist template
- SLA timer visible in header with auto-escalation

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/admin/disputes/:id` | GET | Full case + order + parties |
| `/api/v1/admin/disputes/:id/messages` | GET | Message thread |
| `/api/v1/admin/disputes/:id/messages` | POST | Operator platform message |
| `/api/v1/admin/disputes/:id/request-info` | POST | Request info workflow |
| `/api/v1/admin/disputes/:id/resolve` | POST | `{ outcome, amount?, rationale, notify }` |
| `/api/v1/admin/disputes/:id/escalate` | POST | Escalate case |
| `/api/v1/admin/disputes/:id/audit` | GET | Audit trail |

Payment: `/api/v1/admin/payments/refund` invoked by resolve — idempotent with case ID.

---

## Related Pages

- [Admin Dashboard](admin-dashboard.md)
- [Moderation Queue](moderation-queue.md)
- [Creator Admin Detail](creator-admin-detail.md)
- [Verification Queue](verification-queue.md) — fraud-related disputes
- [Platform Settings](platform-settings.md) — dispute SLA, refund limits
