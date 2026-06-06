---
description: Review a press release or op-ed with structured critique, attractiveness scoring, competitive benchmarking via web search, and a proposed rewrite. Use when the user shares a press release, PR draft, or tribune for professional review.
allowed-tools: Read, Write, Edit, WebSearch, WebFetch, Glob
---

# Press Release & Op-Ed Review

> Apply solid copy fundamentals throughout: headline, tone, and proof-framing standards. This skill's specialty is the PR workflow: web competitive benchmark and a full rewrite.

Review press releases (communiques de presse), op-eds (tribunes), and media-facing professional texts. Produce a structured critique, score the content, benchmark against comparable publications, and deliver a rewritten version.

## Input handling

Two input modes:

### Mode 1: File path provided
- Read the .md file
- Append all output as a new `## Revue PR` section at the end of the document
- Do NOT modify the original text above

### Mode 2: Raw text (copy-paste)
- Create a new file: `YYYY-MM-DD - PR Review - {short title}.md` in the working directory
- Include the original text under `## Texte original`
- Add the review below

## Review workflow

### Step 1: Context extraction

Before anything, identify and state:
- **Type**: press release (CP), op-ed (tribune), announcement, product launch, partnership, etc.
- **Issuer**: who is publishing this (company, person, org)
- **Target audience**: journalists, industry analysts, general public, B2B
- **Core message**: the single sentence this text wants to land
- **5W+H check**: Who, What, When, Where, Why, How — flag any missing

### Step 2: Critique

Two sections, no fluff:

**Strengths** (2-4 bullet points)
- What works, what's effective, what a journalist would pick up
- Cite specific passages

**Weaknesses** (2-4 bullet points)
- What's vague, generic, or AI-sounding
- Missing data, unsupported claims, buried lede
- Structural issues (inverted pyramid violated, no hook, weak headline)
- Cite specific passages

### Step 3: Attractiveness scoring

Score each dimension from 1 to 5. Display as a table.

| Dimension | Score | Comment |
|-----------|-------|---------|
| **Headline** | /5 | Does it grab attention? Would a journalist click? |
| **News value** | /5 | Is there actual news here? Timeliness, impact, novelty |
| **Data density** | /5 | Concrete numbers, facts, quotes vs. vague claims |
| **Readability** | /5 | Can a non-expert follow? Is the structure logical? |
| **Quotability** | /5 | Are there ready-made quotes a journalist would use? |
| **Overall** | /5 | Would this get picked up by press? |

### Step 4: Competitive benchmark

Use WebSearch to find:
- 2-3 recent press releases on the same topic or from competitors
- Current news coverage of the subject area
- What angle journalists are currently taking on this topic

Summarize findings in 5-10 lines:
- What others are saying on this topic
- What angle is overused vs. underexplored
- How this CP positions itself relative to the current conversation

### Step 5: Rewritten version

Produce a complete rewrite applying:
- **Inverted pyramid**: most newsworthy info first
- **Strong headline**: factual, specific, no corporate jargon
- **Dense lead**: answer 5W+H in the first paragraph
- **Data over adjectives**: replace "significant growth" with "42% growth"
- **Quotable pull quote**: one strong quote from a spokesperson, written to be copy-pasted by journalists
- **Boilerplate**: clean company description at the end

### Step 6: Diff summary

3-5 short annotations explaining the most impactful changes between original and rewrite, tied to specific improvements.

## Style rules

### Never do this
- Em dashes or en dashes
- "Leader de...", "solution innovante", "fort de son expertise"
- "Nous sommes fiers de...", "Nous avons le plaisir de..."
- "Dans un monde en constante evolution..."
- Any sentence that contains zero information
- Corporate buzzword bingo: "synergie", "disruption", "paradigme", "ecosysteme"

### Always do this
- Write like a sharp communications director, not like an AI
- French output (unless the original is in English)
- Numbers and data wherever possible
- Short paragraphs (3-4 lines max)
- Active voice
- If information is missing and would strengthen the CP, flag it explicitly as "[A COMPLETER: ...]"
