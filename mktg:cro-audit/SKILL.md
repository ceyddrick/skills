---
description: Audit a landing page or web page on 8 conversion dimensions (headline, CTA, social proof, urgency, trust, friction, mobile, speed). Produces a scored report with prioritized fixes. Use before launching or when conversion is underperforming.
allowed-tools: Read, Write, WebFetch, Bash, mcp__chrome-devtools__take_screenshot, mcp__chrome-devtools__navigate_page, mcp__chrome-devtools__evaluate_script, mcp__chrome-devtools__lighthouse_audit, mcp__chrome-devtools__take_snapshot, mcp__chrome-devtools__resize_page
argument-hint: "<URL to audit>"
---

# CRO Audit — Landing Page Conversion Scoring

Scores a web page on 8 conversion dimensions. Produces a grade (A+ to F), prioritized fixes, and benchmark comparisons.

## Input

- A URL (required)
- Optional: industry context for benchmark comparison (SaaS, ecommerce, media, consumer app)
- If no URL provided, ask for one

## Step 1: Capture the Page

Use the available tools to analyze the page:

1. **Navigate** to the URL and take a screenshot (desktop + mobile viewport)
2. **Fetch** the HTML content via WebFetch for text analysis
3. If Chrome DevTools MCP is available:
   - Take screenshots at desktop (1440px) and mobile (390px) widths
   - Run a Lighthouse audit for performance/accessibility data
   - Evaluate DOM for CTA count, form fields, trust badges, social proof elements

If Chrome DevTools is not available, fall back to WebFetch + HTML analysis only.

## Step 2: Score 8 Dimensions

Each dimension is scored 0-100. The weighted aggregate gives the overall score.

### 1. Headline Clarity (weight: 15%)
- Is the value proposition clear in under 5 seconds?
- Does the headline answer "what is this and why should I care?"
- Is it specific (numbers, outcomes) or vague ("the best solution")?
- **90+**: Specific outcome + target audience in headline. "Read 100 feeds in one place. No algorithms."
- **70-89**: Clear but generic. "The modern RSS reader."
- **50-69**: Vague or feature-focused. "A powerful feed aggregation platform."
- **<50**: No clear value prop, or headline is the product name only.

### 2. CTA Visibility (weight: 20%)
- Is there a primary CTA above the fold?
- Is the CTA text action-oriented and specific? ("Start reading free" > "Sign up")
- Is there only ONE primary CTA? (multiple = confusion)
- Is the CTA visually distinct (contrast, size, whitespace)?
- **90+**: Single clear CTA above fold, action-specific text, high contrast, repeated at scroll points
- **70-89**: CTA present but generic text or low contrast
- **50-69**: CTA below fold or competing with secondary CTAs
- **<50**: No clear CTA or CTA hidden

### 3. Social Proof (weight: 15%)
- User count, testimonials, logos, ratings, press mentions?
- Are testimonials specific (name, role, company) or anonymous?
- Are numbers real and verifiable?
- **90+**: Named testimonials with photos + specific metrics + recognizable logos
- **70-89**: Some social proof but generic ("loved by thousands")
- **50-69**: Weak social proof or buried below fold
- **<50**: No social proof at all

### 4. Urgency (weight: 5%)
- Is there a reason to act now? (limited spots, launch pricing, beta access)
- Is the urgency real or manufactured?
- NOTE: Not all pages need urgency. Score 60 (neutral) if urgency doesn't apply. Only penalize if urgency would clearly help but is missing.
- **90+**: Real, specific urgency (countdown, limited spots with number)
- **70-89**: Soft urgency ("Early access", "Beta")
- **50-69**: No urgency but not needed
- **<50**: Urgency would help but is completely absent

### 5. Trust Signals (weight: 10%)
- Security badges, privacy policy link, HTTPS, team/company info?
- Is there a real human/company behind this? (about page, team photos, address)
- Free trial / money-back guarantee / no credit card needed?
- **90+**: Multiple trust layers (SSL + privacy + real team + guarantee + social proof)
- **70-89**: Basic trust (SSL, privacy link)
- **50-69**: Minimal trust signals
- **<50**: Feels sketchy or anonymous

### 6. Form Friction (weight: 15%)
- How many fields in the signup/contact form?
- Can you start with just an email? Or Google/social login?
- Is there progressive disclosure (don't ask everything upfront)?
- **90+**: One-click signup (Google/Apple) or single email field
- **70-89**: 2-3 fields, clear labels
- **50-69**: 4+ fields or confusing labels
- **<50**: Long form, required phone number, or unclear what happens after submit

### 7. Mobile Responsiveness (weight: 10%)
- Does the layout work on mobile (390px)?
- Is the CTA tappable (44px+ touch target)?
- Is text readable without zooming?
- Do images/videos resize properly?
- **90+**: Flawless mobile experience, CTA thumb-reachable
- **70-89**: Works but some elements feel cramped
- **50-69**: Layout breaks or CTA hard to find on mobile
- **<50**: Not mobile-friendly

### 8. Page Speed Indicators (weight: 10%)
- Does the page feel fast? (no heavy animations, lazy-loaded images, minimal JS)
- Lighthouse performance score if available
- Large hero images or videos that block rendering?
- **90+**: Lighthouse 90+, instant load feel, no layout shift
- **70-89**: Loads in 2-3 seconds, minor layout shifts
- **50-69**: Noticeable lag, heavy assets
- **<50**: Slow, blocking resources, poor mobile performance

## Step 3: Calculate Overall Score

```
Overall = (Headline x 0.15) + (CTA x 0.20) + (Social Proof x 0.15) +
          (Urgency x 0.05) + (Trust x 0.10) + (Friction x 0.15) +
          (Mobile x 0.10) + (Speed x 0.10)
```

Grade scale:
- **A+ (95-100)**: Exceptional. Ship and monitor.
- **A (90-94)**: Strong. Minor polish only.
- **B+ (85-89)**: Good. 1-2 improvements would make a real difference.
- **B (80-84)**: Solid foundation with clear gaps.
- **C (70-79)**: Significant issues. Fix before major traffic push.
- **D (60-69)**: Major problems. Needs redesign of weak areas.
- **F (<60)**: Fundamental issues. Don't spend on traffic until fixed.

## Step 4: Industry Benchmarks

Compare against typical scores for the industry:

| Industry | Avg Score | Top 10% |
|----------|-----------|---------|
| SaaS | 72 | 88+ |
| E-commerce | 68 | 85+ |
| Consumer App | 65 | 82+ |
| Media/Content | 60 | 78+ |
| Agency/Services | 70 | 86+ |

## Step 5: Output

```
---
## CRO Audit: [URL]
**Date**: [YYYY-MM-DD]
**Industry**: [detected or specified]
**Overall Score**: XX/100 (Grade: X)
**Benchmark**: [vs industry avg and top 10%]

### Dimension Scores

| # | Dimension | Score | Weight | Weighted |
|---|-----------|-------|--------|----------|
| 1 | Headline Clarity | XX/100 | 15% | XX |
| 2 | CTA Visibility | XX/100 | 20% | XX |
| 3 | Social Proof | XX/100 | 15% | XX |
| 4 | Urgency | XX/100 | 5% | XX |
| 5 | Trust Signals | XX/100 | 10% | XX |
| 6 | Form Friction | XX/100 | 15% | XX |
| 7 | Mobile | XX/100 | 10% | XX |
| 8 | Page Speed | XX/100 | 10% | XX |

### Top 3 Priority Fixes

1. **[Dimension]** (current: XX -> target: XX)
   - What's wrong: [specific issue]
   - Fix: [specific actionable recommendation]
   - Impact: [expected improvement]

2. ...
3. ...

### Dimension Details
[For each dimension: what was observed, what's good, what needs work. 2-3 lines each max.]

### Screenshots
[Reference desktop and mobile screenshots if taken]
---
```

## Rules

- Be specific in feedback. "Your CTA says 'Submit'" is useful. "Improve your CTA" is not.
- Reference what you actually see on the page, not generic advice.
- If you can't assess a dimension (e.g., no mobile screenshot available), score it as "N/A" and exclude from the weighted average.
- Don't fabricate Lighthouse scores. If you can't run it, say so and assess speed qualitatively.
- Urgency is the one dimension where a neutral score (60) is fine. Not every page needs urgency.
