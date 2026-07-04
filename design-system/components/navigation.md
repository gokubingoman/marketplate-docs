# Navigation

> Wayfinding across customer and creator surfaces — global nav, sidebars, tabs, breadcrumbs, pagination, and segmented controls.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Purpose

Navigation provides predictable wayfinding across platform surfaces. Consistent placement and active states implement [accessible, calm interfaces](../principles.md#6-accessibility-first) — users always know where they are and how to move.

### Components

| Component | Usage | Primary audience |
|-----------|-------|----------------|
| **Top nav bar** | Global navigation — logo, search, account, cart | All users |
| **Sidebar nav** | Creator dashboard — persistent section links | Creators |
| **Tab bar (mobile)** | Customer app bottom nav — Home, Search, Orders, Account | Customers |
| **Breadcrumbs** | Dashboard depth — Settings → Verification → Kitchen | Creators |
| **Pagination** | Order history, review lists, admin tables | All users |
| **Segmented control** | Toggle views — "Active menu" / "Draft menu" | Creators |

**Appears on:** All authenticated surfaces. Mobile bottom tab bar for customer app.

→ Inventory context: [components-overview.md](../components-overview.md#navigation)

---

## Anatomy

### Top nav bar

```
┌────────────────────────────────────────────────────────────┐
│ [Logo]     [Search…………………]     [Cart] [Account ▾]         │
└────────────────────────────────────────────────────────────┘
```

| Part | Required | Description |
|------|----------|-------------|
| **Logo** | Yes | Links to home; `aria-label="Marketplate home"` |
| **Primary links** | Context-dependent | Hidden on mobile — moved to tab bar |
| **Search** | Customer-facing | Collapses to icon on mobile |
| **Utility actions** | Yes | Cart, notifications (future), account |
| **Container** | Yes | Sticky optional; `surface-default` background |

### Sidebar nav (creator dashboard)

```
┌──────────────┐
│ Dashboard    │  ← Nav item (active state)
│ Menu         │
│ Orders       │
│ ──────────── │
│ Settings     │
└──────────────┘
```

### Mobile tab bar

```
┌──────┬──────┬──────┬──────┐
│ Home │Search│Orders│ Acct │
│  ○   │  ○   │  ○   │  ○   │
└──────┴──────┴──────┴──────┘
```

Fixed bottom; 4 items maximum. Icon + label stacked.

---

## Sizes & Dimensions

| Component | Height | Item padding | Typography |
|-----------|--------|--------------|------------|
| **Top nav bar** | 56px (mobile), 64px (desktop) | `space-4` horizontal | `text-ui-lg` |
| **Sidebar item** | 44px | `space-4` horizontal, `space-3` vertical | `text-ui-md` |
| **Tab bar item** | 56px + safe area | `space-2` vertical | `text-ui-sm` |
| **Breadcrumb** | auto | `space-1` between items | `text-body-sm` |
| **Pagination button** | 44px | `space-3` | `text-ui-md` |
| **Segmented control** | 40px | `space-1` internal | `text-ui-md` |

**Icon size:** 20px (nav), 24px (tab bar).

**Border radius:** `radius-md` for segmented control segments; nav items use background fill, not pill.

---

## States

### Nav link / sidebar item / tab bar item

| State | Background | Text | Indicator |
|-------|------------|------|-----------|
| **Default** | transparent | `text-secondary` | none |
| **Hover** | `surface-subtle` | `text-primary` | none |
| **Focus** | transparent | `text-primary` | `border-focus` outline |
| **Active / current** | `color-trust-subtle` | `color-trust-default` | Optional 2px bottom bar (top nav) or left bar (sidebar) |
| **Disabled** | transparent | `text-disabled` | none |

Active state uses `aria-current="page"` on current link.

### Segmented control

| State | Background | Text |
|-------|------------|------|
| **Container** | `color-neutral-100` | — |
| **Segment default** | transparent | `text-secondary` |
| **Segment selected** | `surface-default` + subtle shadow | `text-primary`, weight 600 |
| **Segment hover** | `surface-subtle` | `text-primary` |
| **Segment focus** | — | `border-focus` outline |
| **Segment disabled** | transparent | `text-disabled` |

### Pagination

| State | Background | Text | Border |
|-------|------------|------|--------|
| **Default** | `surface-default` | `text-primary` | `border-default` |
| **Hover** | `surface-subtle` | `text-primary` | `border-default` |
| **Focus** | `surface-default` | `text-primary` | `border-focus` |
| **Active page** | `color-trust-subtle` | `color-trust-default` | none |
| **Disabled** | `surface-default` | `text-disabled` | `border-default` |

No loading state on nav itself. Content area shows loading while nav remains interactive.

---

## Component Tokens

| Token | Maps to | Context |
|-------|---------|---------|
| `nav-background` | `surface-default` | Top nav, sidebar |
| `nav-text` | `text-secondary` | Default links |
| `nav-text-active` | `color-trust-default` | Current page |
| `nav-background-active` | `color-trust-subtle` | Active item fill |
| `nav-border` | `border-subtle` | Nav bottom border, sidebar divider |
| `tab-bar-background` | `surface-default` | Mobile bottom bar |
| `breadcrumb-text` | `text-tertiary` | Separator and inactive crumbs |
| `breadcrumb-text-current` | `text-primary` | Current page (not linked) |

→ Semantic source: [color foundations](../foundations/color.md)

---

## Token Usage Summary

| Property | Token |
|----------|-------|
| Nav link typography | `text-ui-md` (sidebar), `text-ui-lg` (top nav) |
| Tab bar label | `text-ui-sm` |
| Breadcrumb | `text-body-sm` |
| Nav height padding | `space-4` |
| Sidebar width | 240px (desktop), overlay drawer (mobile) |
| Tab bar z-index | `z-sticky` |
| Top nav z-index | `z-sticky` |
| Item gap | `space-6` (top nav links) |

→ Typography: [typography foundations](../foundations/typography.md)  
→ Spacing: [spacing foundations](../foundations/spacing.md)

---

## Accessibility

Target: **WCAG 2.2 AA** → [accessibility standards](../accessibility-standards.md)

| Requirement | Implementation |
|-------------|----------------|
| **Landmarks** | `<header>`, `<nav aria-label="Primary">`, `<nav aria-label="Dashboard">` |
| **Skip link** | "Skip to main content" — first focusable element |
| **Current page** | `aria-current="page"` on active nav item |
| **Keyboard** | All nav items focusable; `Tab` through nav; sidebar `Enter` to navigate |
| **Tabs pattern** | Tab bar uses `role="tablist"`, items `role="tab"`, panels `role="tabpanel"` if switching content in-page |
| **Segmented control** | `role="tablist"` or radio group pattern; arrow keys switch segments |
| **Breadcrumbs** | `<nav aria-label="Breadcrumb">`; ordered list; current page not a link |
| **Pagination** | `aria-label="Pagination"`; current page `aria-current="page"`; disabled prev/next `aria-disabled` |
| **Mobile tab bar** | 44px min touch target per item; visible text labels (not icon-only) |
| **Cart badge** | `aria-live="polite"` for count updates — "3 items in cart" |

No keyboard-only hover menus. Dropdown account menu: `Enter`/`Space` open, `Escape` close, arrow navigation.

---

## Responsive Behavior

| Breakpoint | Top nav | Sidebar | Tab bar | Breadcrumbs |
|------------|---------|---------|---------|-------------|
| **Mobile (320–767px)** | Logo + search icon + cart + menu/account. Height 56px. | Hidden — hamburger opens drawer overlay | Fixed bottom, 4 tabs | Truncate middle crumbs: `Settings … Kitchen` |
| **Tablet (768–1023px)** | Full search bar. No tab bar. | Collapsible sidebar, 64px icon-only or 240px | Hidden | Full path visible |
| **Desktop (1024px+)** | Full nav with inline links where applicable | Persistent 240px sidebar | Hidden | Full path |

**Sticky behavior:**

- Top nav: sticky top, `z-sticky`, `border-subtle` bottom border
- Mobile tab bar: fixed bottom with safe-area-inset padding
- Sidebar: fixed left, scrollable if content exceeds viewport

**Collapse rules:** Customer primary nav moves to tab bar on mobile — not duplicated in top nav. Creator dashboard uses hamburger → drawer on mobile, persistent sidebar on tablet+.

**Content parity:** All nav destinations reachable at every breakpoint — nothing hidden exclusively on mobile without equivalent access.

---

## Do / Don't

### Do

- Keep **nav placement consistent** across pages
- Show **clear active state** on current section
- Limit mobile tab bar to **4 items**
- Use **breadcrumbs** for dashboard depth 2+
- Make **logo link to home** from all pages
- Include **skip navigation** link

### Don't

- Hide critical destinations on mobile without tab bar or menu equivalent
- Use icon-only tab bar labels
- Show multiple active nav items simultaneously
- Replace breadcrumbs with browser back only
- Auto-expand submenus on hover without keyboard access
- Add more than one primary nav pattern per viewport (top + bottom for same links)

---

## Related Documents

- [Design Principles](../principles.md)
- [Components Overview](../components-overview.md#navigation)
- [Color Foundations](../foundations/color.md)
- [Typography Foundations](../foundations/typography.md)
- [Spacing Foundations](../foundations/spacing.md)
- [Accessibility Standards](../accessibility-standards.md)
- [Avatars](avatars.md) — account menu
- [Inputs](inputs.md) — search input
- [Buttons](buttons.md) — pagination controls
