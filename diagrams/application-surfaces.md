# Application Surfaces

> Three surfaces, one platform — see [Architecture Overview](../engineering/architecture-overview.md#three-application-surfaces).

```mermaid
flowchart TB
    subgraph Surfaces["Application Surfaces"]
        CW[Customer Marketplace<br/>/]
        CD[Creator OS<br/>/dashboard]
        AC[Admin Console<br/>/admin]
    end

    GW[API Gateway / BFF]

    subgraph Modules["Domain Modules — Modular Monolith"]
        ID[Identity]
        TR[Trust]
        CA[Catalog]
        OR[Order]
        PA[Payment]
        DI[Discovery]
        NO[Notification]
    end

    subgraph AI["AI — Human Gated"]
        VA[Verification Assist]
        MA[Moderation Assist]
        SA[Support Assist]
    end

    CW --> GW
    CD --> GW
    AC --> GW

    GW --> ID & TR & CA & OR & PA & DI & NO

    TR --> VA
    TR --> MA
    NO --> SA

    style TR fill:#fff3e0
    style VA fill:#fce4ec
    style MA fill:#fce4ec
    style SA fill:#fce4ec
```

## Access matrix

| Surface | Auth required | MFA | Primary modules |
|---------|---------------|-----|-----------------|
| Customer | Optional browse; required checkout | No | Discovery, Catalog, Order, Payment |
| Creator | Yes | Recommended | Catalog, Order, Trust, Payment |
| Admin | Yes | **Required** | Trust, Order, Payment, Admin config |

→ [Information Architecture — Access Matrix](../pages/information-architecture.md#authentication--access-matrix)
