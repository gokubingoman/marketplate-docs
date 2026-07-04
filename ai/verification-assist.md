# Verification Assist

> AI-assisted document analysis for creator identity, kitchen, and compliance verification. **AI recommends; operators approve.** — [AI Philosophy](../company/constitution.md#ai-philosophy)

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** AI Platform  
**Service owner:** [Trust Service](../engineering/services/trust-service.md)

---

## Purpose

Verification Assist pre-processes creator verification submissions before they reach the [Verification Queue](../pages/admin/verification-queue.md). It extracts structured fields from uploaded documents, scores document quality, flags mismatches and fraud signals, and surfaces a structured summary for Trust & Safety operators.

The system **never** approves, rejects, or changes verification status. All outcomes require human action on the admin queue per [Humans Decide; AI Assists](../company/values.md#7-humans-decide-ai-assists) and [Human approval on high stakes](../product/marketplace-mechanics.md#marketplace-model-overview).

---

## Problem Statement

Manual verification review is slow, inconsistent, and error-prone at scale:

| Pain | Impact |
|------|--------|
| Operators re-type data from PDFs and photos | SLA breaches; transcription errors |
| Subtle document issues (expiry, name mismatch, tampering) missed under volume | False approvals weaken trust thesis |
| Inconsistent checklist completion | Audit gaps; uneven enforcement |
| No prioritization signal | Fraud cases wait in FIFO with routine submissions |

Verification Assist reduces repetitive extraction work, standardizes flag presentation, and elevates high-risk cases — while preserving operator judgment as the sole decision authority.

---

## Inputs

### Primary inputs

| Input | Source | Notes |
|-------|--------|-------|
| **Uploaded documents** | Creator verification flows — identity, kitchen, compliance | PDF, JPEG, PNG; max size enforced at upload |
| **Document metadata** | Trust Service ingest | `{ doc_id, type, mime, hash, upload_timestamp, page_count }` |
| **Submission context** | Creator profile + case record | Entity type, jurisdiction, verification type, resubmission flag |
| **Self-declared fields** | Creator form | Name, address, business name, license numbers — used for cross-check |
| **Prior case history** | Trust Service | Previous submissions, prior AI flags, operator decisions |

### Derived signals (non-AI)

| Signal | Use |
|--------|-----|
| Document hash | Duplicate detection; integrity audit |
| Jurisdiction template | Expected document types per [Platform Settings](../pages/admin/platform-settings.md) |
| SLA tier | Priority ordering in queue |

### Input exclusions

- Customer PII unrelated to verification case
- Payment or order data
- Unrelated creator catalog content

---

## Outputs

All outputs are **recommendations** attached to the verification case record. They appear in the AI assist panel on [Verification Queue](../pages/admin/verification-queue.md) detail view.

| Output | Type | Operator use |
|--------|------|--------------|
| **Extracted fields** | Structured JSON | Pre-fill review form; side-by-side with document viewer |
| **Document type classification** | Enum + confidence | Route to correct checklist (ID, kitchen photo, food handler cert, etc.) |
| **Document quality score** | 0–100 + reasons | Legibility, completeness, resolution; warn creator at submit if below threshold |
| **Mismatch flags** | List of `{ field, declared, extracted, severity }` | Name ≠ ID, address ≠ kitchen photo metadata, expired dates |
| **Fraud flags** | List of `{ signal, severity, explanation }` | Tampered image, duplicate doc across accounts, font inconsistency |
| **Overall assist confidence** | 0.0–1.0 | Drives UI prominence and senior-review routing |
| **Suggested checklist hints** | Non-binding | "Likely expired — verify date manually" |

### Output persistence

```json
{
  "case_id": "ver_abc123",
  "model_version": "verification-assist-v1.2.0",
  "processed_at": "2026-07-03T18:00:00Z",
  "extracted_fields": { "full_name": "...", "expiry_date": "..." },
  "quality_score": 82,
  "flags": [{ "type": "mismatch", "severity": "high", "field": "name" }],
  "confidence": 0.91
}
```

Outputs are immutable per processing run; reprocessing on resubmit creates a new version linked to the case.

---

## Models

### Architecture

Verification Assist runs as an async pipeline stage in [Trust Service](../engineering/services/trust-service.md), invoked after ingest validation and before queue insertion (see [Trust Verification Flow — Phase 2](../pages/flows/trust-verification-flow.md#phase-2--ai-pre-processing)).

| Component | Model / approach | Hosting |
|-----------|------------------|---------|
| **Document OCR & layout** | Vision-capable multimodal model | Managed inference (primary region); no document retention at provider |
| **Field extraction** | Structured output from vision + schema-constrained parsing | Same inference endpoint |
| **Document classification** | Fine-tuned classifier + rules fallback | In-house weights on shared inference |
| **Fraud / tamper detection** | Ensemble: image forensics heuristics + classifier | On-premise image analysis; no external send for raw pixels when heuristics sufficient |
| **Quality scoring** | Rule-weighted composite of OCR confidence, resolution, crop completeness | Deterministic layer post-extraction |

### Model versioning

- Every output records `model_version` and `prompt_version` (when LLM used)
- Deployments are blue/green; in-flight cases complete on prior version
- Breaking schema changes require eval gate pass before promotion

### Provider policy

- **No training on customer documents** without explicit consent and legal review
- Inference-only API calls; zero-retention agreements with providers
- Documents processed in isolated ephemeral compute; no cross-tenant batching

---

## Prompt Strategy

Full prompts live in [`prompts/`](../prompts/) (Phase 3). High-level strategy:

### System role framing

- Model acts as a **document analyst for human reviewers**, not an approver
- Explicit instruction: output uncertainty; never infer missing fields as fact
- Jurisdiction-aware context injected from template library (expected doc types, date formats)

### Structured extraction

- JSON schema output with required confidence per field
- Chain: classify document type → extract fields for type → cross-check against declared values → emit flags
- Low-confidence fields returned as `null` with reason, not guessed

### Few-shot examples

- Curated examples per document type (government ID, cottage food registration, kitchen photo) in prompt library
- Examples emphasize edge cases: partial glare, expired-but-legible docs, multi-page PDFs
- Updated via eval failures — not ad hoc in production

### Fraud signal prompts

- Separate prompt branch for tamper analysis — outputs signals with evidence description for operator
- Does not use creative interpretation; cites observable features (metadata inconsistency, clone stamp patterns)

### What we do not do

- No chain-of-thought exposed to operators (internal reasoning logged at debug tier only)
- No single mega-prompt combining unrelated verification types — type-specific prompt modules composed at runtime

---

## Evaluation

### Offline eval sets

| Eval set | Size (target) | Focus |
|----------|---------------|-------|
| **Identity gold set** | 500+ labeled docs | Field extraction accuracy, expiry detection |
| **Kitchen gold set** | 300+ | Address/facility type extraction, photo quality |
| **Compliance gold set** | 400+ | Certificate numbers, jurisdiction-specific fields |
| **Fraud holdout** | 100+ known bad | Tamper, duplicate, synthetic ID detection |
| **Adversarial** | 50+ | Blur, rotation, non-English, multi-page |

Labels maintained by Trust & Safety QA; PII-sanitized copies in isolated storage.

### Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Field extraction F1** | ≥ 0.92 per critical field (name, expiry, address) | Exact match on normalized values |
| **Flag precision** | ≥ 0.85 high-severity flags | Operator agreement on sample |
| **Flag recall** | ≥ 0.90 on known mismatch cases | Labeled mismatch set |
| **False fraud rate** | ≤ 5% | Flags dismissed without operator concern |
| **Quality score correlation** | ≥ 0.80 with operator legibility rating | Sampled reviews |

### Online evaluation

- Weekly QA sample of approved/rejected cases with AI assist present
- Track `ai_flags_dismissed` from [Verification Queue analytics](../pages/admin/verification-queue.md#analytics)
- Appeal and resubmission rate segmented by AI flag presence

### Release gate

No model or prompt promotion without:
1. Offline metric regression ≤ 1% on critical fields
2. Shadow mode comparison on 48h production traffic
3. Trust & Safety sign-off on flag UX changes

---

## Confidence Thresholds

Verification Assist has **no autonomous approval path**. Thresholds govern UI behavior and routing only.

| Confidence / signal | Behavior |
|---------------------|----------|
| **Field extraction ≥ 0.85** | Pre-fill review form; operator confirms |
| **Field extraction 0.60–0.84** | Pre-fill with "low confidence" badge; operator must verify |
| **Field extraction < 0.60** | Field left blank; "Could not extract — review manually" |
| **Any fraud flag ≥ medium severity** | Case priority → `Elevated`; fraud checklist required |
| **Fraud flag high severity** | Case priority → `Fraud suspect`; junior operators cannot approve ([Trust Verification Flow](../pages/flows/trust-verification-flow.md#security--access)) |
| **Overall assist confidence < 0.50** | AI panel shows degraded mode banner; senior review recommended |
| **Quality score < 40 at submit** | Creator warning pre-queue; case tagged `low_quality_scan` |

Thresholds configurable in [Platform Settings](../pages/admin/platform-settings.md) → Trust & Verification → AI confidence thresholds. Defaults above are v1 production values.

---

## Fallback Behaviour

| Failure mode | Fallback |
|--------------|----------|
| **AI pipeline timeout (> 30s)** | Case enters queue without AI outputs; `ai_status: unavailable` |
| **Model provider outage** | Queue without pre-fill; operators use manual checklist only |
| **Partial failure** (OCR ok, extraction fail) | Deliver quality score + raw OCR text; flags skipped |
| **Unsupported document type** | Classification → `unknown`; no extraction attempted |
| **Rate limit** | Retry with backoff (3 attempts); then fallback |
| **Schema validation fail on model output** | Discard AI output; log incident; fallback |

Creator-facing submit flow is **never blocked** by AI failure — only pre-submit quality warnings may be skipped if AI unavailable.

Per [Trust Verification Flow](../pages/flows/trust-verification-flow.md#phase-2--ai-pre-processing): *AI unavailable → case enters queue without pre-fill; operator reviews manually.*

---

## Security

### PII isolation

- Documents processed in dedicated Trust Service enclave; no replication to analytics warehouse
- AI inference receives signed, time-limited URLs — not persistent storage at model provider
- Extracted fields stored encrypted at rest; access scoped to verification roles
- Operator document viewer watermarked with `operator_id` ([Trust Verification Flow](../pages/flows/trust-verification-flow.md#security--access))

### Data handling

| Rule | Implementation |
|------|----------------|
| **No training on customer data** | Contractual + technical zero-retention; no fine-tuning on production docs without consent |
| **Retention** | AI output retained with case; raw inference logs 30 days then redacted |
| **Cross-account isolation** | Strict tenant scoping; duplicate-doc detection uses hashed fingerprints only |

### Prompt injection / adversarial uploads

- Documents treated as untrusted input; no instruction following from embedded text in images/PDFs
- System prompts include explicit ignore of document-embedded instructions
- PDF JavaScript and embedded objects stripped at ingest
- Anomaly detection on repeated submission patterns

### Audit

Every AI run logs: `{ case_id, model_version, latency_ms, flag_count, ai_status, document_hashes }` — no raw document content in logs.

---

## Human Approval

### Approval gates (non-negotiable)

| Action | AI role | Human role |
|--------|---------|------------|
| Approve verification | Summarize; pre-fill | Operator completes checklist; clicks Approve |
| Reject | Flag reasons | Operator selects reason code + rationale |
| Request info | Suggest missing items | Operator writes creator-visible message |
| Dismiss AI flag | N/A | Operator notes reason — logged in audit |
| Change verification status | **Never** | Trust & Safety only via queue actions |

### UI contract ([Verification Queue](../pages/admin/verification-queue.md))

- AI assist panel visually subordinate to checklist and document viewer
- Approve blocked if required checklist incomplete
- Approve with unresolved high-severity AI flags requires explicit confirmation modal
- AI flags are not editable — dismiss only with audit note

### Escalation

- Fraud-suspect priority cases require senior reviewer or Trust lead per platform settings
- AI cannot escalate — it only sets priority metadata for queue sort

---

## Monitoring

### Operational metrics

| Metric | Alert threshold |
|--------|-----------------|
| **Pipeline latency p95** | > 25s |
| **Pipeline error rate** | > 2% over 15 min |
| **Fallback rate** (queue without AI) | > 10% over 1 hr |
| **Provider availability** | < 99.5% rolling 24h |

### Quality metrics

| Metric | Review cadence |
|--------|----------------|
| Flag precision / recall | Weekly on QA sample |
| Field extraction error rate | Per deploy + weekly |
| Operator time-in-queue vs. AI flag count | Bi-weekly efficiency review |
| `ai_flags_dismissed` rate by flag type | Weekly — tune thresholds |

### Cost

- Cost per case processed (compute + inference tokens)
- Monthly budget cap with alert at 80%
- Document type breakdown — optimize expensive paths (multi-page PDFs)

### Dashboards

- AI Platform dashboard: latency, errors, fallback, cost
- Trust Ops dashboard: queue depth, SLA, flag distribution — linked from [Admin Dashboard](../pages/admin/admin-dashboard.md)

---

## Continuous Improvement

### Feedback loops

1. **Operator dismiss reasons** → prompt and threshold tuning backlog
2. **QA audit findings** → gold set label updates + retrain/few-shot refresh
3. **Resubmission patterns** → creator-facing guidance improvements (non-AI product)
4. **False approve incidents** → priority fraud eval expansion

### Iteration process

```
Production telemetry → Weekly AI platform review → Eval set update → Offline benchmark
    → Shadow deploy → Trust & Safety UX review → Promote → Document version bump
```

### Creator-facing improvements

- Pre-submit quality feedback reduces low-quality scans (reduces operator burden)
- Jurisdiction template updates propagate to extraction schema automatically

### Roadmap (non-v1)

- Side-by-side ID vs. selfie liveness correlation (human decision remains)
- Third-party identity provider result ingestion as supplemental signal
- Bulk compliance expiration assist (human batch review)

---

## Related Documents

- [Founding Constitution — AI Philosophy](../company/constitution.md#ai-philosophy)
- [Marketplace Mechanics — Identity & Kitchen Verification](../product/marketplace-mechanics.md#identity-verification)
- [Trust Verification Flow](../pages/flows/trust-verification-flow.md)
- [Verification Queue](../pages/admin/verification-queue.md)
- [Platform Settings](../pages/admin/platform-settings.md)
- [Trust Service](../engineering/services/trust-service.md)
- [AI Platform README](README.md)
- [Moderation Assist](moderation-assist.md) — parallel trust pipeline for content
