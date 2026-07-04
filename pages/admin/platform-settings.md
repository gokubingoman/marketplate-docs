# Platform Settings

> Template: Page Specification — see [Founding Constitution](../../company/constitution.md)

**Status:** Draft  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** Product  
**Surface:** Admin (Internal)  
**Route:** `/admin/settings`

---

## Purpose

Platform Settings is the internal configuration console for Marketplate operators and authorized engineering — not customer-facing. It centralizes trust SLAs, verification rules, compliance grace periods, moderation thresholds, feature flags, and jurisdiction templates that govern creator onboarding, admin queues, and enforcement automation.

Changes here affect marketplace behavior platform-wide. Every save requires audit logging and appropriate role authorization per [Audit everything](../../product/marketplace-mechanics.md#marketplace-model-overview) and [Design for the Long Term](../../company/values.md#8-design-for-the-long-term).

---

## Goals

**User goals (operators/engineering):**
- Configure trust and ops parameters without code deploys where safe
- Understand current production values and last change history
- Preview impact before enabling jurisdiction or enforcement changes
- Roll back errant configuration quickly

**Business goals:**
- Operational agility for Trust & Safety SLAs and compliance policies
- Reduce engineering bottleneck for non-code policy tuning
- Maintain change audit trail for regulatory and incident review
- Separate customer-facing settings (creator dashboard) from platform internals

---

## Target User

| Role | Priority |
|------|----------|
| **Primary:** [Platform Operations (Internal)](../../product/personas.md#platform-operations-internal) — Ops lead | SLA and compliance configuration |
| **Secondary:** Engineering / platform admin | Feature flags, integration keys (masked) |
| **Secondary:** Trust & Safety leadership | Moderation thresholds, enforcement defaults |
| **Anti-persona:** Creators and customers | No access — settings affect them but are not self-serve |

---

## Navigation

**Arrival paths:**
- Admin sidebar → "Settings"
- [Admin Dashboard](admin-dashboard.md) gear icon
- Engineering runbook links

**Exit paths:**
- Section links within settings (tabbed IA)
- Back to [Admin Dashboard](admin-dashboard.md)
- Change history → audit detail modal

**Not linked from** any customer or creator surface.

---

## Layout

Settings shell with left sub-nav categories + main form area.

```
┌──────────┬──────────────────────────────────────────────────────────────┐
│ Admin    │  Platform settings                                           │
│ nav      ├─────────────┬────────────────────────────────────────────────┤
│          │ Categories  │  Trust & verification SLAs                   │
│          │             │                                              │
│          │ Trust & SLAs│  Identity review target:  [ 48 ] hours       │
│          │ Compliance  │  Kitchen review target:    [ 48 ] hours       │
│          │ Moderation  │  Compliance review target: [ 72 ] hours       │
│          │ Disputes    │                                              │
│          │ Jurisdictions│ Warning threshold (% of SLA): [ 80 ]%       │
│          │ Feature flags│                                              │
│          │ Integrations│  Compliance grace period:   [ 14 ] days       │
│          │             │  (listings suspended after expiry + grace)    │
│          │             │                                              │
│          │             │  Password reset token TTL: [ 60 ] minutes     │
│          │             │                                              │
│          │             │  Last changed: Jul 1 by Jane · View history   │
│          │             │                                              │
│          │             │  [ Save changes ]  [ Discard ]                │
└──────────┴─────────────┴────────────────────────────────────────────────┘
```

Dangerous settings (enforcement automation, global suspend) use confirmation modals + senior role.

---

## Components

| Component | Usage |
|-----------|-------|
| **Sidebar nav** | Settings categories |
| **Text input** | Numeric SLA hours, grace days, token TTL |
| **Select** | Jurisdiction template, default kitchen types |
| **Checkbox** | Feature flags on/off |
| **Toggle** | Enable/disable automation rules |
| **Primary button** | "Save changes" — one primary per section |
| **Secondary button** | "Discard", "View history" |
| **Modal** | Confirm high-impact changes; show diff |
| **Cards** | Setting groups with descriptions |
| **Data table** | Jurisdiction list, feature flag inventory |
| **Status badge** | Flag: enabled/disabled; env: prod/staging |
| **Toast** | Save success/failure |
| **Breadcrumbs** | Admin → Settings → {category} |

---

## Settings categories (v1)

### Trust & verification SLAs
- Identity, kitchen, compliance review target hours
- SLA warning threshold (% of target before dashboard warning)
- Drives [Admin Dashboard](admin-dashboard.md) and [Verification Queue](verification-queue.md) badges

### Compliance
- Document expiration grace period before auto-suspend
- Reminder schedule (30/14/7 days) for [Compliance Center](../auth/compliance-center.md)
- Cottage food sales cap enforcement toggle per jurisdiction — `TODO(decision):`

### Moderation
- AI classifier confidence threshold for auto-queue (never auto-action)
- High-severity escalation timeout
- Drives [Moderation Queue](moderation-queue.md)

### Disputes
- Resolution SLA hours
- Refund limits by role for [Dispute Detail](dispute-detail.md)
- Auto-escalation rules

### Jurisdictions
- Launch market templates linking to compliance rule sets
- `TODO(decision):` geographic launch market — initial template library
- Affects [Kitchen Verification](../auth/kitchen-verification.md) and [Compliance Center](../auth/compliance-center.md)

### Feature flags
- Gradual rollout toggles (not customer-visible marketing flags)
- Environment scoping: staging vs. production

### Integrations
- Masked API keys reference (actual secrets in vault — not stored in UI)
- Webhook endpoints for ops notifications

---

## Interactions

| Action | Behavior |
|--------|----------|
| Edit field | Mark section dirty; enable Save |
| Save changes | Validate ranges; show diff modal if high-impact; POST; audit log |
| Discard | Revert to last saved |
| View history | Modal with paginated change log: who, when, before/after |
| Rollback | Restore previous version from history — senior role |
| Jurisdiction add | Wizard to clone template — future |
| Feature flag toggle | Immediate effect in prod requires confirmation + optional canary — `TODO(decision):` |

**Human gates:** Settings cannot disable human verification approval or auto-approve creators — hardcoded invariant, not configurable.

---

## Animations

| Element | Motion |
|---------|--------|
| Section switch | Content fade 200ms |
| Dirty indicator | Dot on category nav — no blink |
| Save success | Toast slide in |
| Diff modal | Standard modal animation |

Minimal motion — ops efficiency focus.

---

## Responsive Behaviour

Desktop-primary (1280px+). Tablet usable. Mobile not optimized — show banner "Use desktop for settings changes."

---

## Loading States

| State | Treatment |
|-------|-----------|
| Category load | Skeleton form fields |
| Save | Disable section + button spinner |
| History modal | Table skeleton |
| Jurisdiction list | Table loading rows |

Show last saved values immediately from cache; refresh in background.

---

## Error States

| Error | Message | Recovery |
|-------|---------|----------|
| Validation out of range | "SLA must be between 1 and 168 hours." | Fix input |
| Unauthorized save | "You don't have permission to change dispute settings." | — |
| Concurrent edit | "Settings were updated by [user] at [time]. Reload to see current values." | Reload |
| Save failed | "Changes couldn't save. Try again." | Retry |
| Rollback failed | "Rollback failed. Contact engineering." | Support |

---

## Empty States

| Scenario | Treatment |
|----------|-----------|
| No jurisdictions configured | "No jurisdiction templates. Add launch market template." + CTA |
| No feature flags | "No feature flags defined." — unlikely |
| Empty change history | "No changes recorded yet." |

---

## Permissions

| Role | Access |
|------|--------|
| **Platform admin** | Full settings read/write |
| **Trust & Safety lead** | Trust, moderation, dispute SLAs only |
| **Ops lead** | Compliance grace, verification SLAs |
| **Engineering** | Feature flags, integrations |
| **Reviewer** | Read-only all |

Production changes require MFA re-auth — `TODO(decision):`. Staging may be more permissive.

---

## Analytics

| Event | Properties |
|-------|------------|
| `admin.settings.view` | `category` |
| `admin.settings.save` | `category`, `fields_changed[]` |
| `admin.settings.rollback` | `category`, `version` |
| `admin.settings.flag_toggle` | `flag_name`, `enabled` |

All saves in immutable audit store — separate from product analytics.

---

## Accessibility

- Form labels and helper text for every setting — explain impact in plain language
- Diff modal readable by screen readers — before/after values announced
- Toggle switches have visible text state
- Error summary at section top on save failure
- Keyboard navigable category list

---

## SEO

| Element | Value |
|---------|-------|
| `<title>` | Platform settings — Marketplate Admin |
| `meta robots` | `noindex, nofollow` |
| Access | Internal network / SSO only |

---

## Future Improvements

- Staged rollout: apply jurisdiction changes to canary creators first
- Simulation mode: preview how many creators affected by grace period change
- ADR linkage: require ADR URL for high-impact changes
- Config export/import for disaster recovery
- Approval workflow: second operator approves prod changes
- Integration health checks inline

---

## API Requirements

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/admin/settings/:category` | GET | Current settings for category |
| `/api/v1/admin/settings/:category` | PATCH | Save with `{ changes, rationale? }` |
| `/api/v1/admin/settings/:category/history` | GET | Change audit log |
| `/api/v1/admin/settings/:category/rollback` | POST | Rollback to version |
| `/api/v1/admin/settings/jurisdictions` | GET/POST | Jurisdiction templates |
| `/api/v1/admin/settings/feature-flags` | GET/PATCH | Flag management |

**Audit schema:** `{ id, category, actor_id, timestamp, before_json, after_json, rationale }`

Secrets never returned in GET — reference IDs only.

Hardcoded invariants (API enforced):
- `verification.human_approval_required: true` (read-only display)
- `reviews.pay_to_remove: false` (read-only display)

---

## Related Pages

- [Admin Dashboard](admin-dashboard.md)
- [Verification Queue](verification-queue.md)
- [Moderation Queue](moderation-queue.md)
- [Dispute Detail](dispute-detail.md)
- [Creator Admin Detail](creator-admin-detail.md)
- [Identity Verification](../auth/identity-verification.md)
- [Kitchen Verification](../auth/kitchen-verification.md)
- [Compliance Center](../auth/compliance-center.md)
- [Password Reset](../auth/password-reset.md) — token TTL setting
