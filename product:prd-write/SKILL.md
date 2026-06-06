---
description: Write a structured PRD from scratch through guided discovery. Runs an interactive workflow (problem → personas → solution → metrics → stories), then outputs a publishable document or a draft. Use when starting a new feature, module, or product initiative. Companion to product-prd-review.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, WebSearch, WebFetch
---

# PRD Write

Write a new PRD for a product, feature, or platform initiative through guided discovery. The skill drives a multi-phase conversation, anchors the document in your product context, and produces a publishable PRD or a draft.

## When to use

- Starting a new feature or module
- Reworking or replatforming an existing product
- Scoping a new platform initiative before kicking off design or dev
- Drafting a PRD before a leadership or product review

For reviewing an existing PRD, use `product-prd-review` instead.

## Input

A subject line as argument, e.g. "billing module rework", "new onboarding flow". If no argument: ask what the PRD is about.

Optional follow-up flags from the user:
- "from [URL]" → seed from an existing draft or brief
- "draft only" → output a local draft, do not publish
- "express" → run a condensed version (skip phases 2 and 5)

## Workflow

### Phase 1 — Frame the project

Ask the user, one question at a time when needed, otherwise group into a single message:

1. **One-liner**: in one sentence, what is this project?
2. **Trigger**: why now? (commercial pressure, competitive threat, user pain, technical debt, regulation)
3. **Scope hint**: feature, module, platform, full rework?
4. **Stakeholders**: who is the sponsor? Who decides go/no-go?
5. **Deadline or window**: any hard date (review, event, contract)?

Capture the answers as working notes. If the user is vague, push back once with a concrete prompt; do not loop.

### Phase 2 — Load context

Read whatever product context the user can provide and keep it in working memory for the rest of the session. Skip in `express` mode.

- Company and product overview
- Product portfolio and modules
- Catalog or pricing reference
- Competitive landscape
- Team structure (sponsor, owners)

Search for prior art in the user's existing docs (wiki, knowledge base, notes): existing PRDs, briefs, post-mortems, or decisions touching the same module or flow.

If existing PRDs are found, read them. Decide: extend, replace, or fork. Tell the user what you found and confirm direction.

### Phase 3 — Discovery (interactive)

Run a structured discovery dialog. Ask focused questions, group when possible. Stop when each section has enough material.

**Grill mode (optional)**: by default, batch questions as above. Switch to grill mode when the user asks for it or when a section is hard (fuzzy problem, contested scope, ambiguous personas). In grill mode:
- Ask one question at a time, wait for the answer before the next.
- Always propose your own recommended answer with each question.
- Walk the decision tree by dependency (each answer opens the next branch), not the checklist in order.
- If the answer already exists in loaded context or docs, use it instead of asking.
- Actively challenge the loaded references: point out contradictions.
- Invent 2-3 edge scenarios to force precision on concept boundaries.

**3.1 Problem statement**
- What is the customer problem? Who feels it?
- What evidence do we have? (tickets, churn, NPS, sales feedback, lost deals, support load)
- How is it handled today? (workaround, manual ops, missing entirely)
- Quantified impact if known

**3.2 Personas**
Identify every layer the product touches:
- **Buyer / decision-maker persona**: who pays or signs off?
- **End-user persona**: who actually uses it day to day?
- **Internal user**: support, sales, ops — if applicable

**3.3 Goals and non-goals**
- 3 to 5 outcome goals (not features)
- Explicit non-goals: what we will NOT do in this scope

**3.4 Solution direction**
- High-level approach (not detailed design yet)
- Alternatives considered and why rejected
- Key design principles

**3.5 Success metrics**
Pick the framework that fits:
- **NSM** (North Star Metric) for platform or business-level initiatives
- **AARRR** for adoption funnels
- **HEART** for UX or engagement focus
- **OKR** for strategic alignment

Always include:
- A leading indicator (early signal, weeks)
- A lagging indicator (real outcome, quarters)
- Baseline value if available

**3.6 User stories**
- 3 to 8 core stories in `As a [persona], I want [action], so that [outcome]` format
- Mark each: must / should / could

### Phase 4 — Draft the PRD

Write the PRD using the structure below. Be dense, factual, no filler.

```markdown
# PRD — [Product / Feature Name]

**Author**: [Name]
**Status**: Draft / In review / Approved
**Date**: YYYY-MM-DD
**Sponsor**: [Name]
**Target date**: [date or quarter]

## 1. Executive summary
[3 to 5 lines. Problem, proposed solution, expected outcome, why now.]

## 2. Context and problem
### Problem
[What is broken, for whom, with evidence]

### Current state
[How it works today, why it's insufficient]

### Why now
[Trigger: commercial, competitive, technical, regulatory]

## 3. Personas
### Buyer / decision-maker
[Type, size, maturity, role in the flow]

### End-user
[Profile, context, expectations]

### Internal user (if applicable)
[Support, sales, ops]

## 4. Objectives
### Goals (outcomes)
- [Outcome 1]
- [Outcome 2]
- [Outcome 3]

### Non-goals
- [What we explicitly do NOT cover]

## 5. Solution
### Overview
[High-level approach]

### Design principles
- [Principle 1]
- [Principle 2]

### Alternatives considered
| Option | Pros | Cons | Verdict |
|--------|------|------|---------|
| ... | ... | ... | ... |

## 6. User stories
| # | Persona | Story | Priority |
|---|---------|-------|----------|
| US-1 | ... | As a... I want... so that... | Must |

## 7. Requirements
### Must
- [REQ-M-1] ...

### Should
- [REQ-S-1] ...

### Could
- [REQ-C-1] ...

## 8. Success metrics
### Framework
[NSM / AARRR / HEART / OKR + rationale]

### Indicators
| Metric | Type | Baseline | Target | Horizon |
|--------|------|----------|--------|---------|
| ... | Leading/Lagging | ... | ... | ... |

## 9. UX / Design
[Principles, key flows, references to mockups if any. Not detailed mockups.]

## 10. Technical considerations
- **Architecture**: [services impacted]
- **Data**: [model, migration, retention]
- **Performance / scale**: [SLO, expected load]
- **Security**: [auth, data classification, compliance]
- **Dependencies**: [teams, services, vendors]

## 11. Product / catalog fit
- **Module**: [where it sits in the product]
- **Pricing / packaging**: [model]
- **Impact on existing modules**: [list]

## 12. Go-to-market enablement
- **Communication**: [channels]
- **Training**: [support team, sales]
- **Documentation**: [help center articles, sales kit]

## 13. Rollout
- **Phase 1 — Beta**: [scope, users, duration]
- **Phase 2 — GA**: [criteria to ship]
- **Feature flag**: [yes/no, scope]
- **Rollback plan**: [how to pull back]

## 14. Risks
| Risk | Type | Severity | Mitigation |
|------|------|----------|------------|
| ... | Commercial/Tech/Coherence/Timing/Support | High/Medium/Low | ... |

## 15. Dependencies and assumptions
### Dependencies
- [team, service, decision]

### Assumptions
- [assumption + how we'll validate it]

## 16. Open questions
- [Question + owner + due date]

## 17. Timeline and milestones
| Milestone | Target date | Owner |
|-----------|-------------|-------|
| Kickoff | ... | ... |
| Design freeze | ... | ... |
| Beta | ... | ... |
| GA | ... | ... |
```

### Phase 5 — Validate

Before publishing, run a self-check on the draft. Skip in `express` mode.

**Quality gates**:
- [ ] Problem is described with evidence, not anecdote
- [ ] All relevant personas are explicit (buyer, end-user, internal)
- [ ] Non-goals are listed
- [ ] At least one leading and one lagging metric, with baseline if available
- [ ] Product and pricing fit is covered
- [ ] Risks are scored, not just listed
- [ ] Open questions have owners and due dates

If 3+ gates fail, loop back to phase 3 with the user on the gaps.

**Pre-mortem** (recommended for high-stakes projects):
Before locking the PRD, run a pre-mortem. Prompt yourself: "Assume this project has failed 6 months after launch. Write the post-mortem as if it already happened. List the top 3 most likely failure reasons, ordered by probability. Be specific and brutal — not generic risks but this project's real blind spots." Surface hidden assumptions and second-order effects. Feed the output back into section 14 (Risks) and section 15 (Assumptions), and flag anything new as an open question.

### Phase 6 — Publish

Ask the user where to publish:

1. **Team wiki / knowledge base** (default for finalized PRDs)
   - Title format: `PRD — [Product Name]`
   - Return the URL

2. **Local draft** (for early WIP or `draft only`)
   - Filename: `YYYY-MM-DD - PRD - [Product Name].md`

3. **Both** — common case for projects that need iteration

After publishing, suggest next steps:
- Run `product-prd-review` on the freshly published PRD for a second pass
- Open a tracking epic linked to the PRD
- Schedule the kickoff or product review

## Rules

- Be direct and dense. No filler, no AI slop.
- Never invent data. If a metric, baseline, or competitive insight is missing, mark it as an open question.
- A PRD is a contract for alignment, not a creative essay. Brevity wins.
- If a section has nothing meaningful to say, write "TBD" with an owner and a date, not filler.
- Quote real signals when available (analytics, existing docs, customer feedback).
- Stop and ask the user when a strategic call is needed (scope, sponsor, priority). Do not guess.
