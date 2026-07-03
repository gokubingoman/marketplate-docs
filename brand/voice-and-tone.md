# Voice and Tone

> How Marketplate sounds across every touchpoint — consistent voice, context-appropriate tone.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03

---

## Voice vs. Tone

| Concept | Definition | Stability |
|---------|------------|-----------|
| **Voice** | Marketplate's personality in words — who we are | Constant across all contexts |
| **Tone** | How voice adapts to situation and audience | Varies by context, emotion, and urgency |

Our voice reflects [brand personality](brand-strategy.md#brand-personality): trustworthy, warm, precise, calm, premium, and human.

---

## Voice Attributes

### 1. Trustworthy

Say what is true. Show evidence. Never imply verification that does not exist.

| Do | Don't |
|----|-------|
| "This creator has completed identity verification." | "100% guaranteed safe!" |
| "Pickup is between 5:00–5:30 PM at the listed address." | "Your order will be ready soon!" |

### 2. Warm

Food is personal. Acknowledge the human on both sides of the transaction.

| Do | Don't |
|----|-------|
| "Maria's Kitchen prepares your order fresh for each pickup window." | "Vendor #4821 will fulfill." |
| "We're sorry your order didn't meet expectations." | "Ticket #92847 has been logged." |

### 3. Precise

Specific beats vague — especially for money, time, allergens, and policies.

| Do | Don't |
|----|-------|
| "Total: $47.50 (includes $3.50 service fee). Pickup Saturday, 11:00 AM." | "Your total may vary. See checkout for details." |
| "Contains: wheat, eggs, dairy." | "May contain allergens." |

### 4. Calm

Confidence without pressure. No artificial urgency or fear-based language.

| Do | Don't |
|----|-------|
| "Order by Thursday at 6 PM for this week's menu." | "Only 2 left! Order NOW before it's gone!" |
| "Take a moment to review your pickup details." | "Hurry! Cart expires in 3:00!" |

### 5. Premium

Quality in word choice — concise, polished, never cheap or gimmicky.

| Do | Don't |
|----|-------|
| "Discover verified local creators." | "Find yummy eats near u!" |
| "Your order is confirmed." | "Woohoo! You're all set!!! 🎉🎉🎉" |

### 6. Human

Write for people. AI assists behind the scenes; customer-facing copy is human-reviewed.

| Do | Don't |
|----|-------|
| "Our team will review your verification within 2 business days." | "An automated system has processed your request." |
| "A support specialist will follow up." | "Your inquiry has been routed to Tier 1." |

---

## Writing Principles

1. **Lead with clarity** — Most important information first.
2. **Use plain language** — Prefer "pickup window" over "fulfillment slot."
3. **Write actively** — "Confirm your order" not "Order confirmation can be completed."
4. **Be scannable** — Short paragraphs, meaningful headings, bullets for lists.
5. **Respect attention** — Every word earns its place.
6. **Creator-first in marketplace contexts** — Lead with the creator's name, not "Marketplate user."

→ Capitalization and naming rules: [naming-conventions.md](naming-conventions.md)

---

## Tone by Context

### Marketing & Growth

**Tone:** Inspiring, confident, story-driven — still calm, never hype.

**Goal:** Attract creators and customers who value trust and quality over discounts.

| Element | Guidance |
|---------|----------|
| Headlines | Lead with trust or creator identity |
| Body | Specific benefits, real stories, verification proof |
| CTAs | Clear, single action — "Start your verified storefront," not "Get started today!" |
| Social | Celebrate creators; share behind-the-kitchen content |

**Example**

> **Verified local food, made by people you can trust.**  
> Marketplate gives independent chefs the tools to build credible businesses — and gives customers confidence in every order.

---

### Product & UI Copy

**Tone:** Direct, helpful, minimal.

**Goal:** Reduce cognitive load. One primary action per screen per [design principles](../design-system/principles.md).

| Element | Guidance |
|---------|----------|
| Labels | Noun or verb-noun: "Pickup time," "Add to order" |
| Helper text | One line when needed; explain *why*, not just *what* |
| Empty states | Acknowledge + guide: "No orders yet. Share your storefront link to get started." |
| Success states | Confirm fact, suggest next step: "Order placed. Pickup Saturday at 11 AM." |

**Example**

> **Confirm pickup details**  
> Pickup is at 742 Elm Street, Saturday 11:00–11:30 AM. Orders not picked up within the window may be discarded per the creator's policy.

---

### Customer Support

**Tone:** Empathetic, accountable, resolution-focused.

**Goal:** Reduce uncertainty in every interaction — per [operations philosophy](../company/constitution.md#operations-philosophy).

| Situation | Tone adjustment |
|-----------|-----------------|
| Order issue | Empathetic + specific timeline: "I understand this is frustrating. I'll investigate and reply within 4 hours." |
| Verification delay | Transparent: "Your kitchen verification is in review. We expect a decision by [date]." |
| Policy explanation | Neutral, clear: "Refunds are handled by the creator per their stated policy. Here's how to request one." |
| Escalation | Calm urgency: "I'm escalating this to our trust team now." |

**Avoid:** Blame shifting, passive voice, canned empathy ("We apologize for any inconvenience") without action.

→ Support playbooks: [`support/`](../support/) *(Phase 4)*

---

### Error Messages

**Tone:** Calm, honest, actionable — never alarming or blaming.

**Structure:** What happened → Why (if helpful) → What to do next

| Severity | Pattern | Example |
|----------|---------|---------|
| **Validation** | Inline, specific | "Enter a valid email address." |
| **Recoverable error** | Explain + retry | "We couldn't process your payment. Check your card details and try again." |
| **System error** | Acknowledge + fallback | "Something went wrong on our end. Your order was not charged. Try again in a few minutes." |
| **Trust / safety block** | Firm, clear, no apology for enforcement | "This order cannot be completed. The creator is not accepting orders in your area." |

**Avoid:** Error codes alone, "Oops!", humor in payment or safety contexts, blaming the user ("You entered invalid data").

→ Accessibility for errors: [accessibility-standards.md](../design-system/accessibility-standards.md)

---

### Legal & Compliance

**Tone:** Formal, precise, unambiguous — still readable.

**Goal:** Legal accuracy without hiding behind jargon when plain language suffices.

| Element | Guidance |
|---------|----------|
| Terms & policies | Defined terms on first use; table of contents for long docs |
| Food safety disclosures | Factual, no marketing language mixed in |
| Consent flows | Explain what the user is agreeing to in one sentence above the legal text |
| Regulatory notices | Required language verbatim; supplementary plain-language summary when allowed |

**Example**

> **Food allergen acknowledgment**  
> By placing this order, you confirm you have reviewed the allergen information provided by the creator. Marketplate does not prepare food and cannot guarantee allergen-free preparation.

→ Legal docs: [`legal/`](../legal/) *(Phase 5)*

---

### Internal & Operations

**Tone:** Clear, direct, audit-friendly.

**Goal:** SOPs and internal comms that humans and AI agents can execute reliably.

| Element | Guidance |
|---------|----------|
| SOPs | Imperative steps, numbered, with owner and SLA |
| Incident comms | Facts first, impact, action, timeline |
| AI-assisted drafts | Human-reviewed before customer-facing send |

→ SOP template: [`templates/sop-template.md`](../templates/sop-template.md)

---

## Inclusive Language

- Use **gender-neutral defaults** ("they/them" for unknown individuals).
- Avoid idioms that do not translate across cultures.
- Write at **8th–10th grade reading level** for customer-facing copy; legal excepted.
- Do not use disability metaphors ("blind spot," " crazy fast").
- **Food and culture:** Respect diverse cuisines without exoticizing or tokenizing.

---

## Localization Readiness

Write for translation from day one:

- Full sentences, not fragments stitched in UI
- Avoid string concatenation ("You have " + count + " orders")
- No puns or culture-specific humor in core flows
- Expand abbreviations on first use in legal and safety contexts

TODO(decision): Primary launch locale(s) and whether creator-facing copy defaults to US English food-regulation terminology globally at launch.

---

## Voice Checklist

Before publishing any customer-facing copy, confirm:

- [ ] Is the most important information first?
- [ ] Would a customer trust this statement? Is it verifiable?
- [ ] Is timing, money, or safety information specific?
- [ ] Is there one clear action (not three competing CTAs)?
- [ ] Does it sound human, not robotic or overly casual?
- [ ] Does it follow [naming conventions](naming-conventions.md)?

---

## Related Documents

- [Founding Constitution](../company/constitution.md)
- [Brand Strategy](brand-strategy.md)
- [Positioning](positioning.md)
- [Naming Conventions](naming-conventions.md)
- [Design System Principles](../design-system/principles.md)
- [Accessibility Standards](../design-system/accessibility-standards.md)
- [Support Playbooks](../support/) *(Phase 4)*
