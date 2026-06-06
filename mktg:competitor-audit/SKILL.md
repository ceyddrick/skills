---
description: Audit a competitor's website on 5 dimensions (positioning, conversion, SEO/GEO, offer/pricing, design/UX) and produce a scored report with a competitive verdict per dimension. Use when sizing up a competitor, before a positioning decision, or to find where a rival beats you.
allowed-tools: Read, Write, WebFetch, WebSearch, Bash, mcp__chrome-devtools__navigate_page, mcp__chrome-devtools__take_screenshot, mcp__chrome-devtools__take_snapshot, mcp__chrome-devtools__evaluate_script, mcp__chrome-devtools__lighthouse_audit, mcp__chrome-devtools__resize_page
argument-hint: "<competitor URL> [your own site URL]"
---

# Competitor Audit — Website Teardown & Scoring

Audit a competitor's website on 5 dimensions. Produce a grade (A+ to F), a competitive verdict per dimension (Threat / Opportunity / Parity), and prioritized recommendations for the user's own site.

This skill is self-contained and runs end-to-end on its own.

## Input

- **Competitor URL** (required). If none provided, ask for one.
- **Your own site URL** (optional). If provided, every dimension is judged comparatively and the report frames threats and opportunities relative to it. If absent, run a standalone audit and skip the comparative verdicts (mark them "N/A — no reference site").
- Optional: industry context (SaaS, fintech, ecommerce, media, services). If not given, detect it from the homepage.

## Step 1 — Decide the page set

A competitor audit is never just the landing page. Before fetching, settle on a page set:

1. **Homepage** — always.
2. **Pricing page** — always if it exists. If pricing is gated ("contact sales"), note it and audit what is visible.
3. **One product / feature / offer page** — pick the most prominent one from the nav.
4. **About / company page** — for trust signals and positioning.

Find these by fetching the homepage first and reading its navigation. List the 3-4 URLs you will audit before going further.

## Step 2 — Capture the pages

For each page in the set:

1. If **Chrome DevTools MCP** is available (preferred):
   - Navigate to the URL. Take a screenshot at desktop (1440px) and mobile (390px).
   - Take a DOM snapshot. Use `evaluate_script` to count CTAs, form fields, trust badges, pricing tiers, structured-data blocks.
   - Run a Lighthouse audit on the homepage for real performance/accessibility/SEO data.
2. **Fallback — WebFetch** for text, copy, and SEO signals.

JS-heavy sites (React/Next SPAs — most modern SaaS) render empty or partial under WebFetch. Use Chrome DevTools for anything that depends on the rendered DOM: messaging, CTAs, pricing tables, schema. Use WebFetch only for static text and meta tags.

Never fabricate a Lighthouse score. If you cannot run Lighthouse, assess speed qualitatively and say so explicitly.

## Step 3 — Score the 5 dimensions

Each dimension is scored 0-100 using its anchors below. The weighted aggregate gives the overall score.

For every issue you log, use this finding format. Each finding must reference something actually observed on a page — never generic advice.

> **Issue** — what is wrong (quote the headline, name the page).
> **Impact** — why it costs them, or why it threatens the user.
> **Evidence** — the exact element: a quoted line, a screenshot reference, a DOM count.
> **Fix** — a specific, actionable change.

### 1. Positioning & Messaging (weight: 20%)

- Is the value proposition clear in under 5 seconds?
- Is the target audience named, or is it "for everyone"?
- Is there a category frame and a clear differentiator vs alternatives?
- Is the message consistent across homepage, product page, and about?
- **90+**: Specific value prop + named audience + clear differentiator, consistent across pages.
- **70-89**: Clear but generic positioning. "The modern way to X."
- **50-69**: Feature-led, no audience, no differentiation.
- **<50**: No discernible value prop; visitor cannot tell what it is or who it is for.

### 2. Conversion / CRO (weight: 25%)

Condensed CRO logic — assess these sub-points and score the dimension as a whole:

- **Headline**: answers "what is this and why care?" — specific over vague.
- **CTA**: one primary CTA above the fold, action-specific text, visually distinct, repeated at scroll points.
- **Social proof**: named testimonials, logos, real metrics — placed near CTAs.
- **Trust signals**: HTTPS, real company info, guarantee / free trial / no-card-needed.
- **Form friction**: how many fields to start; one-click or single-email is best.
- **Mobile**: layout holds at 390px, CTA is a 44px+ thumb-reachable target.
- **Speed**: fast load feel; use the Lighthouse performance score if captured.
- **90+**: Single sharp CTA above fold, strong proof near it, low friction, fast, flawless mobile.
- **70-89**: Converts but with generic CTA copy, weak proof, or minor friction.
- **50-69**: CTA buried or competing, thin proof, 4+ form fields, cramped mobile.
- **<50**: No clear CTA, no proof, heavy friction, broken mobile.

### 3. SEO & GEO (weight: 20%)

Classic SEO plus GEO (visibility inside generative engines — ChatGPT, Perplexity, Google AI overviews).

- **Technical**: indexable, crawlable, Core Web Vitals (LCP <2.5s, INP <200ms, CLS <0.1).
- **On-page**: title 50-60 chars, meta description 150-160 chars, single H1, keyword in the first 100 words.
- **Content & E-E-A-T**: depth, named authors, evidence, recency.
- **Structured data**: schema.org / JSON-LD present and valid (Organization, Product, FAQ).
- **GEO**: citable answer-shaped content, clear entity definitions, `llms.txt`, content that an AI can quote verbatim.
- **90+**: Clean technical base, strong on-page, valid schema, content built to be cited by AI engines.
- **70-89**: Solid classic SEO, little to no GEO consideration.
- **50-69**: Gaps in technical or on-page basics; no schema.
- **<50**: Indexation problems, missing meta, no structure.

If structured data is injected client-side it may not show in WebFetch — verify via the rendered DOM or say "could not verify". Never invent it.

### 4. Offer & Pricing (weight: 20%)

- Is pricing transparent and easy to find, or hidden behind "contact sales"?
- Is the plan structure clear, with sensible anchoring and a guided default?
- Is what each plan includes legible at a glance?
- Is there a free trial, freemium tier, or guarantee that lowers the entry risk?
- Is the perceived value vs price defensible?
- **90+**: Transparent pricing, clean tiers with a clear anchor and recommended plan, low-risk entry.
- **70-89**: Pricing visible but tiers are confusing or value is unclear.
- **50-69**: Pricing partly hidden, or packaging is hard to parse.
- **<50**: No visible pricing, no entry path, opaque packaging.

Gated pricing is a deliberate choice for some segments — score what is visible, do not over-penalize an enterprise model. Pricing changes often: screenshot it and date-stamp the audit as a point-in-time snapshot.

### 5. Design & UX (weight: 15%)

- Visual hierarchy: does the eye land on the right things?
- Typography and spacing: consistent, readable, deliberate.
- Component and brand consistency across pages.
- Navigation: predictable, shallow, labelled clearly.
- Responsive behaviour and loading/empty/error states.
- Accessibility: contrast (WCAG AA), touch targets, alt text.
- Dark patterns: flag manipulative UX (forced continuity, confirmshaming, hidden costs).
- **90+**: Coherent, accessible, confident design that supports the message.
- **70-89**: Clean but generic, or small inconsistencies.
- **50-69**: Dated, inconsistent, or accessibility gaps.
- **<50**: Broken layout, illegible, or dark patterns present.

## Step 4 — Calculate the overall score

```
Overall = (Positioning x 0.20) + (Conversion x 0.25) + (SEO_GEO x 0.20) +
          (Offer_Pricing x 0.20) + (Design_UX x 0.15)
```

Grade scale:

- **A+ (95-100)**: Exceptional. A serious competitive threat.
- **A (90-94)**: Strong across the board.
- **B+ (85-89)**: Good, with one or two real gaps.
- **B (80-84)**: Solid foundation, clear weak spots.
- **C (70-79)**: Significant issues. Beatable.
- **D (60-69)**: Major problems. Wide open.
- **F (<60)**: Fundamentally weak.

If a dimension cannot be assessed, score it "N/A" and exclude it from the weighted average (re-normalize the remaining weights).

## Step 5 — Competitive verdict per dimension

For each dimension, if the user's own site URL was provided, audit it on the same dimension and assign a verdict:

- **Threat** — the competitor is clearly stronger here. The user is exposed.
- **Opportunity** — the competitor is weak here. The user can win this ground.
- **Parity** — roughly equal; not a deciding factor.

If no reference site was provided, skip verdicts and mark them "N/A — no reference site". The rest of the audit still stands as a standalone teardown.

## Step 6 — Output

Write the report as a markdown block.

```
## Competitor Audit: [Competitor name] — [URL]

**Date**: [YYYY-MM-DD]
**Industry**: [detected or specified]
**Pages audited**: [list]
**Reference site**: [user's site URL, or "none"]
**Overall Score**: XX/100 (Grade: X)

### Snapshot

| Dimension | Score | Weight | Verdict |
|-----------|-------|--------|---------|
| Positioning & Messaging | XX/100 | 20% | Threat / Opportunity / Parity |
| Conversion / CRO | XX/100 | 25% | ... |
| SEO & GEO | XX/100 | 20% | ... |
| Offer & Pricing | XX/100 | 20% | ... |
| Design & UX | XX/100 | 15% | ... |

### Dimension detail

[For each of the 5 dimensions: score, a one-line verdict rationale,
then the findings in Issue / Impact / Evidence / Fix format.
What they do well = threats to the user. Their weaknesses = the user's openings.]

### Strategic takeaways

**Top 3 threats** — where the competitor beats the user:
1. ...
2. ...
3. ...

**Top 3 opportunities** — gaps the user can exploit:
1. ...
2. ...
3. ...

### Prioritized recommendations (for the user's own site)

| # | Action | Effort | Expected impact |
|---|--------|--------|-----------------|
| 1 | ... | Low/Med/High | ... |
| 2 | ... | ... | ... |
| 3 | ... | ... | ... |

### Screenshots
[Reference the desktop and mobile captures taken, if any.]
```

## Rules

- Every finding references something actually observed on a page. "Their hero says 'The pro bank that...'" is useful. "Improve the messaging" is not.
- Recommendations are framed for the user's own site, never as advice to the competitor.
- Do not fabricate Lighthouse scores, schema, or metrics. If you cannot verify, say "could not verify".
- Treat the audit as a point-in-time snapshot. Date-stamp it. Pricing and copy change.
- If a page is blocked (Cloudflare, anti-bot) or gated, mark the dimension partial and score only what is visible.
- Keep dimension detail tight: a few sharp findings beat a long generic list.
