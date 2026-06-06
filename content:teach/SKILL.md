---
description: Produces a pedagogical guide for an educational site or blog that teaches a non-technical audience. Use when the user wants to write, draft, or structure a teaching guide, tutorial, or explainer for publication (not a 1:1 tutoring session).
allowed-tools: Read, Write, WebSearch, WebFetch
---

# Content Teach — Pedagogical Guide

Write a public teaching guide that takes a non-technical reader from "I don't get it" to "I can do it." This is content production, not live tutoring: the reader is anonymous and reads alone, so the guide must carry the whole learning loop on its own.

Before anything, load your site context: positioning, editorial voice (banned words, tone), and the catalogue quality bar. Respect that voice throughout.

## The four pillars (define before writing)

Answer these before drafting a single section. If you cannot, ask the user.

1. **MISSION** — the reader's *why*. What can they concretely do after reading that they could not before? State it as a real-world outcome ("draft a prompt that gets usable output," not "understand prompting"). Without this, the guide reads abstract.

2. **ZONE OF PROXIMAL DEVELOPMENT** — calibrate the level. What do you assume the reader already knows? Name the prerequisites explicitly. Do not over-explain basics they have, do not skip the gap they actually face. Aim just above their current reach.

3. **The KNOWLEDGE → SKILLS → WISDOM triptych** — structure the body around it:
   - **Knowledge**: explain the concept from reliable, cited sources (see Sourcing below).
   - **Skills**: one hands-on exercise with a feedback loop. The reader does something and can tell whether they got it right. No exercise = no skill transfer.
   - **Wisdom**: close by pointing to a real community or ongoing practice (a tool, a place, a habit) so learning continues past the page.

## Sourcing — non-negotiable

Never rely on the model's parametric knowledge. Every factual claim, capability statement, price, or version must be checked against a live source via WebSearch / WebFetch and cited. If a claim cannot be sourced, cut it or flag it as uncertain. Prefer primary sources (vendor docs, papers) over secondary commentary. Avoid time-sensitive specifics that go stale fast unless dated and sourced.

## Site glossary

Each guide feeds a shared site glossary for cross-guide terminology consistency (also an SEO/UX asset).

- Before defining a term, check your glossary file. Reuse the existing definition verbatim.
- For any new key term the guide introduces, append it to that file (term + one-line plain-language definition + the guide that introduced it). Create the file if missing.

## Output

Follow a fixed guide structure with this frontmatter and body, then save the draft to your content pipeline. Do not publish or commit.

Frontmatter:

```yaml
---
title:
description:   # one sentence, the reader's mission, used for SEO meta
audience:      # who this is for + assumed prerequisites (ZPD)
mission:       # concrete outcome after reading
sources: []    # list of cited URLs
glossary: []   # key terms this guide adds to the site glossary
---
```

Body, in order:

1. **Hook + mission (1 short paragraph)** — name the reader's situation and state what they will be able to do by the end. Concrete, not abstract.
2. **What you need first (prerequisites)** — the ZPD line. 2-4 bullets of assumed knowledge. Reassure if low, redirect to a prior guide if one covers a gap.
3. **Knowledge — the concept** — explain the idea from cited sources. One recognizable example per concept. Define jargon inline and tag it for the glossary. Inline citations.
4. **Skills — do it yourself** — a single, scoped, hands-on exercise. Give the task (precise, doable in a few minutes), what good output looks like (the feedback signal), and one common mistake plus how to spot it.
5. **Wisdom — keep going** — point to a real community, tool, or practice. One next step the reader can take today.
6. **Sources** — numbered list of every cited URL. No source = claim removed.

## Rules

- One guide = one mission. If scope sprawls, split it.
- Plain language for non-technical readers. Define jargon on first use, link to the glossary.
- Show, don't assert: every concept gets a concrete example the reader recognizes.
- Match your editorial voice — no AI slop, no filler, no em dashes.
- Reader can complete the exercise without external help.
