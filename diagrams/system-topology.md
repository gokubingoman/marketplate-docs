# System Topology

> Launch infrastructure — see [Infrastructure Overview](../engineering/infrastructure-overview.md) for full detail.

```mermaid
flowchart TB
    subgraph Users["Users"]
        C[Customers]
        CR[Creators]
        AD[Admins]
    end

    subgraph Edge["Edge Layer"]
        CDN[CDN — static + images]
        LB[Load Balancer / TLS]
    end

    subgraph Compute["Compute"]
        API[marketplate-api<br/>Modular Monolith]
        WORK[marketplate-worker<br/>Events + jobs]
    end

    subgraph Data["Data Layer"]
        PG[(PostgreSQL)]
        RD[(Redis)]
        OS[(Object Storage)]
        Q[Message Queue]
    end

    subgraph External["External"]
        ST[Stripe Connect]
        EM[Email]
        AUTH[Auth Provider]
        IDV[Identity Vendor — optional]
    end

    C & CR & AD --> CDN
    C & CR & AD --> LB
    CDN --> OS
    LB --> API
    API --> PG & RD & OS & Q
    WORK --> Q & PG
    API --> ST & AUTH
    WORK --> EM
    API -.-> IDV

    style API fill:#e8f4f8
    style WORK fill:#e8f4f8
```

## Environments

| Env | Purpose | Stripe | Auth |
|-----|---------|--------|------|
| **local** | Docker Compose | Test CLI | Stub |
| **dev** | Integration | Test | Dev tenant |
| **staging** | Pre-prod QA | Test | Staging |
| **prod** | Live marketplace | Live | Production |

→ [Infrastructure Overview — Environments](../engineering/infrastructure-overview.md)
