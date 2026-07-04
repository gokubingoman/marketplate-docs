# Creator Messages (Customer Communication)

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Surface:** Creator OS  
**Route:** `/creator/messages`  
**Phase:** 2  
**Last updated:** 2026-07-03

---

## Purpose

The Messages page is the creator's **inbox for customer communication** — order-related questions, pickup coordination, allergy clarifications, and post-order follow-up. It replaces scattered DMs and text threads with an auditable, order-linked conversation history tied to the [order lifecycle](../../product/marketplace-mechanics.md#order-lifecycle).

Messages are operational, not marketing. Creators respond in context; customers initiate from order or storefront touchpoints. All threads are logged for dispute resolution in [Dispute Detail](../admin/dispute-detail.md).

---

## Goals

| User goal | Business goal |
|-----------|---------------|
| See unread customer messages at a glance | Reduce response time and missed inquiries |
| Reply in order context without switching apps | Improve customer satisfaction and repeat rate |
| Find past conversations by customer or order | Support dispute evidence and quality coaching |
| Send proactive updates (delay, ready early) | Reduce no-shows and support tickets |

**Primary action on this screen:** Open the oldest unread thread or highest-priority order-linked message.

---

## Target User

| Role | Persona | Notes |
|------|---------|-------|
| **Primary** | [Independent Chef](../../product/personas.md#independent-chef) | High-touch customer relationships |
| **Secondary** | [Baker](../../product/personas.md#baker) | Custom order clarification |
| **Secondary** | [Meal Prep Business](../../product/personas.md#meal-prep-business) | Batch coordination messages |
| **Anti-persona** | Customer support bot | No automated bulk messaging to non-customers in v1 |

---

## Navigation

### Arrival

| Source | Context |
|--------|---------|
| Sidebar nav | "Messages" — badge shows unread count |
| [Dashboard](./dashboard.md) | Unread message indicator |
| [Orders](./orders.md) | "Message customer" from order row |
| [Order Detail](./order-detail.md) | Message thread tab or CTA |
| Push notification | "New message from Sarah about order #1042" |

### Departure

| Destination | Trigger |
|-------------|---------|
| [Order Detail](./order-detail.md) | Order link in thread header |
| [Orders](./orders.md) | Back to queue |
| [Dashboard](./dashboard.md) | Sidebar home |

### Breadcrumbs

`Dashboard → Messages` (list view)  
`Dashboard → Messages → Order #1042` (thread view on mobile)

---

## Layout

Master-detail: thread list + active conversation. Mobile shows list OR thread with back navigation.

```
┌─────────────────────────────────────────────────────────────────┐
│ Dashboard → Messages                              [Search threads]│
├──────────────────────┬──────────────────────────────────────────┤
│ Threads              │  Order #1042 · Sarah M. · Pickup 4:30 PM │
│                      │  [ View order → ]                        │
│ ● Sarah M.     2m    │  ─────────────────────────────────────── │
│   Re: pickup time    │  Sarah · 2:15 PM                         │
│                      │  Can I pick up at 5 instead of 4:30?     │
│ ○ James K.     1h    │                                          │
│   Allergy question   │  You · 2:18 PM                           │
│                      │  Yes, 5 PM works. See you then!          │
│ ○ Platform   yesterday│                                         │
│   Verification note  │  ┌─────────────────────────────────────┐ │
│                      │  │ Type a message...          [ Send ] │ │
│ [ All ] [ Unread ]   │  └─────────────────────────────────────┘ │
│ [ Order-linked only ]│  Quick replies: [ Running late ] [ Ready ]│
└──────────────────────┴──────────────────────────────────────────┘
```

**Content hierarchy:**

1. Filter tabs — All / Unread / Order-linked
2. Thread list — sorted by unread first, then recency
3. Active thread — order context header + message history
4. Compose area — input + quick replies

---

## Components

| Component | Usage on this page | DS reference |
|-----------|-------------------|--------------|
| **Sidebar nav** | Persistent Creator OS navigation | [Navigation — Sidebar](../../design-system/components-overview.md#navigation) |
| **Search input** | Filter threads by customer name or order # | [Inputs — Search](../../design-system/components-overview.md#inputs) |
| **Segmented control** | All / Unread / Order-linked filters | [Segmented control](../../design-system/components-overview.md#segmented-control) |
| **List item** | Thread preview with unread dot | [Lists](../../design-system/components-overview.md#lists) |
| **Avatar** | Customer initials/photo in thread | [Avatars](../../design-system/components-overview.md#avatars) |
| **Message bubble** | Inbound/outbound styling | [Messages](../../design-system/components-overview.md#messages) |
| **Textarea** | Compose input; auto-expand | [Inputs — Textarea](../../design-system/components-overview.md#inputs) |
| **Primary button** | Send message | [Buttons — Primary](../../design-system/components-overview.md#buttons) |
| **Chip / quick reply** | Canned responses | [Chips](../../design-system/components-overview.md#chips) |
| **Status badge** | Order status in thread header | [Badges — Status](../../design-system/components-overview.md#badges) |
| **Ghost link** | View order, mark read | [Buttons — Ghost](../../design-system/components-overview.md#buttons) |

---

## Interactions

| Element | Behavior |
|---------|----------|
| **Thread row tap** | Open conversation; mark as read on view |
| **Send message** | `Enter` sends (Shift+Enter newline); optimistic UI with rollback |
| **Quick reply chip** | Inserts template text; creator can edit before send |
| **View order** | Navigate to [Order Detail](./order-detail.md) |
| **Search** | Debounced filter on customer name, order ID |
| **Unread filter** | Show only threads with unread inbound messages |
| **Platform messages** | Read-only system threads (verification, policy) — no reply |
| **Realtime** | New messages appear via WebSocket; badge updates on nav |
| **Attachment** | v2 — text only in Phase 2 |
| **Keyboard** | `Tab` between list and compose; `/` focuses search |

**Moderation:** Outbound messages scanned for PII exchange patterns and off-platform payment requests — flags to [Moderation Queue](../admin/moderation-queue.md), not blocked silently.

---

## Animations

| Trigger | Motion | Duration |
|---------|--------|----------|
| New message (realtime) | Bubble slide up + thread list reorder | 200ms |
| Send optimistic | Bubble appears immediately at bottom | instant |
| Thread switch | Content crossfade | 150ms |
| Unread dot clear | Fade out | 150ms |

Respect `prefers-reduced-motion`: instant message append.

---

## Responsive Behaviour

| Breakpoint | Layout changes |
|------------|----------------|
| **Mobile (320–767px)** | List view OR thread view; back button returns to list |
| **Tablet (768–1023px)** | Narrow list (35%) + thread panel |
| **Desktop (1024px+)** | Master-detail as wireframe |

Compose area sticky at bottom on mobile — above keyboard.

---

## Loading States

| Region | Treatment |
|--------|-----------|
| **Thread list** | Skeleton rows (5) |
| **Active thread** | Message bubble skeletons |
| **Send** | Send button spinner; input disabled briefly |
| **Load older messages** | Spinner at top of thread on scroll-up |

Pagination: load 50 messages initially; infinite scroll up for history.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Thread list fetch failed | "Messages couldn't load" | Retry |
| Send failed | "Message didn't send" | Retry button on failed bubble |
| Order context unavailable | Thread header shows customer only | Link disabled with tooltip |
| Realtime disconnect | Subtle banner: "Reconnecting..." | Auto-reconnect; manual refresh |
| Blocked content | "This message can't be sent — it may violate marketplace policy" | Edit message |

---

## Empty States

| Scenario | Display | Primary action |
|----------|---------|----------------|
| **No messages ever** | "When customers message you about orders, they'll appear here" | [View orders](./orders.md) |
| **No unread** | Filter shows "All caught up" when Unread tab empty | Switch to All |
| **Search no results** | "No threads match your search" | Clear search |
| **Completed order thread** | Banner: "This order is complete — messages are archived" | Still readable; compose allowed 7 days post-completion |

---

## Permissions

| Role | Access |
|------|--------|
| **Creator owner** | All threads; send/receive |
| **Creator staff — orders** | Order-linked threads only |
| **Creator staff — kitchen** | Read-only on active order threads |
| **Unverified creator** | Platform messages only; no customer threads until verified |
| **Suspended creator** | Read-only historical threads; cannot send |

---

## Analytics

| Event | Properties | Purpose |
|-------|------------|---------|
| `creator_messages_viewed` | `unread_count`, `thread_count` | Inbox engagement |
| `creator_messages_thread_opened` | `order_id`, `unread` | Response funnel |
| `creator_messages_sent` | `order_id`, `used_quick_reply` (bool) | Response patterns |
| `creator_messages_quick_reply_used` | `template_id` | Template effectiveness |
| `creator_messages_search` | `query_length` | Findability |
| `creator_messages_response_time` | `minutes_to_first_reply` | SLA tracking |

Target: median first response < 2 hours during business hours.

---

## Accessibility

| Requirement | Implementation |
|-------------|----------------|
| **Page title** | `<h1>Messages</h1>` |
| **Thread list** | `role="listbox"`; unread announced in label |
| **Message history** | `role="log"` with `aria-live="polite"` for new inbound |
| **Compose** | `aria-label="Message to Sarah about order 1042"` |
| **Quick replies** | Keyboard selectable chips |
| **Timestamps** | `<time datetime="...">` elements |

Screen reader announces new message: "New message from Sarah about order 1042."

---

## SEO

Not applicable — authenticated creator surface. `noindex, nofollow`.

---

## Future Improvements

- Photo attachments (food ready photo)
- Automated status messages on order state change (opt-in)
- Customer message templates library
- SLA indicator for response time
- Integration with SMS for creators who prefer mobile
- Translation support for multilingual customers
- Support ticket escalation to platform (separate from customer threads)

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `GET /api/v1/creator/messages/threads` | GET | Thread list with preview, unread flag |
| `GET /api/v1/creator/messages/threads/{id}` | GET | Messages paginated: `?before=&limit=50` |
| `POST /api/v1/creator/messages/threads/{id}` | POST | Send message `{ body }` |
| `PATCH /api/v1/creator/messages/threads/{id}/read` | PATCH | Mark thread read |
| `GET /api/v1/creator/messages/unread-count` | GET | Badge count for nav |
| `GET /api/v1/creator/messages/quick-replies` | GET | Template list |
| WebSocket `creator.{id}.messages` | Subscribe | Realtime inbound messages |

Messages immutable after send — no edit/delete in v1 (audit requirement).

---

## Related Pages

- [Dashboard](./dashboard.md) — unread badge
- [Orders](./orders.md) — message entry from order row
- [Order Detail](./order-detail.md) — order context in thread
- [Availability](./availability.md) — schedule change notifications to customers
- [Reviews](./reviews.md) — post-order customer relationship
- [Dispute Detail](../admin/dispute-detail.md) — message evidence in disputes
