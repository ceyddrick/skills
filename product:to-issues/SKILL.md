---
description: Turn an approved PRD into execution-ready issues, sliced as vertical tracer bullets, validated through a quiz, then published in dependency order. Use after a PRD is written (companion to product-prd-write) and you need a backlog an agent or a dev can pick up and merge. Loads the PRD, proposes slices, gets sign-off, then creates the issues in your tracker.
allowed-tools: Read, Write
---

# Product to Issues

Convert an approved PRD into a set of issues that an agent or a developer can execute. Companion to `product-prd-write`: that skill produces the PRD, this one slices it into shippable work. Works with any issue tracker (Jira, Linear, GitHub Issues, etc.).

## Input

A PRD reference: a URL/title, a file path, or pasted text. If none given, ask. Read the full PRD before slicing. Note the target tracker and project (ask if unknown).

## Core principle — vertical tracer-bullet slices

Slice the PRD into **vertical tracer bullets**: each slice delivers a narrow but COMPLETE path through every layer it touches (data, API, UI, tests). Not horizontal layers (never "build the schema", then "build the API"). A slice must be independently mergeable and demonstrate one observable behavior end to end.

- Prefer MANY thin slices over FEW fat ones. When in doubt, split.
- The first slice is the thinnest walking skeleton that proves the path exists.
- Each later slice widens the path: one more behavior, one more case, one more persona.

## HITL vs AFK tag

Tag every slice:
- **AFK** (away from keyboard): can be specified, built, and merged with no human decision. Default. Prefer AFK.
- **HITL** (human in the loop): needs a human design call, judgment, or sign-off mid-flight (ambiguous UX, contested data model, business rule to confirm, security/compliance choice).

Push to make slices AFK. If a slice is HITL only because of one open question, consider extracting that decision into its own upstream HITL slice so the rest stays AFK.

## Workflow

### 1. Slice
Read the PRD. Map user stories and requirements to vertical slices. Order them by dependency (skeleton first, then widen). Assign each a type (Story / Task / Bug / Spike), a HITL/AFK tag, and its blockers.

### 2. Quiz (validate before creating anything)
Present the full slice list as a numbered table and ask for sign-off. Do NOT create any issue until the user approves.

| # | Title | Type | Tag | Blocked by | User stories covered |
|---|-------|------|-----|------------|----------------------|

Then ask explicitly:
- Granularity OK, or should any slice be split / merged?
- Dependencies correct?
- HITL/AFK tags right?
- Anything missing or out of scope?

Iterate on the table until the user approves. This loop is the point of the skill — do not skip it.

### 3. Publish to the tracker
Once approved, create issues **in dependency order** (a blocker exists before the issue that links to it). For each issue:
- Build the body from the issue template below.
- Create it with the agreed type.
- Set "Blocked by" links once both issues exist.
- Tag HITL/AFK via a label.

Return the created issue keys and URLs, listed in dependency order.

## Issue contents

Every issue follows this template:
- **Parent** — epic or PRD link
- **What to build** — the behavior this slice delivers, end to end
- **Acceptance criteria** — checkbox list, BEHAVIORAL (what the system does), not procedural (how to code it)
- **Blocked by** — upstream issue keys

## Durability rule

Issues must not rot. So:
- NO file paths and NO code snippets in issues. They go stale the moment code moves.
- ONE exception: a trimmed snippet from a prototype that ENCODES A DECISION (a state machine, a schema, a type signature). Keep it minimal and label it as the decision it captures, not as implementation.
- Describe behavior and outcomes, not the current shape of the codebase.

## Rules

- Never create issues before the quiz is approved.
- One observable behavior per slice; if a slice has "and" in its goal, split it.
- Acceptance criteria are testable and behavioral. "User sees X after Y", not "add field to table".
- Default to AFK; justify every HITL.
- Don't invent scope. If the PRD is silent on something needed to slice, flag it as an open question in the quiz, don't guess.
