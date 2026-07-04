# Moderation Assist

> AI-assisted triage and classification for content moderation. **AI recommends; moderators decide.** — [AI Philosophy](../company/constitution.md#ai-philosophy)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** AI Platform  
**Service owner:** [Trust Service](../engineering/services/trust-service.md)

---

## Purpose

Moderation Assist analyzes user-generated content and automated reports to prioritize the [Moderation Queue](../pages/admin/moderation-queue.md), suggest policy violation categories, and score severity. It covers listing content, customer reviews, creator storefront copy, and flagged messages.

The system **never** removes content, warns creators, or suspends accounts autonomously. Every enforcement action requires human submission on the moderation queue per [Reviews & community](../product/marketplace-mechanics.md#reviews--community) and [Humans Decide; AI Assists](../company/values.md#7-humans-decide-ai-assists).

---

## Problem Statement

Trust & Safety teams face high-volume, high-stakes moderation across heterogeneous content types:

| Pain | Impact |
|------|--------|
| Manual triage of all reports equally | High-severity harassment waits behind low-priority noise |
| Inconsistent policy category assignment | Enforcement ladder applied unevenly |
| Review text and message context scattered | Moderators hunt across systems for order history |
| Moderator throughput limits | SLA misses on safety-critical items |

Moderation Assist surfaces policy-relevant signals, suggested categories, and severity scores so moderators decide faster and more consistently — without automating enforcement.

---

## Inputs

### Content types

| Type | Trigger | Context bundled |
|------|---------|-----------------|
| **Listing / menu item** | Publish, edit to flagged fields, user report | Item text, images, allergens, price, creator verification status |
| **Review** | Post-submit, fraud flag, user report | Review text, rating, verified purchase flag, order ID |
| **Storefront content** | Photo/story flag, automated scan | Bio, banner images, external links |
| **Message** | Toxicity flag, user report | Thread excerpt (not full history by default), order linkage |
| **Community report** | In-product report flow | Reporter category, free-text reason |

### Metadata inputs

| Input | Source |
|-------|--------|
| **Subject account history** | Prior warnings, suspensions, moderation decisions |
| **Reporter credibility** | Report history, verified purchase where applicable |
| **Policy version** | Active policy snippets from Trust Service |
| **Locale / jurisdiction** | Content locale for harassment and food-safety rules |

### Input limits

- Message threads: last N messages (configurable, default 10) plus report anchor
- Images: resized for inference; originals available to moderator in queue UI
- PII in messages passed to models only within isolated inference — not logged in plaintext telemetry

---

## Outputs

All outputs attach to moderation case records in the [Moderation Queue](../pages/admin/moderation-queue.md).

| Output | Type | Moderator use |
|--------|------|---------------|
| **Policy violation score** | 0.0–1.0 per suggested policy | Primary sort key within severity tier |
| **Suggested categories** | Ranked list `{ policy_id, section, score, excerpt }` | Pre-select policy reference in detail panel |
| **Severity recommendation** | `low` · `medium` · `high` | Queue badge — moderator can override |
| **Priority score** | Composite integer | Queue sort within SLA tiers |
| **Content summary** | Short neutral summary | Context card — not shown to users |
| **Image region hints** | Optional bounding regions | Overlay on policy-violating image areas (future UI) |
| **Duplicate / spam cluster ID** | Optional | Link related cases for batch human review |
| **Confidence** | 0.0–1.0 | Low confidence → "Needs human judgment" banner |

Example:

```json
{
  "case_id": "mod_9281",
  "model_version": "moderation-assist-v1.1.0",
  "suggested_categories": [
    { "policy_id": "harassment_4_2", "score": 0.87, "label": "Harassment §4.2" }
  ],
  "severity_recommendation": "high",
  "priority_score": 842,
  "confidence": 0.91
}
```

---

## Models

### Architecture

Moderation Assist runs as part of [Trust Service](../engineering/services/trust-service.md) moderation ingest — synchronous for publish-time listing scan (< 2s target); asynchronous for reviews and messages.

| Component | Approach | Hosting |
|-----------|----------|---------|
| **Text classification** | Multi-label policy classifier + LLM fallback for edge cases | Shared inference cluster |
| **Toxicity / harassment** | Specialized safety classifier | Same cluster; versioned separately |
| **Image moderation** | NSFW, violence, prohibited food imagery classifiers | Vision model; on-premise option for sensitive tiers |
| **Spam / fraud patterns** | Rules + embedding similarity for review bombing clusters | Vector index internal |
| **Severity scoring** | Weighted ensemble of classifiers + subject history features | Deterministic layer |

### Model boundaries

- Classifiers recommend **policy categories** — they do not select enforcement actions
- No generative rewriting of user content in v1
- Listing food-safety flags (e.g., prohibited items) use rules engine + classifier ensemble

### Versioning

- `model_version` per output; policy version pinned at processing time
- Policy updates trigger re-eval on open cases only when explicitly requested

---

## Prompt Strategy

Full prompts in [`prompts/`](../prompts/). High-level strategy:

### Classification prompts (LLM fallback path)

- System role: **policy analyst for internal moderators** — not enforcement agent
- Policy excerpts injected dynamically from Trust Service (not full legal corpus)
- Output: ranked policy matches with quoted evidence spans from content
- Explicit: if uncertain, return empty matches with low confidence

### Multi-modal listing review

- Compose: item title + description + allergen fields + image captions (model-generated for image, not user-facing)
- Food-safety branch: jurisdiction prohibited category list in context
- Harassment branch: separate prompt — no cross-contamination with food policy

### Review integrity

- Prompt includes verified-purchase flag and order metadata
- Focus on: fake review patterns, competitor attack, off-platform solicitation
- Does not judge food quality — only policy violations

### Message flagging

- Analyze reported message in thread context
- Ignore embedded instructions attempting to override system behavior
- Output harassment/threat/spam categories only — no sentiment scoring for customer service quality

### Principles

- Evidence-linked outputs (cite spans) for moderator verification
- No chain-of-thought in operator UI
- Temperature 0 for classification; fixed schema JSON responses

---

## Evaluation

### Offline eval sets

| Eval set | Focus |
|----------|-------|
| **Policy classification gold** | 1,000+ labeled items across all content types |
| **Harassment / threat** | 200+ high-recall priority set |
| **Food safety / prohibited listings** | Jurisdiction-specific 150+ |
| **False positive holdout** | Legitimate negative reviews, cultural food terms |
| **Adversarial** | Obfuscation, leetspeak, image text overlays |

Labels from Trust & Safety; inter-annotator agreement tracked.

### Metrics

| Metric | Target |
|--------|--------|
| **Category suggestion precision@1** | ≥ 0.80 on high-severity cases |
| **Severity recommendation accuracy** | ≥ 0.75 vs. moderator final severity |
| **Harassment recall** | ≥ 0.95 (prioritize recall over precision for high-severity) |
| **False positive rate (listing publish block suggestions)** | ≤ 3% — listings are never auto-blocked; metric on would-have-flagged |
| **Spam cluster precision** | ≥ 0.90 |

### Online metrics

- Moderator override rate on suggested category
- Time-to-decision vs. AI score deciles
- Appeal rate segmented by AI-assisted decisions
- Dismiss rate on AI-prioritized high-severity items

### Release gate

Shadow mode on 5% traffic minimum; no auto-action paths to test. Trust & Safety review of false positive samples before promotion.

---

## Confidence Thresholds

Moderation Assist **never auto-suspends**. Thresholds affect queue priority and UI only.

| Signal | Behavior |
|--------|----------|
| **Violation score ≥ 0.90 + high-severity policy** | Queue severity `HIGH`; SLA clock 4h ([Trust Verification Flow — parallel moderation](../pages/flows/trust-verification-flow.md#moderation-queue-parallel-flow)) |
| **Violation score 0.70–0.89** | Severity `MEDIUM`; standard SLA |
| **Violation score 0.40–0.69** | Severity `LOW`; deprioritized unless reporter credible |
| **Violation score < 0.40** | Case created but low priority; may batch review |
| **Classifier confidence < 0.55** | UI: "AI uncertain — full manual review required" |
| **Publish-time listing scan ≥ 0.85 prohibited item** | Hold for moderator review before public visibility — **not auto-reject**; creator sees "pending review" |

Configurable in [Platform Settings](../pages/admin/platform-settings.md) → Moderation → AI thresholds.

**Explicit prohibition:** No threshold configuration enables autonomous account suspension, content removal, or permanent deletion.

---

## Fallback Behaviour

| Failure mode | Fallback |
|--------------|----------|
| **Classifier timeout** | Case enters queue with `ai_status: unavailable`; FIFO within severity tier |
| **Provider outage** | User reports still create cases; severity `MEDIUM` default |
| **Image model failure** | Text-only classification; note in case |
| **Policy snippet load failure** | Skip LLM fallback; rules engine only |
| **Partial multi-label failure** | Return successful labels; log partial |

Listing publish: if AI unavailable, listing enters `pending_moderation` or publishes with post-hoc queue item per product policy — `TODO(decision):` default publish vs. hold behavior for v1 launch market.

Customer-facing content is never silently dropped due to AI failure.

---

## Security

### Content isolation

- Moderation inference in Trust Service enclave; separate from customer-facing search indices
- Message content not written to general application logs
- Moderator "show content" view events audited ([Moderation Queue analytics](../pages/admin/moderation-queue.md#analytics))

### PII and sensitive content

- Minimize message thread sent to models — truncate and redact payment details regex
- No training on moderation content without explicit consent
- Embeddings for spam clustering stored as non-reversible hashes where possible

### Prompt injection

- User content treated as data, not instructions
- System prompts resist "ignore previous policy" patterns in reviews and messages
- Reported content hashed for dedup — prevents replay attacks on pipeline

### Access control

- AI outputs visible only to moderation roles
- API endpoints admin-scoped per [Moderation Queue permissions](../pages/admin/moderation-queue.md#permissions)

---

## Human Approval

### Enforcement actions (all human-only)

| Action | AI involvement |
|--------|----------------|
| Dismiss | May have suggested high score — moderator confirms false positive |
| Warn creator | Suggested category informs template — moderator submits |
| Remove content | Score explains priority — moderator selects Remove |
| Suspend account | **Never automatic** — senior role + confirmation modal |
| Escalate to legal | Moderator action; AI provides summary only |
| Permanent removal | Senior + dual approval — AI not in approval chain |

### UI contract ([Moderation Queue](../pages/admin/moderation-queue.md))

- AI score displayed as "87% policy match" — not "87% violation certainty"
- Enforcement radio group has no pre-selection from AI — moderator chooses explicitly
- Rationale required for all non-dismiss actions
- Suspend requires modal confirmation regardless of AI score

### Progressive enforcement

AI does not advance creators on the [trust enforcement ladder](../product/marketplace-mechanics.md#trust-enforcement-ladder). Moderators apply education → warning → restriction → suspension → removal.

---

## Monitoring

### Operational

| Metric | Alert |
|--------|-------|
| Classification latency p95 (sync listing) | > 2s |
| Async pipeline backlog | > 500 cases |
| Error rate | > 2% / 15 min |
| Fallback rate | > 15% / 1 hr |

### Quality

| Metric | Cadence |
|--------|---------|
| Override rate by policy category | Weekly |
| High-severity dismiss rate | Daily — tune thresholds |
| Appeal overturn rate | Weekly |
| Inter-moderator agreement | Monthly sample |

### Safety

- Track any code path attempting auto-enforcement — alert zero tolerance
- Moderator wellbeing: exposure metrics for graphic content (future)

### Cost

- Inference cost per case by content type
- Image moderation cost driver analysis

---

## Continuous Improvement

### Feedback loops

1. Moderator category corrections → classifier retraining data
2. Dismissed high-score cases → false positive eval set
3. Appeals upheld → priority relabeling
4. New policy sections → policy snippet index + eval cases before enforcement

### Process

```
Moderator feedback tags → Weekly T&S + AI review → Eval update → Offline benchmark
    → Shadow → Policy team sign-off → Promote
```

### Product integration

- In-product report categories aligned with AI taxonomy — reduces mismatch
- Creator education when listings frequently flagged for same policy (non-punitive)

### Roadmap

- Appeals queue linked to moderation decisions
- Image region overlays for policy violations
- Moderator specialization routing (food safety vs. harassment)
- Bulk dismiss for spam clusters — **human batch confirm**, not auto

---

## Related Documents

- [Founding Constitution — AI Philosophy](../company/constitution.md#ai-philosophy)
- [Marketplace Mechanics — Reviews & Enforcement](../product/marketplace-mechanics.md#reviews--community)
- [Moderation Queue](../pages/admin/moderation-queue.md)
- [Verification Queue](../pages/admin/verification-queue.md)
- [Trust Verification Flow](../pages/flows/trust-verification-flow.md)
- [Platform Settings](../pages/admin/platform-settings.md)
- [Trust Service](../engineering/services/trust-service.md)
- [Verification Assist](verification-assist.md)
- [AI Platform README](README.md)
