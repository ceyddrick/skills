---
description: Optimize any marketing copy (headline, CTA, email, landing section) through iterative variant generation and expert scoring. Generates 10+ variants per round, scores by 5 personas, evolves the best. Use when you need to find the best version of a piece of copy.
allowed-tools: Read, Write, Edit, WebFetch, WebSearch
argument-hint: "<copy to optimize> [type: headline|cta|email|landing|ad]"
---

# Copy Optimize — Iterative Variant Generation

Takes a piece of marketing copy and evolves it through multiple rounds of variant generation, expert scoring, and cross-breeding. Inspired by the autoresearch pattern applied to copywriting.

> Apply solid copy fundamentals throughout (strong first sentence, action-specific CTAs, honest social-proof framing, platform constraints), and avoid AI slop (banned filler words, generic phrasing). The iterative variant-generation mechanic below is this skill's own specialty.

## Input

Accept copy in any of these forms:
- Pasted directly as the argument
- A file path -> read the file
- A URL -> fetch the relevant section
- Copy type hint (optional): headline, cta, email, landing-section, ad-copy, onboarding

If no type is specified, infer from the content.

## Step 1: Analyze the Original

Before generating anything, understand:
- **What type of copy is this?** (headline, CTA, email subject, body, landing hero, ad, etc.)
- **What's the goal?** (click, signup, read more, share, buy)
- **Who's the audience?** (early adopter, casual user, power user, journalist, etc.)
- **What's the current approach?** (feature-led, benefit-led, emotion-led, curiosity-led)
- **What's working already?** (don't throw away what's good)
- **What's weak?** (vague value prop, generic language, no hook, wrong tone)

State this analysis in 6 lines max.

## Step 2: Generate Variants (Round 1)

Generate **10 variants** using different angles:

| Variant | Angle | Description |
|---------|-------|-------------|
| 1-2 | **Benefit-first** | Lead with the outcome for the user |
| 3-4 | **Problem-first** | Lead with the pain point being solved |
| 5-6 | **Curiosity/intrigue** | Create an information gap |
| 7-8 | **Social proof** | Lead with what others are doing |
| 9 | **Contrarian** | Challenge a common assumption |
| 10 | **Wildcard** | Unexpected angle, humor, or format break |

Rules for variants:
- Each must feel genuinely different, not just a rewording
- Match the tone and register of the brand
- Respect platform constraints (character limits, format)
- No AI slop: avoid banned filler words and generic phrasing
- Be specific: numbers, outcomes, concrete details over vague promises

## Step 3: Score Variants

> The 5-persona scoring below is lightweight and tuned for ranking many variants fast — that is this skill's specialty.

Score each variant using **5 personas**. The first 2 are assembled dynamically based on the product/audience context. The last 3 are universal.

### The Panel

**Assemble personas 1 and 2 from the project context:**

1. **The Power User** — Someone who already uses competing products in this space. Adapt to the domain: for a SaaS tool, this is the expert user who knows alternatives; for a consumer app, the early adopter who's tried everything.
   - Scoring lens: "Is this different enough from what I already use? Does it respect my intelligence?"
   - Red flags: feature lists without differentiation, "yet another" feel, dumbed-down language

2. **The Newcomer** — Someone unfamiliar with the product category. They don't know the jargon, don't understand why they'd switch from their current behavior.
   - Scoring lens: "Do I understand what this is in 3 seconds? Why should I care?"
   - Red flags: jargon, assumed knowledge, no clear benefit stated

**Universal personas (always the same):**

3. **The Skeptical Copywriter** (has seen 10,000 landing pages, immune to hype)
   - Scoring lens: "Is this specific or generic? Would this work for any product or only this one?"
   - Red flags: interchangeable copy, buzzwords, no proof, weak CTAs

4. **The CRO Expert** (conversion rate optimizer, thinks in funnels)
   - Scoring lens: "Does this reduce friction? Is the value prop clear? Would I click?"
   - Red flags: multiple messages competing, unclear next step, feature overload

5. **The Brand Builder** (thinks long-term, cares about positioning and memorability)
   - Scoring lens: "Does this create a distinct brand impression? Would someone remember this?"
   - Red flags: generic positioning, copycat vibes, no personality

When assembling the panel, name the Power User and Newcomer specifically based on the product context (e.g., "Feedly power user" and "Casual phone reader" for an RSS app, or "Figma daily user" and "First-time design tool user" for a design tool).

### Scoring dimensions (by copy type)

**Headlines / CTAs**:
- Clarity (0-25): Can someone understand this in under 3 seconds?
- Desire (0-25): Does this make someone want the thing?
- Differentiation (0-25): Could only THIS product say this?
- Memorability (0-25): Would someone remember this tomorrow?

**Emails**:
- Open-worthiness (0-25): Would you open this subject line?
- Value density (0-25): Information-to-word ratio in the body
- Flow (0-25): Does it lead naturally to the CTA?
- Authenticity (0-25): Does this sound like a person wrote it?

**Landing sections**:
- Hook power (0-25): Does the opening stop scrolling?
- Clarity (0-25): Value prop clear in 5 seconds?
- Proof (0-25): Evidence backing the claims?
- Action (0-25): Clear, compelling next step?

**Ad copy**:
- Scroll-stop (0-25): Would this stop someone mid-scroll?
- Relevance (0-25): Does target audience see themselves?
- Urgency (0-25): Is there a reason to act now?
- Click-worthiness (0-25): Compelling enough to click?

### Scoring output

```
| # | Variant (first 50 chars...) | Power User | Newcomer | Copywriter | CRO | Brand | Avg |
|---|---------------------------|------------|----------|------------|-----|-------|-----|
| 1 | "..." | 72 | 85 | 68 | 80 | 75 | 76 |
```

## Step 4: Evolve (Round 2)

Take the **top 3 variants** from Round 1. For each:
- Identify what scored highest per persona
- Combine the strongest elements
- Generate 3 evolved versions per winner (9 total)
- Add 1 new wildcard

Score the 10 new variants with the same panel.

## Step 5: Cross-Breed (Final Round)

Take the winning elements across all rounds:
- Best hook/opening
- Best value proposition framing
- Best CTA/close
- Best tone/voice

Combine them into **5 final candidates**. Score one last time.

## Step 6: Output

```
---
## Copy Optimization Report

**Original**: "[the original copy]"
**Type**: [copy type]
**Audience**: [target audience]

### Winner
**Score**: XX/100
**Copy**: "[the winning variant]"

### Why it won
[2-3 lines: what makes this the strongest option, which personas scored it highest and why]

### Runner-up options
1. **Score XX/100**: "[variant]"
2. **Score XX/100**: "[variant]"

### Evolution history
- Round 1: 10 variants -> top 3 (scores: XX, XX, XX)
- Round 2: 10 evolved variants -> top 3 (scores: XX, XX, XX)
- Final: 5 cross-bred -> winner (score: XX)

### Per-persona verdict (winner)
| Persona | Score | Verdict (1 line) |
|---------|-------|-------------------|
| Power User | XX | ... |
| Newcomer | XX | ... |
| Copywriter | XX | ... |
| CRO Expert | XX | ... |
| Brand Builder | XX | ... |

### Dimension breakdown (winner)
| Dimension | Score |
|-----------|-------|
| ... | /25 |
| ... | /25 |
| ... | /25 |
| ... | /25 |
---
```

## Quality Gates

- **< 70**: Don't ship. The copy needs a fundamentally different approach.
- **70-79**: Shippable but not great. Consider more iterations or a different angle.
- **80-84**: Good. Ship it, test it, iterate based on real data.
- **85-89**: Strong. Ship with confidence.
- **90+**: Exceptional. Rare. Ship and study what made it work.

## Anti-patterns

- Don't generate 10 variants that are just rewordings of the same angle
- Don't over-optimize for one persona at the expense of others
- Don't sacrifice clarity for cleverness
- Don't ignore what was already working in the original
- Don't produce generic copy that could apply to any product
- Don't exceed 3 rounds of evolution (diminishing returns)
- Don't score your own output generously. Be harsh.

## Project context

When used within a project that has a CLAUDE.md or brand brief, read those files to extract:
- **Audience**: who is the target user?
- **Positioning**: how does the product differentiate?
- **Tone**: what voice/register does the brand use?
- **Differentiators**: what makes this product unique?
- **Avoid**: words/phrases the brand never uses

These inform the Power User and Newcomer personas, the variant angles, and the scoring criteria. If no project context is available, ask the user for these 5 points before generating variants.
