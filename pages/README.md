# Pages

Page specifications and information architecture for Marketplate.

**Phase 2 status:** Complete

---

## IA & Navigation

| Document | Description |
|----------|-------------|
| [Information Architecture](information-architecture.md) | Site map, page inventory, URL conventions, content hierarchy |
| [Navigation Model](navigation-model.md) | Global, contextual, and mobile navigation patterns |

---

## User Flows

End-to-end journeys across surfaces — entry points, state transitions, and page index.

| Flow | Description | Surfaces |
|------|-------------|----------|
| [Customer Purchase Flow](flows/customer-purchase-flow.md) | Discovery → storefront → item → cart → checkout → confirmation → tracking → review | Customer Marketplace |
| [Creator Onboarding Flow](flows/creator-onboarding-flow.md) | Signup → identity → kitchen → compliance → first listing → first order | Auth → Creator OS |
| [Order Fulfillment Flow](flows/order-fulfillment-flow.md) | Creator order queue: new → confirmed → in production → ready → completed (+ customer mirror) | Creator OS ↔ Customer Marketplace |
| [Trust Verification Flow](flows/trust-verification-flow.md) | Internal ops: submission → review → approve/reject/request info → creator notification | Admin ↔ Creator OS |

---

## Page Specs

Page specs live in subfolders by surface area. Each spec follows [`templates/page-doc-template.md`](../templates/page-doc-template.md).

| Folder | Surfaces |
|--------|----------|
| `customer/` | Marketplace, discovery, checkout, account |
| `creator/` | Creator dashboard and operating system |
| `auth/` | Authentication and onboarding |
| `admin/` | Internal ops and trust & safety |

Every page spec must map to an entry in the [page inventory](information-architecture.md#page-inventory) and declare its primary persona from [Personas](../product/personas.md).

---

## Related Documents

- [Founding Constitution](../company/constitution.md)
- [Product Overview](../product/overview.md)
- [Marketplace Mechanics](../product/marketplace-mechanics.md)
- [Design System Principles](../design-system/principles.md)
- [Phased Rollout](../roadmap/phased-rollout.md)
