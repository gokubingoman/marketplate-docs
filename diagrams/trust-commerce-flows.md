# Trust & Commerce Flows

> High-level sequences — full specs in [Trust Verification Flow](../pages/flows/trust-verification-flow.md) and [Customer Purchase Flow](../pages/flows/customer-purchase-flow.md).

## Creator verification (trust path)

*Human approval required at every verification decision.*

```mermaid
sequenceDiagram
    participant C as Creator
    participant App as Creator OS
    participant Trust as Trust Module
    participant AI as Verification Assist
    participant Op as Trust Operator

    C->>App: Submit identity docs
    App->>Trust: Create VerificationRecord (in_review)
    Trust->>AI: Async document analysis
    AI-->>Trust: Flags + extracted fields
    Trust->>Op: Queue item
    Op->>Trust: Approve / Reject / Request info
    Note over Op,Trust: Human decision only
    Trust->>App: Status update
    C->>App: Submit kitchen + compliance
    Op->>Trust: Final verified gate
    Trust->>App: Verified Creator — can sell
```

→ SOP: [Verification Review](../operations/verification-review-sop.md)

---

## Customer purchase (commerce path)

```mermaid
sequenceDiagram
    participant Cu as Customer
    participant M as Marketplace
    participant Cat as Catalog
    participant Ord as Order
    participant Pay as Payment
    participant Cr as Creator
    participant Notif as Notification

    Cu->>M: Discover verified creator
    Cu->>Cat: Add to cart
    Cu->>Ord: Checkout
    Ord->>Pay: PaymentIntent (Stripe)
    Pay-->>Cu: Confirm payment
    Pay->>Ord: payment.captured
    Ord->>Cr: New order
    Ord->>Notif: Confirmation email
    Cr->>Ord: Fulfill order
    Cu->>Ord: Review (post-completion)
```

→ Flow: [Order Fulfillment](../pages/flows/order-fulfillment-flow.md) · Mechanics: [Marketplace Mechanics](../product/marketplace-mechanics.md)

---

## Verified-to-sell gate

```mermaid
flowchart LR
    A[Creator signup] --> B[Identity review]
    B --> C[Kitchen review]
    C --> D[Compliance review]
    D --> E{All approved?}
    E -->|Yes| F[Verified Creator]
    E -->|No| G[Cannot accept paid orders]
    F --> H[Catalog publish allowed]
    G --> H2[Draft only / blocked checkout]
```

Hard invariant: unverified creators **never** appear in customer discovery or accept payment.

→ [Marketplace Mechanics — Verified to sell](../product/marketplace-mechanics.md#marketplace-model-overview)
