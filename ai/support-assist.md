# Support Assist

> AI-assisted help discovery, ticket classification, and operator macros. Customer-facing search on [Help](../pages/customer/help.md); internal triage for support ops.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** AI Platform  
**Service owner:** [Notification Service](../engineering/services/notification-service.md) (tickets) · shared search infra

---

## Purpose

Support Assist powers semantic search on the customer [Help](../pages/customer/help.md) center, classifies inbound support tickets for routing and prioritization, and suggests response macros for operations staff.

The system improves deflection, routing accuracy, and response consistency. It **does not** send customer-facing replies autonomously, close tickets without human review, or access order modification APIs.

Governing principle: [Humans Decide; AI Assists](../company/values.md#7-humans-decide-ai-assists) — AI accelerates support ops; humans own customer outcomes.

---

## Problem Statement

Support volume scales with marketplace growth. Keyword FAQ search misses paraphrased questions; uncategorized tickets land in general queues; operators rewrite similar answers daily.

| Pain | Impact |
|------|--------|
| Keyword-only FAQ search | Low deflection; duplicate tickets |
| Manual ticket categorization | Slow routing; food-safety issues not prioritized |
| Inconsistent macro usage | Brand voice drift; longer handle times |
| Missing order context | Customers repeat information |

Support Assist connects customers to relevant help content and gives operators structured starting points — without replacing human support for disputes, refunds, or safety incidents.

---

## Problem Scope

### In scope

| Surface | AI role |
|---------|---------|
| **Customer Help search** | Semantic retrieval over FAQ articles; ranked results with snippets |
| **Support ticket intake** | Category, priority, sentiment-neutral urgency classification |
| **Operator assist panel** | Suggested macros, related articles, similar resolved tickets |
| **Deflection analytics** | Track search → FAQ expand → no ticket |

### Out of scope (v1)

- Autonomous chatbot replies to customers
- Automatic refunds or order changes
- Creator OS help (future separate index)
- Phone/voice support

---

## Inputs

### Customer Help search

| Input | Source |
|-------|--------|
| **Search query** | Help page search input ([Help](../pages/customer/help.md#help-search)) |
| **Optional context** | `?order=` param, category filter, locale |
| **FAQ corpus** | CMS articles: `{ id, category, question, answer, anchor, related_links }` |
| **Policy snippets** | Cancellation, fee, allergen summaries (non-legal) |

### Support ticket classification

| Input | Source |
|-------|--------|
| **Ticket fields** | Category select, message, name, email |
| **Order attachment** | Verified `order_id` when customer attaches |
| **Referrer** | Page URL, user agent |
| **Customer history** | Prior ticket count (not full transcript in model context by default) |

### Operator assist

| Input | Source |
|-------|--------|
| **Open ticket** | Full thread |
| **Macro library** | Approved templates by category |
| **Resolution KB** | Anonymized past resolutions (no PII in embeddings) |

---

## Outputs

### Customer-facing (Help search)

| Output | Description |
|--------|-------------|
| **Ranked article matches** | `{ article_id, title, snippet, relevance_score, anchor }` |
| **Suggested queries** | Query refinement when ambiguous |
| **No-AI fallback indicator** | Hidden from customer — degrades to keyword search |

Displayed on [Help](../pages/customer/help.md) — debounced 300ms search; no generative answers in v1 (retrieval only). Future: cited answer summaries with links to source articles.

### Internal (ticket pipeline)

| Output | Description |
|--------|-------------|
| **Suggested category** | Maps to Help categories + ops-only tags |
| **Priority score** | `standard` · `elevated` · `urgent` (food safety, allergic reaction) |
| **Routing queue** | e.g., `orders`, `trust`, `payments`, `general` |
| **Macro suggestions** | Top 3 macros with fill-in field predictions |
| **Related articles** | For operator sidebar |
| **Confidence** | Per classification field |

Ticket record example:

```json
{
  "ticket_id": "tkt_4412",
  "ai_assist": {
    "model_version": "support-assist-v1.0.3",
    "suggested_category": "order_issue",
    "priority": "elevated",
    "routing_queue": "orders",
    "macro_suggestions": ["macro_order_late_pickup"],
    "confidence": 0.88
  }
}
```

---

## Models

### Architecture

| Component | Approach | Hosting |
|-----------|----------|---------|
| **Semantic FAQ retrieval** | Embedding index over article chunks + hybrid keyword boost | Managed vector DB; embeddings from approved model |
| **Query understanding** | Lightweight classifier for intent (order, refund, verification, allergen) | Shared inference |
| **Ticket classification** | Multi-label classifier + LLM fallback for long messages |
| **Macro suggestion** | Embedding similarity ticket ↔ macro library |
| **Priority escalation** | Rules-first (keyword: "allergic reaction", "food poisoning") + classifier |

### Index management

- FAQ index rebuilt on CMS publish webhook
- Chunking: per FAQ question + answer sections; anchor metadata preserved for deep links
- Separate indices: customer FAQ vs. internal ops KB

### Customer-facing constraints

- Retrieval-only in v1 — no hallucinated policy answers
- Snippets extracted from source articles only
- Maximum 8 results returned; relevance threshold hides poor matches

---

## Prompt Strategy

Full prompts in [`prompts/`](../prompts/). High-level strategy:

### Ticket classification (LLM path)

- System role: **support triage assistant for internal operators**
- Input: ticket message + category + order status summary (if attached)
- Output schema: `{ category, priority, routing_queue, reasoning_internal }`
- Explicit food-safety escalation rules in system context
- Never generate customer-visible reply text in classification prompt

### Macro suggestion

- Retrieve top macros by embedding similarity
- LLM optionally ranks retrieved macros with one-line justification for operator
- Macros are **suggestions** — operator edits before send

### FAQ retrieval (non-generative)

- No LLM generation for v1 customer search — embedding similarity + BM25 hybrid
- Future generative FAQ: RAG with mandatory citation IDs; answer must be subset of retrieved chunks

### Voice alignment

- Macro suggestions tagged with [Voice and Tone](../brand/voice-and-tone.md) profile — classification only, not generation

---

## Evaluation

### Offline eval

| Eval set | Size | Focus |
|----------|------|-------|
| **FAQ retrieval queries** | 300+ paraphrased customer questions | MRR@5, hit rate@3 |
| **Ticket classification** | 800+ labeled tickets | Category accuracy, priority recall on urgent |
| **Macro suggestion** | 200+ ticket → macro pairs | Top-3 hit rate |
| **Adversarial** | Prompt injection in ticket body | No action execution |

### Targets

| Metric | Target |
|--------|--------|
| **FAQ MRR@5** | ≥ 0.75 |
| **FAQ deflection proxy** (click expand within top 3) | ≥ 60% in user testing |
| **Ticket category accuracy** | ≥ 0.85 |
| **Urgent priority recall** | ≥ 0.98 (food safety, allergic reaction) |
| **Macro top-3 hit rate** | ≥ 0.70 |

### Online metrics

- `help_search` → `help_faq_expanded` conversion ([Help analytics](../pages/customer/help.md#analytics))
- `help_deflection` event — expand without contact within 30s
- Ticket first-response time by AI routing queue
- Operator macro acceptance rate (sent without major edit)

---

## Confidence Thresholds

| Context | Threshold | Behavior |
|---------|-----------|----------|
| **FAQ result relevance** | < 0.45 similarity | Omit from results; show keyword fallback message if none |
| **FAQ top result** | ≥ 0.65 | Highlight as best match |
| **Ticket category** | ≥ 0.80 | Pre-select category in ops UI — operator confirms |
| **Ticket category** | 0.55–0.79 | Suggest with "uncertain" badge |
| **Ticket category** | < 0.55 | No suggestion; manual triage |
| **Priority urgent** | Rules override | Keyword rules always win for safety terms |
| **Macro suggestion** | ≥ 0.70 similarity | Show in operator panel |
| **Auto-routing** | **Disabled in v1** | AI suggests queue; human or rule-based auto-route only for urgent keywords |

No autonomous customer email sends. Operator must send all responses.

---

## Fallback Behaviour

| Failure | Fallback |
|---------|----------|
| **Vector index unavailable** | Keyword search on FAQ titles and bodies ([Help](../pages/customer/help.md) existing filter) |
| **Embedding API down** | BM25-only retrieval |
| **Classification timeout** | Ticket → `general` queue; standard priority |
| **Macro suggestion fail** | Operator uses manual search |
| **Partial CMS index** | Serve stale index with banner to ops; customer search unaffected if cache warm |

Customer Help page documents static FAQ fallback if CMS fails ([Help error states](../pages/customer/help.md#error-states)).

---

## Security

### PII handling

- Customer search queries logged with retention 90 days; no sale to third parties
- Ticket classification sends minimum necessary order context (status, creator name, fulfillment type) — not full payment details
- Operator assist embeddings exclude customer name/email from vector text where possible
- **No training on support tickets** without anonymization and consent

### Customer-facing search

- No injection into downstream actions from search box
- Search is read-only retrieval
- Rate limiting on search API — prevent scraping

### Internal

- Macro library write access restricted — AI cannot add macros
- Ticket AI outputs not visible to customers

### Isolation

- Support indices separate from moderation and verification document stores
- Cross-service order lookup via authenticated API only

---

## Human Approval

| Action | Human gate |
|--------|------------|
| Customer sees FAQ results | Retrieval-only — no approval needed |
| Ticket priority `urgent` | Ops validates urgent queue items at start of shift |
| Send macro / reply | Operator always edits and sends |
| Route to Trust & Safety | Suggested only; ops confirms for non-keyword cases |
| Close ticket | Human action |
| Refund / order change | Outside AI scope — human workflows |

Food safety and allergic reaction categories route to priority queue with SLA alert — human must acknowledge.

---

## Monitoring

### Operational

| Metric | Alert |
|--------|-------|
| Search latency p95 | > 500ms |
| Index lag (CMS → vector) | > 15 min |
| Classification error rate | > 2% |
| Fallback to keyword rate | > 20% / 1 hr |

### Quality

| Metric | Cadence |
|--------|---------|
| FAQ search zero-result rate | Daily |
| Deflection rate | Weekly |
| Ticket reclassification rate | Weekly |
| Macro edit distance (sent vs. suggested) | Monthly |

### Cost

- Embedding cost per FAQ rebuild
- Query cost per search (cached queries for popular terms)

---

## Continuous Improvement

### Feedback loops

1. Zero-result searches → new FAQ candidates
2. Tickets where operator changed AI category → classifier training
3. High-edit macros → template improvements
4. `help_deflection` false positives → retrieval tuning

### Content ops

- FAQ updates trigger automatic re-embed
- Seasonal content (holiday ordering) flagged for review

### Roadmap ([Help future improvements](../pages/customer/help.md#future-improvements))

- AI-assisted FAQ answers with citations (RAG)
- In-app chat with human handoff
- Localized help indices by jurisdiction
- Creator OS help index (separate from customer)

---

## Related Documents

- [Help](../pages/customer/help.md) — Customer-facing surface
- [Founding Constitution — AI Philosophy](../company/constitution.md#ai-philosophy)
- [Values — Clarity Creates Confidence](../company/values.md#3-clarity-creates-confidence)
- [Voice and Tone](../brand/voice-and-tone.md)
- [Notification Service](../engineering/services/notification-service.md)
- [Moderation Assist](moderation-assist.md) — Escalation path for trust reports
- [AI Platform README](README.md)
