# Marketplate Values

> How we behave while building the trusted marketplace operating system for independent food creators.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

These values translate [Mission](mission.md) and [Vision](vision.md) into daily behavior. They are hiring criteria, design constraints, and escalation guides — not wall art.

When values conflict in a specific situation, **trust wins**. See [Company Philosophy](company-philosophy.md) for decision frameworks.

---

## 1. Trust Is the Product

We treat trust as a measurable outcome, not a brand adjective. Every ship decision asks whether we are making it easier for customers to buy from verified creators with confidence.

**We do:**
- Block or delay launches that weaken verification, food safety, or transparency — even when revenue is at stake
- Design customer-facing surfaces so trust signals (identity, kitchen, compliance, reviews) are visible without hunting for them
- Document trust-impacting changes with clear audit trails and rollback plans

**We don't:**
- Onboard unverified creators to hit growth targets
- Hide verification status behind vague language or buried settings
- Trade long-term credibility for short-term conversion tricks

---

## 2. Quality Over Volume

We build fewer things and build them exceptionally well. A single workflow that feels premium and reliable beats ten half-finished features.

**We do:**
- Hold a quality bar comparable to products we admire — calm interfaces, reliable systems, thoughtful edge cases
- Refuse feature bloat; cut scope before cutting quality
- Treat documentation, testing, and observability as part of "done," not follow-up work

**We don't:**
- Ship "good enough for launch" experiences that creators must apologize to their customers for
- Add configuration options to avoid making a clear product decision
- Measure success only by feature count or sprint velocity

---

## 3. Clarity Creates Confidence

Uncertainty erodes trust. We reduce ambiguity for creators, customers, and teammates through plain language, explicit states, and honest communication.

**We do:**
- Write copy, docs, and error messages that a first-time cottage food operator can act on without support
- Show loading, empty, and error states — never leave users guessing what happened
- Name things consistently across product, docs, and support (see [Glossary](glossary.md))

**We don't:**
- Use jargon to sound sophisticated when plain language would serve users better
- Bury critical information (allergens, pickup windows, verification requirements) below the fold
- Assume users will "figure it out" — if it's confusing in docs, it will be confusing in product

---

## 4. Creators Come First

We optimize for independent food entrepreneurs — not aggregators, not corporate restaurant chains, not investors seeking extraction. If a decision helps Marketplate but hurts creators, we reconsider.

**We do:**
- Price and design so creators can build durable businesses, not just transient side hustles
- Seek creator feedback before major workflow changes; creators are partners, not supply units
- Build for diverse creator types (meal prep, bakers, caterers, food trucks, cottage food, pop-ups)

**We don't:**
- Copy delivery-app patterns (race-to-bottom commissions, opaque ranking) that commoditize creators
- Optimize marketplace mechanics for volume at the expense of small creators' visibility
- Ship creator-facing tools that require a technical co-founder to operate

---

## 5. Operational Excellence Is Respect

Reliable operations are how we respect creators' time and customers' hunger. Every workflow gets an owner, an SLA, and a path to measurement.

**We do:**
- Define measurable SLAs for verification, payouts, support response, and incident resolution
- Turn every incident into documentation and, where possible, automation
- Maintain complete audit trails on trust-critical and financial workflows

**We don't:**
- Rely on heroic manual effort as a permanent substitute for systems
- Leave creators without status updates during outages or verification delays
- Treat internal ops tooling as second-class — operators deserve the same quality bar as customers

---

## 6. Documentation Is Production Code

Incomplete documentation means the feature is incomplete. We write for the engineer, designer, operator, executive, and AI agent who will consume this work years from now.

**We do:**
- Spec before code; link decisions to [ADRs](../decisions/) when significant
- Cross-reference related systems instead of duplicating content
- Keep docs evergreen — accurate, dated, and traceable to [Constitution](constitution.md)

**We don't:**
- Ship features with "we'll document it later" as the plan
- Write docs that only make sense to the author in the current sprint
- Leave vague TODOs without `TODO(decision):` when blocked on founder input

---

## 7. Humans Decide; AI Assists

AI removes repetitive work and improves consistency. It does not replace accountability — especially on trust, safety, compliance, and customer impact.

**We do:**
- Document every AI system: purpose, inputs, outputs, evaluation, fallbacks, confidence thresholds, human review
- Default to "AI recommends, human approves" on verification, moderation, and policy enforcement
- Use AI to scale internal teams without scaling errors

**We don't:**
- Auto-approve creators, listings, or trust-impacting content without human oversight paths
- Deploy AI without measurable evaluation and fallback behavior
- Use AI to avoid hard conversations or hide behind algorithmic opacity with creators

---

## 8. Design for the Long Term

We optimize for the company Marketplate becomes in ten years — maintainable architecture, international scale, regulatory adaptability — not just the next release.

**We do:**
- Prefer boring, readable technology over clever shortcuts
- Question assumptions; identify edge cases before they become incidents
- Build accessibility, localization, and observability into foundations, not backlogs

**We don't:**
- Accumulate technical or operational debt with "we'll fix it when we're bigger" as the only plan
- Design for a single breakpoint, locale, or creator type when the vision requires breadth
- Sacrifice maintainability for speed without an explicit, time-bounded tradeoff documented in an ADR

---

## Using Values in Decisions

When facing a difficult tradeoff, walk through this sequence:

1. **Trust check** — Does either option weaken verification, safety, or transparency?
2. **Creator check** — Which option helps independent food entrepreneurs build durable businesses?
3. **Clarity check** — Which option reduces uncertainty for users and teammates?
4. **Long-term check** — Which option still looks correct at 10× scale?

If values still conflict after this sequence, escalate with explicit framing and propose a `TODO(decision):` for founder input. Do not silently compromise trust.

---

## Related Documents

- [Founding Constitution](constitution.md) — Governing principles and quality bar
- [Mission](mission.md) — What we exist to do
- [Vision](vision.md) — Where we are going
- [Company Philosophy](company-philosophy.md) — Detailed philosophies and decision frameworks
- [Glossary](glossary.md) — Shared terminology
- [Brand Voice & Tone](../brand/voice-and-tone.md) — How values sound in external communication
- [Design Principles](../design-system/principles.md) — How values manifest in interface design
- [Product Overview](../product/overview.md) — Product expression of values
- [Marketplace Mechanics](../product/marketplace-mechanics.md) — Trust operationalization
