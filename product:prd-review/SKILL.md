---
description: Review a PRD as a product leader, producing a structured critique with gaps, competitive context, usage data, risks, and questions for the meeting. Use when preparing to review or discuss a PRD.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, WebSearch, WebFetch
---

# PRD Review

Read a PRD and produce a structured product-leader review. The output is a standalone note that can be linked from a meeting note.

**Scope**: `product-prd-review` = critique of a PRD. For a slide deck, a stakeholder email, or a roadmap, use a different review skill.

## Input

A PRD reference as argument: a URL, a doc ID, a file path, or pasted text. If no argument: ask which PRD to review.

## Workflow

### 1. Fetch the PRD

Retrieve the full content. Extract:
- Product/feature name
- Author
- Date
- The full PRD content

### 2. Structural analysis

Evaluate the PRD against this checklist. For each item, note: present/missing/incomplete.

**Problem & context**
- [ ] Problem clearly defined with evidence (not just "customers want X")
- [ ] Target user/persona identified (which buyer? which end-user?)
- [ ] Current state documented (how is this handled today?)
- [ ] Quantified impact of the problem (support tickets, churn, lost revenue, workarounds)

**Commercial & coherence lens**
- [ ] Buyer/user impact: will the target audience understand, adopt, and support this?
- [ ] Pricing/packaging model defined or referenced
- [ ] Go-to-market enablement: communication and training (support, sales)
- [ ] Catalog fit + impact on existing modules
- [ ] UX/design coherence with existing product patterns; new vs modified user flows
- [ ] Feature flag / rollout strategy defined?

**Success criteria**
- [ ] Measurable success metrics defined (not just "increase satisfaction")
- [ ] Baseline values provided for comparison
- [ ] Timeline for measurement

**Technical**
- [ ] Dependencies on other teams/services identified
- [ ] Data model implications noted
- [ ] Performance/scale considerations addressed
- [ ] Security implications assessed

**Risks & edge cases**
- [ ] Risks explicitly listed with mitigation
- [ ] Edge cases considered (multi-country, legacy accounts, migration)

### 2bis. Two-axis review (do not merge)

Review along two independent axes:
- **Form / conformance** = the structural checklist above (template respected, sections present, consistent with the team's product standards and PRD conventions).
- **Substance** = does the PRD solve the real product/business problem, for the right user, at the right time, regardless of how well it's written?

Report both verdicts separately. The verdict in step 6 weighs both but keeps the two reads visible.

### 3. Knowledge gaps

List what the PRD does NOT address but should. Frame as questions to ask in the meeting, not as criticisms. Categorize:
- **Must answer before dev**: blockers
- **Should clarify**: important but not blockers
- **Nice to know**: context that would strengthen the PRD

### 4. Contextual research (mini-intel)

Run targeted research to arm the review with data:

**Internal data** — if the PRD touches an existing module:
- Current usage volumes for the module
- Trend (growing, stable, declining)
- Any active alerts or SLO issues

Note: pulling product analytics may require API keys. If not available in the session, skip and note "Analytics data not available — run manually if needed."

**Existing docs** — search the team's wiki or knowledge base for:
- Previous PRDs on the same topic or module
- Architecture decisions, tech specs
- Past meeting notes mentioning this feature

**Competitors** — check how direct competitors handle this feature/need and whether it's table stakes or differentiation.

**Web** — if relevant:
- Industry benchmarks or standards for this type of feature
- Competitor public announcements

**Notes** — search your own notes for related context

### 5. Risk assessment

Identify the top risks, categorized:
- **Commercial**: will users adopt? Does it cannibalize existing revenue?
- **Technical**: complexity, dependencies, performance
- **Coherence**: does this fragment the product experience?
- **Timing**: is this the right moment? What else is competing for attention?
- **Support**: will this increase or decrease support load?

### 6. Verdict

Provide a clear assessment:
- **Go**: PRD is solid, proceed to dev
- **Go with reserves**: proceed but X must be addressed first
- **Needs rework**: fundamental gaps, send back to PM with specific asks
- **No-go**: wrong problem, wrong timing, or wrong approach — explain why

Always justify with specific references to the PRD content and the research.

### 7. Questions for the meeting

List 5-7 prioritized questions to ask in the PRD review meeting. For each:
- The question itself
- Why it matters (one line)
- Who should answer (PM, tech lead, support, commercial)

## Output

Create a self-contained file with the following format:

**Filename**: `YYYY-MM-DD - PRD Review - [Product Name].md`

**Structure**:
```markdown
# PRD Review — [Product Name]

Source: [PRD title](URL)
Author: [Name] | PRD date: [date]

## Verdict

[Go / Go with reserves / Needs rework / No-go]
[2-3 lines justification]

## Two-axis review

### Form / conformance: [solid / ok / weak]
[Does the PRD respect the template, format, product standards? 1-2 lines.]

### Substance: [solid / ok / weak]
[Does it solve the real product/business problem? Is it the right thing to build? 1-2 lines.]

## Structural analysis

[Checklist results grouped by category, with status and comments for each item]

## Knowledge gaps

### Blockers
- [question]

### To clarify
- [question]

### Nice to know
- [question]

## Context & data

### Internal data
- [Analytics / docs findings]

### Competition
- [How competitors handle this]

### Market
- [Web research findings if relevant]

## Risks

| Risk | Type | Severity | Proposed mitigation |
|------|------|----------|---------------------|
| ... | Commercial/Tech/Coherence/Timing/Support | High/Medium/Low | ... |

## Questions for the meeting

1. **[Question]**
   Stakes: [why it matters] — Ask: [who]

2. ...
```

## Rules

- Be direct and critical. A useful review is honest, not diplomatic.
- Every criticism must be specific: quote the PRD, point to what's missing, explain why it matters.
- Never fabricate data. If you can't find competitive intel or usage data, say so.
- The verdict must be justified by the analysis, not by gut feeling.
- Keep the output dense. No filler, no AI slop.
- The review file must be self-contained and linkable from a meeting note.
