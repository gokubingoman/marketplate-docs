# Onboarding a New Employee

> End-to-end operational playbook for cross-functional new hire activation — access, training, systems, and culture.

**Status:** Active  
**Version:** 1.0  
**Last updated:** 2026-07-03  
**Owner:** People Operations  
**Playbook type:** Cross-functional orchestration

---

## Purpose

This playbook orchestrates **internal employee onboarding** across People Ops, IT, Security, team leads, and domain owners. It ensures every new teammate can operate Marketplate systems safely — especially trust-critical admin surfaces — and understands the company thesis before touching creator or customer data.

**Governing values:** [Operational Excellence Is Respect](../company/values.md#5-operational-excellence-is-respect) · [Documentation Is Production Code](../company/values.md#6-documentation-is-production-code) · [Humans Decide; AI Assists](../company/values.md#7-humans-decide-ai-assists)

This is not an IT ticket checklist alone. It coordinates role-specific training paths, admin access provisioning with least privilege, and 30/60/90-day success criteria.

---

## Trigger

| Trigger | Timing |
|---------|--------|
| **Offer accepted** | People Ops opens onboarding ticket (T-14 days before start) |
| **Start date confirmed** | IT and Security provisioning begins (T-7 days) |
| **Day 1** | Full playbook execution begins |
| **Role change with new system access** | Partial playbook — access + training modules for new scope |

---

## Stakeholders

| Role | Team | Responsibility |
|------|------|----------------|
| **People Ops Coordinator** | People | Master timeline, welcome logistics, 30/60/90 check-ins |
| **Hiring Manager** | Functional team | Role-specific goals, buddy assignment, first-week plan |
| **Onboarding Buddy** | Peer | Day-to-day questions, culture integration |
| **IT / Security** | Engineering | Account provisioning, device setup, MFA |
| **Trust & Safety Lead** | Trust & Safety | Admin access approval, trust training certification |
| **Engineering Lead** | Engineering | Repo access, environment setup, on-call orientation (if applicable) |
| **Legal** | Legal | Confidentiality, data handling acknowledgment |
| **Domain Doc Owner** | Varies | Role-specific doc walkthrough |

---

## Prerequisites

Before Day 1:

| Prerequisite | Owner | Complete by |
|--------------|-------|-------------|
| Signed offer letter and employment agreement | People Ops | T-7 |
| Background check cleared (trust-facing roles) | People Ops + vendor | T-3 (required before admin access) |
| Equipment ordered and shipped | IT | T-5 |
| Google Workspace / SSO account created | IT | T-1 |
| Slack workspace invite | IT | T-1 |
| Role mapped to access tier (see below) | Hiring Manager + Security | T-7 |
| Buddy assigned | Hiring Manager | T-3 |
| Day 1 calendar holds: orientation, manager 1:1, buddy intro | People Ops | T-3 |
| Trust training module assigned (if Tier 2+ access) | Trust Lead | T-1 |

---

## Access Tiers

Admin access follows least privilege per [Trust Verification Flow — Security](../../pages/flows/trust-verification-flow.md#security--access):

| Tier | Roles | Systems | Approval |
|------|-------|---------|----------|
| **Tier 0 — General** | All employees | Slack, email, Notion/wiki, Figma (view), docs repo | Hiring Manager |
| **Tier 1 — Product & Eng** | Engineers, designers, PMs | GitHub, staging environments, analytics (read), Feature flags (staging) | Eng Lead |
| **Tier 2 — Trust Operations** | Trust operators, support leads | Admin Console (verification queue, moderation, disputes), production read-only logs | Trust Lead + Security |
| **Tier 3 — Trust Senior** | Supervisors, Trust Lead | Creator suspension, payout holds, bulk exports, Platform Settings | Trust Lead + Founder |
| **Tier 4 — Engineering Production** | On-call engineers | Production deploy, database read (scoped), incident response | Eng Lead + Security |

**Hard rules:**

- No Tier 2+ until background check cleared and trust training passed
- Operators cannot review own test accounts — [Trust Service security](../../engineering/services/trust-service.md#security)
- Session timeout enforced on admin surface
- Separation of duties: junior operators cannot approve fraud-flagged cases

---

## Phase-by-Phase Execution

### Phase 1 — Pre-Boarding (T-14 to T-1)

| Step | Actor | Action |
|------|-------|--------|
| 1.1 | People Ops | Send welcome email with Day 1 logistics, dress code (if any), first-week agenda |
| 1.2 | IT | Ship equipment; create SSO account (disabled until Day 1) |
| 1.3 | Hiring Manager | Prepare 30/60/90 goals document linked to team OKRs |
| 1.4 | Hiring Manager | Assign buddy; brief buddy on onboarding responsibilities |
| 1.5 | Security | Map role to access tier; open provisioning tickets |
| 1.6 | People Ops | Send required reading list (below) for pre-start |

**Pre-start reading (all roles):**

- [Founding Constitution](../../company/constitution.md)
- [Company Values](../../company/values.md)
- [Mission](../../company/mission.md) and [Vision](../../company/vision.md)
- [Product Overview](../../product/overview.md)
- [Glossary](../../company/glossary.md)

---

### Phase 2 — Day 1 — Orientation

| Step | Actor | Action |
|------|-------|--------|
| 2.1 | People Ops | Welcome session: company history, thesis ("Trust is our product"), org chart |
| 2.2 | People Ops | Benefits, payroll, policies, code of conduct |
| 2.3 | Legal | Confidentiality and data handling acknowledgment (signed) |
| 2.4 | IT | Device setup, MFA enrollment, password manager, SSO activation |
| 2.5 | Hiring Manager | 1:1 — role expectations, 30/60/90 goals, team rituals |
| 2.6 | Buddy | Lunch or coffee; Slack tour; introduce key teammates |
| 2.7 | All | Add to relevant Slack channels per role |

**Day 1 exit criteria:** SSO active, MFA enrolled, code of conduct signed, manager 1:1 complete.

---

### Phase 3 — Week 1 — Domain Foundations

Role-specific doc deep-dives:

| Role family | Required reading | Walkthrough owner |
|-------------|------------------|-------------------|
| **Trust & Safety** | [Marketplace Mechanics — Trust Model](../../product/marketplace-mechanics.md#trust-model), [Trust Verification Flow](../../pages/flows/trust-verification-flow.md), [Trust Service](../../engineering/services/trust-service.md), [AI Platform](../../ai/README.md) | Trust Lead |
| **Engineering** | [Engineering README](../../engineering/README.md), [Service Catalog](../../engineering/service-catalog.md), relevant service docs, [docs/standards/](../standards/) | Eng Lead |
| **Product / Design** | [Marketplace Mechanics](../../product/marketplace-mechanics.md), all [page flows](../../pages/flows/), [Design Principles](../../design-system/principles.md) | PM / Design Lead |
| **Creator Ops / Support** | [Creator Onboarding Flow](../../pages/flows/creator-onboarding-flow.md), [Chef Welcome Package](../onboarding/chef-welcome-package.md), [Voice and Tone](../../brand/voice-and-tone.md) | Creator Ops Lead |
| **Marketing / Growth** | [Value Propositions](../../product/value-props.md), [Brand Voice](../../brand/voice-and-tone.md), trust messaging constraints | Marketing Lead |
| **Legal / Compliance** | [Marketplace Mechanics — Compliance](../../product/marketplace-mechanics.md#compliance-verification), `legal/` docs | Legal Lead |

| Step | Actor | Action |
|------|-------|--------|
| 3.1 | New hire | Complete domain reading; note questions |
| 3.2 | Domain owner | 2-hour walkthrough session |
| 3.3 | New hire | Shadow live work where safe (trust roles: shadow queue review, no actions) |
| 3.4 | People Ops | End-of-week pulse check |

---

### Phase 4 — Week 2–4 — Systems & Certification

| Step | Actor | Action |
|------|-------|--------|
| 4.1 | IT + Security | Provision Tier-appropriate access per approved matrix |
| 4.2 | Trust Lead (Tier 2+) | Trust training: verification checklists, audit requirements, AI assist boundaries, escalation paths | 
| 4.3 | New hire (Tier 2+) | Pass trust certification quiz (≥ 90%) before queue access |
| 4.4 | Eng Lead (Tier 1+) | Staging environment setup; first PR (docs or low-risk fix encouraged) |
| 4.5 | New hire | Complete first supervised actions (trust: review case with supervisor co-sign) |
| 4.6 | Hiring Manager | Week 2 check-in — blockers, access gaps, goal adjustment |

**Trust certification covers:**

- Three-layer verification model (identity, kitchen, compliance)
- Approve / reject / request info with rationale
- AI flag review and dismissal documentation
- When to escalate ([Trust & Safety Escalation](trust-safety-escalation.md))
- PII handling in admin console
- Never auto-approve invariant

---

### Phase 5 — Day 30 — First Month Review

| Step | Actor | Action |
|------|-------|--------|
| 5.1 | Hiring Manager | 30-day review against goals: systems proficiency, culture fit, blockers |
| 5.2 | New hire | Self-assessment: what learned, what unclear, doc gaps found |
| 5.3 | People Ops | Collect onboarding feedback survey |
| 5.4 | Domain owner | Confirm certification complete (or remediation plan) |
| 5.5 | All | Update access tier if role scope changed |

---

### Phase 6 — Day 60 & 90 — Integration

| Milestone | Success signal |
|-----------|----------------|
| **Day 60** | Independent contribution on role core work; no outstanding access/training gaps |
| **Day 90** | Full productivity; new hire can orient others to their domain docs; onboarding feedback incorporated |

People Ops schedules 60- and 90-day manager reviews. Trust roles: supervisor audits first 20 cases for quality.

---

## Decision Points

| Decision | Owner | Options |
|----------|-------|---------|
| Grant Tier 2 admin access before background check complete | Security | Deny (default) · Exception with Founder approval |
| Trust certification failure | Trust Lead | Retrain · Role scope change · Offboarding |
| Expedited access for incident hire | Security + Trust Lead | Time-limited elevated access with supervisor co-sign on all actions |
| Remote vs. in-person onboarding track | People Ops | Adjust logistics; same access and training requirements |
| Buddy mismatch | Hiring Manager | Reassign buddy |

---

## Communication Templates

### Template: Pre-Start Welcome

**From:** People Ops  
**Timing:** T-7 days

```
Subject: Welcome to Marketplate — your first week

Hi [Name],

We're excited to have you join on [DATE] as [TITLE] on the [TEAM] team.

Day 1:
• [Time] — Orientation (Zoom link / office location)
• [Time] — 1:1 with [Manager name]
• [Time] — IT setup

Before you start, please read:
• Founding Constitution: [link]
• Company Values: [link]
• Product Overview: [link]

Your buddy is [Buddy name] — they'll reach out before Day 1.

Questions? Reply to this email.

— People Ops
```

### Template: Trust Training Assignment

**From:** Trust Lead  
**Timing:** T-1 (Tier 2 roles)

```
Subject: Trust & Safety certification — required before admin access

Hi [Name],

Your role requires access to verification and moderation tools. Before access is granted:

1. Complete the trust training module: [link]
2. Read: Trust Verification Flow, Trust Service security section, AI Platform overview
3. Pass certification quiz (≥ 90%)
4. Shadow [Supervisor name] for 2 supervised case reviews

Access will be provisioned after certification. Target: complete by end of Week 2.

— [Trust Lead name]
```

### Template: 30-Day Check-In Agenda

**From:** Hiring Manager

```
30-Day Check-In — [Name]

Agenda:
1. Progress on 30/60/90 goals
2. Systems and access — any gaps?
3. Documentation clarity — what was confusing?
4. Team integration and buddy feedback
5. Blockers and support needed
6. Adjust goals if needed
```

---

## Metrics

| Metric | Target | Owner |
|--------|--------|-------|
| Time to full access (Tier appropriate) | ≤ 10 business days | IT + Security |
| Trust certification pass rate (first attempt) | ≥ 80% | Trust Lead |
| Day 30 onboarding satisfaction (survey) | ≥ 4.5 / 5 | People Ops |
| Day 90 regrettable attrition | 0 | People Ops |
| Doc gap reports filed by new hires | Track; resolve within 14d | Doc owners |
| Supervised case audit pass rate (trust roles) | 100% first 20 cases | Trust Supervisor |

---

## Post-Incident / Retro

Run onboarding retro when:

- New hire with admin access causes trust incident within 90 days
- Background check delayed but access granted (process failure)
- Certification bypassed
- Repeated doc confusion from multiple new hires in same role

**Retro outputs:** Update this playbook, training modules, access matrix, or pre-start reading list.

---

## Related Documents

### Company
- [Founding Constitution](../../company/constitution.md)
- [Company Values](../../company/values.md)
- [Company Philosophy](../../company/company-philosophy.md)
- [Glossary](../../company/glossary.md)

### Product & trust
- [Product Overview](../../product/overview.md)
- [Marketplace Mechanics](../../product/marketplace-mechanics.md)
- [Trust Verification Flow](../../pages/flows/trust-verification-flow.md)

### Engineering
- [Engineering README](../../engineering/README.md)
- [Trust Service](../../engineering/services/trust-service.md)
- [AI Platform](../../ai/README.md)

### Standards & internal
- [docs/standards/](../standards/)
- [docs/internal/](../internal/)

### Related playbooks
- [Trust & Safety Escalation](trust-safety-escalation.md)
- [Launching a New Feature](launching-new-feature.md) — for engineers shipping first feature
