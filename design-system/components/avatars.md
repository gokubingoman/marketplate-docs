# Avatars

> Visual representation of people — creators and customers — with photo or initials fallback.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Avatars represent people across the platform. Creator avatars reinforce [trust in design](../principles.md#trust-in-design) — visible identity alongside verification badges on storefronts and discovery surfaces.

### Variants

| Variant | Usage | Shape |
|---------|-------|-------|
| **Creator avatar** | Storefront header, reviews, discovery cards | Circle |
| **Customer avatar** | Review attribution, account settings | Circle |
| **Avatar group** | Multiple creators (catering contexts) | Overlapping circles |

**Appears on:** Storefronts, profiles, reviews, navigation account menu.

→ Inventory context: [components-overview.md](../components-overview.md#avatars)

---

## Anatomy

```
┌──────────┐
│          │
│  Photo   │  ← Image OR initials fallback
│  or AB   │
│          │
└──────────┘
  Status dot (optional, future)
```

| Part | Required | Description |
|------|----------|-------------|
| **Container** | Yes | Fixed square clipped to circle |
| **Image** | Preferred | Creator/customer photo |
| **Initials fallback** | Yes | 1–2 characters when image missing or loading |
| **Status indicator** | No | Online/offline — deferred; not in v1 implementation |
| **Border** | No | Optional 2px `surface-default` border on avatar groups |

---

## Sizes

| Size | Dimensions | Typography (initials) | Usage |
|------|------------|------------------------|-------|
| **xs** | 24px | `text-ui-xs` | Inline mentions, compact lists |
| **sm** | 32px | `text-ui-sm` | Review attribution, comments |
| **md** | 40px | `text-ui-md` | Navigation account menu, cards |
| **lg** | 48px | `text-ui-lg` | Creator cards, review headers |
| **xl** | 64px | `text-display-sm` | Storefront header, profile page |
| **2xl** | 96px | `text-display-md` | Profile edit, verification upload preview |

**Border radius:** `radius-full` (9999px) — always circular.

**Avatar group overlap:** Each subsequent avatar offset `-space-2` (8px) left; max 4 visible + "+N" overflow badge.

---

## Initials Fallback Logic

| Input | Initials displayed |
|-------|-------------------|
| Full name "Maria Lopez" | `ML` |
| Single name "Maria" | `MA` (first two characters) |
| Business name "Joe's Kitchen" | `JK` (significant words, skip articles) |
| Email only (no name) | First letter of local part, uppercase |
| No name available | Generic person icon (not initials) |

Initials background: `color-trust-subtle`. Initials text: `color-trust-default`, weight 600.

Generic fallback icon: neutral silhouette on `color-neutral-100` — `aria-label` required, no initials.

---

## States

| State | Visual | Notes |
|-------|--------|-------|
| **Default** | Photo or initials displayed | — |
| **Hover** | Optional subtle ring on clickable avatar | Creator profile link only |
| **Focus** | `border-focus` 2px outline, 2px offset | When avatar is link/button |
| **Active** | Same as hover | — |
| **Loading** | Neutral skeleton circle, pulse optional | `aria-busy="true"` |
| **Error** | Initials fallback if image fails to load | `onerror` → fallback |
| **Disabled** | Opacity 0.5 | Account menu when logged out — show generic icon |

No error state styling on the avatar itself — failed images silently fall back to initials.

---

## Component Tokens

| Token | Maps to | Context |
|-------|---------|---------|
| `avatar-background` | `color-trust-subtle` | Initials fallback fill |
| `avatar-text` | `color-trust-default` | Initials text |
| `avatar-border` | `surface-default` | Group overlap border |
| `avatar-fallback-background` | `color-neutral-100` | Generic icon fallback |
| `avatar-ring-hover` | `color-trust-muted` | Hover ring on interactive |

→ Semantic source: [color foundations](../foundations/color.md)

---

## Token Usage Summary

| Property | Token |
|----------|-------|
| Initials typography | Size-matched UI/display token, weight 600 |
| Group border | 2px `surface-default` |
| Group overlap | `-space-2` margin |
| Focus ring | `border-focus`, 2px, 2px offset |
| Overflow badge | `text-ui-sm`, `color-neutral-100` background |

→ Typography: [typography foundations](../foundations/typography.md)  
→ Spacing: [spacing foundations](../foundations/spacing.md)

---

## Accessibility

Target: **WCAG 2.2 AA** → [accessibility standards](../accessibility-standards.md)

| Requirement | Implementation |
|-------------|----------------|
| **Alt text (image)** | `"[Person name], [role if relevant]"` — e.g., "Maria Lopez, creator" |
| **Decorative in context** | When name appears adjacent in same link, image uses `alt=""` and `aria-hidden="true"` |
| **Initials fallback** | Container has `role="img"` + `aria-label="Maria Lopez"` |
| **Interactive avatar** | Wrap in `<a>` or `<button>` with accessible name; 44×44px min touch target for md+ in nav |
| **Avatar group** | `aria-label="4 creators"` on group container; individual avatars hidden from SR if redundant |
| **Loading** | `aria-busy="true"` on container until image loads |

Creator photos are meaningful — always provide descriptive alt unless redundant with adjacent visible name in the same focus target.

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| **Mobile (320–767px)** | Storefront header: `xl` (64px). Nav account menu: `md` (40px). Review cards: `sm` (32px). |
| **Tablet (768–1023px)** | Storefront header: `2xl` (96px) when hero layout. Cards: `lg` (48px). |
| **Desktop (1024px+)** | Profile pages: `2xl`. Discovery cards: `lg`. Dashboard: `md` for table rows. |

**Avatar group on mobile:** Max 3 visible + overflow; reduce overlap to `-space-1` if cramped.

**Touch targets:** Nav and profile avatars expand hit area to 44px even when visual size is `md` (40px).

---

## Do / Don't

### Do

- Use **real creator photos** — reinforces authenticity
- Show **initials fallback** immediately while image loads
- Pair creator avatar with **name and verification** on storefronts
- Use **consistent sizes** within a context (all review avatars = sm)
- Expand **touch target** for interactive avatars in navigation

### Don't

- Use generic stock silhouettes when a name is available
- Show avatars without associated name in discovery (except avatar group overflow)
- Rely on avatar alone for identity — always show name nearby
- Use square avatars — always circular
- Add online status indicators without product requirement
- Crop faces poorly — use `object-fit: cover` centered on face

---

## Related Documents

- [Design Principles](../principles.md)
- [Components Overview](../components-overview.md#avatars)
- [Color Foundations](../foundations/color.md)
- [Typography Foundations](../foundations/typography.md)
- [Spacing Foundations](../foundations/spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Badges](badges.md) — verification alongside avatar
- [Cards](cards.md) — creator card layout
- [Navigation](navigation.md) — account menu avatar
