---
description: Score any content (copy, landing page, email, strategy, visual) with an auto-assembled panel of 7-10 simulated experts. Iterates until score >= 90/100 (max 3 rounds). Use when you need rigorous, multi-perspective quality scoring before shipping.
allowed-tools: Read, Write, Edit, Glob, Grep, WebFetch
argument-hint: "<text, file path, or URL> [content type]"
---

# Expert Panel — Iterative Multi-Expert Scoring

Takes any content and scores it through a panel of simulated domain experts. Loops until the score hits 90+ or 3 rounds are exhausted. The humanizer expert is always included at 1.5x weight.

## Input

Accept content in any of these forms:
- Pasted directly as the argument
- A file path -> read the file
- A URL -> fetch the content
- Content type hint (optional): landing-page, email, social-post, article, pr, strategy, ad-copy

If no content type is specified, infer from the content itself.

## Step 1: Intake

Identify:
- **Content type**: what are we scoring?
- **Goal**: what should this content achieve?
- **Audience**: who reads this?
- **Context**: any constraints (brand voice, platform limits, regulations)?

State these in 4 lines max before proceeding.

## Step 2: Auto-Assemble the Panel

Select 7-10 experts based on content type and domain. Always include:

1. **Humanizer** (mandatory, weight 1.5x) -- Detects AI writing patterns. Scores how human the text sounds. Uses the 24-pattern detection framework from writing:unslop.
2. **Brand Voice Match** (mandatory) -- Does this sound like the brand/person, or like generic AI output?

Then add 5-8 domain experts from the pre-built panels below.

### Landing Page
- Conversion Rate Optimizer (CTA, friction, clarity)
- Headline Specialist (hook, specificity, scroll-stopping)
- Social Proof Analyst (trust signals, testimonials, credibility)
- UX/Mobile Expert (readability, hierarchy, mobile rendering)
- Competitive Positioning Expert (differentiation, unique value)

### Email (onboarding, newsletter, campaign)
- Subject Line Specialist (open rate, curiosity, relevance)
- Email Deliverability Expert (spam signals, formatting, length)
- Copywriter (flow, tone, CTA placement)
- Audience Empathy Expert (relevance to reader, pain points)
- Retention Strategist (nurture sequence logic, timing)

### Social Post (X, LinkedIn)
- Platform Algorithm Expert (format, timing, engagement signals)
- Hook Specialist (first line, scroll-stopping power)
- Audience Growth Expert (shareability, quote-worthiness)
- Authenticity Analyst (does it sound like a person or a brand?)

### Article / Blog
- Editor (structure, flow, argument strength)
- SEO Analyst (keyword relevance, search intent match)
- Reader Engagement Expert (hook, readability, value density)
- Subject Matter Expert (accuracy, depth, credibility)

### PR / Communications
- Journalist Perspective (would I cover this? is there news value?)
- Headline Analyst (click-worthiness, specificity)
- Data Density Expert (facts vs. fluff ratio)
- Crisis/Risk Reviewer (could this backfire?)

### Strategy / Business
- Data Foundation Expert (are claims data-backed?)
- ROI Analyst (is the business case clear?)
- Risk Assessor (what could go wrong?)
- Actionability Expert (can someone execute this tomorrow?)

For domains not listed above, assemble a panel using this principle:
- 3-4 craft experts (how to make good content of this type)
- 2-3 domain experts (the specific market/audience/subject)
- Humanizer (always)
- Brand Voice Match (always)
- Cap at 10, merge overlapping roles

## Step 3: Select Scoring Rubric

Choose the rubric based on content type. Each has 4 dimensions worth 0-25 points (total 0-100):

### Content Quality (articles, social posts, newsletters)
| Dimension | 0-25 | What it measures |
|-----------|------|-----------------|
| Hook Power | /25 | Does the opening stop scrolling? Curiosity gap? Tension? |
| Voice Authenticity | /25 | Does this sound like a human with opinions? Or like AI? |
| Value Density | /25 | Information-to-word ratio. Every sentence earns its place? |
| Engagement Potential | /25 | Would someone share, reply, or save this? |

### Conversion Quality (landing pages, emails, ads, CTAs)
| Dimension | 0-25 | What it measures |
|-----------|------|-----------------|
| Headline/Hero | /25 | Clarity, specificity, relevance to target audience |
| Clarity & Friction | /25 | Can someone understand and act in under 10 seconds? |
| Social Proof & Trust | /25 | Credibility signals, testimonials, trust badges |
| CTA Strength | /25 | Clear, compelling, low-friction call to action |

### Strategic Quality (strategies, plans, briefs)
| Dimension | 0-25 | What it measures |
|-----------|------|-----------------|
| Data Foundation | /25 | Claims backed by specific data, not vibes |
| Actionability | /25 | Can someone execute this tomorrow? |
| ROI Clarity | /25 | Is the business case obvious? |
| Risk Assessment | /25 | Are failure modes identified? |

### Evaluation Quality (reviews, audits, assessments)
| Dimension | 0-25 | What it measures |
|-----------|------|-----------------|
| Evidence Quality | /25 | Specific examples, not vague impressions |
| Criteria Relevance | /25 | Are we measuring what matters? |
| Risk Assessment | /25 | Blind spots identified? |
| Actionability | /25 | Clear next steps with priority? |

## Step 4: Score (Recursive Loop)

### Round structure

For each round, produce:

1. **Expert scores table**:

| Expert | Score | Key feedback (1 line) |
|--------|-------|-----------------------|
| Humanizer (1.5x) | XX/100 | ... |
| Brand Voice Match | XX/100 | ... |
| [Expert 3] | XX/100 | ... |

2. **Rubric scores**: the 4-dimension breakdown

3. **Weighted aggregate**: average of all expert scores (humanizer counted at 1.5x weight)

4. **Top 3 weaknesses**: ranked, with specific fix suggestions

5. **If score < 90**: revise the content addressing the top 3 weaknesses, then run the next round

6. **If score >= 90**: finalize

### Scoring rules
- Scores must be brutally honest. No padding to reach 90.
- First round scores are typically 55-75. That's normal.
- Each round should show measurable improvement on the identified weaknesses.
- Max 3 rounds. If still under 90 after round 3, ship with the best version and note remaining issues.
- The humanizer score gates everything: if humanizer < 80, the content does not ship regardless of aggregate score.

### Quality gates
- < 70: Do not ship. Major rewrite needed.
- 70-79: Shippable with caveats. Note what's weak.
- 80-89: Good. Minor polish possible but not blocking.
- 90+: Ship with confidence.

## Step 5: Output

```
---
**Content type**: [type]
**Panel**: [list of expert names]
**Rubric**: [which rubric used]
**Final score**: XX/100 (after N rounds)

### Rubric breakdown
| Dimension | Score |
|-----------|-------|
| ... | /25 |
| ... | /25 |
| ... | /25 |
| ... | /25 |

### Round history
[Round 1: XX/100 -> top issues -> Round 2: XX/100 -> ...]

### Expert verdicts (final round)
| Expert | Score | Verdict |
|--------|-------|---------|
| ... | ... | ... |

---

[The final scored/revised content]

---

### Remaining issues (if score < 90)
- [what's still weak and why]
```

## Step 6: Feedback-to-Source

When scoring content produced by another skill (e.g., mktg:copy-optimize output, writing:xpost draft):
- Generate a 3-5 line improvement brief that the source skill can use
- Format: "To improve: [specific change]. Because: [expert rationale]."

## Memory: Learned Patterns

After each scoring session, if the user approves or rejects the final output, note the pattern in `~/.claude/skills/mktg:expert-panel/patterns.md`

Format:
```
## [Pattern Name]
- **Type:** approval | rejection
- **Content types:** [which types]
- **Rule:** [what to always/never do]
- **Date:** [YYYY-MM-DD]
```
