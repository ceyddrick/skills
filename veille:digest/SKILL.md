---
description: Surface the best content from the past week across the user's domains of interest. Filters ruthlessly, delivers with opinion, and creates vault clippings for keepers. Use weekly or on-demand.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, WebSearch, WebFetch
---

# Veille Digest

Find what's worth reading this week. Not a link dump. A curated, opinionated selection of content that matters for the user's role and interests.

## Philosophy

Veille is guided by a few principles:
- **"Don't delegate understanding"** (Steph Ango) — surface things that BUILD understanding, not things that replace thinking
- **Anti-hype filter** — skip the "AI will change everything" takes. Keep the "here's what actually happened when we tried" pieces.
- **Practitioner over pundit** — favor people who build things over people who comment on things
- **Signal density** — one excellent article beats ten mediocre ones. If only 2 things are worth reading this week, output 2 things.

## Domains

Search across the user's domains of interest, weighted by priority. Configure these based on the user's role, current challenges, and side interests. Example structure:

### 1. Core domain (highest priority)
Whatever is most central to the user's work. Process, craft, strategy, tooling.

### 2. Practice / Tooling (practitioner angle)
Tools and workflows the user actually uses. Honest accounts of what's working and what's failing.

### 3. Industry / Competition (business)
Market moves, competitor news, sector shifts. Load a competitor list from a known path if one exists.

### 4. Thinking & Writing (personal growth)
Writing craft, clear thinking, mental models, knowledge management.

## Workflow

### 1. Search

Run 8-12 targeted WebSearches. Be specific, not generic. Adapt queries based on the current news cycle. If a major event happened (product launch, acquisition, regulation), search for that specifically.

If an argument is provided (e.g., `/veille:digest AI agents`), focus the search on that topic specifically instead of the broad domain sweep.

### 2. Filter ruthlessly

For each result, apply these filters:

**KEEP if:**
- It changes how you think about something (not just confirms what you know)
- It's from a practitioner sharing real experience, not a journalist summarizing
- It has specific data, examples, or frameworks (not just opinions)
- It's relevant to a current challenge (meeting, PRD, strategy decision)
- It would make the user say "I need to save this" or "I want to react to this"

**KILL if:**
- It's a listicle or "top 10" without substance
- It's AI hype without evidence ("AI will revolutionize X")
- It's behind a hard paywall with no substance visible
- **It's older than 1 week. Target: content from the last 7 days. Tolerance: up to 1 month if exceptionally relevant. NEVER include anything older than 1 month. WebSearch often returns old articles ranked high. ALWAYS verify the actual publication date before including (use WebFetch if unclear). If you can't confirm the date is recent, kill it. When a week is quiet, say so rather than padding with old content.**
- It reads like it was written by an LLM (generic, no voice, no edge)
- It says things everyone already knows

Target: **5-8 items max.** If you can't find 5 good ones, output fewer. Never pad.

### 3. For each keeper, assess

- **Why it matters for the user specifically** (link to their role, current challenges, interests)
- **Rebond potential**: could they react to this on social or their blog? Is there a contrarian take? A connection to their work context?
- **Vault-worthy?** Should this become a clipping in their notes?

### 4. Check against existing vault

Before presenting, search the user's clippings folder to make sure you're not surfacing something they already have.

### 5. Output

Write the digest to a file in the user's configured veille folder AND display it in conversation.

**Filename**: `YYYY-WXX - Veille Digest.md` (ISO week number)

**File format**:

```markdown
---
categories:
  - Veille
tags:
  - veille
date: YYYY-MM-DD
week: WXX
---

# Veille — Semaine du [date]

### 1. [Titre de l'article](URL)
**[Auteur]** · [Source] · [Date]
[2-3 phrases : de quoi ça parle ET pourquoi c'est pertinent pour toi. Pas un résumé neutre. Un avis.]
[Si rebond potentiel : "Angle pour réagir : ..."]

### 2. [Titre](URL)
...
```

Titles MUST be clickable links to the article URL. Number each item.

After displaying the digest, ask:

```
Des articles à clipper dans le vault ? (numéros ou "tous")
```

### 6. Clip to vault

For each article the user wants to clip, use WebFetch to get the full content, then create a file in the clippings folder following the clipping template:

```markdown
---
categories:
  - article
title: "[Title]"
source: "[URL]"
author:
  - "[[Author Name]]"
published: [YYYY-MM-DD]
created: [today's date]
description: "[first 200 chars of article]"
tags:
  - clippings
topics: [relevant topics]
Read: false
---
AI Summary (FR)
[Dense 3-5 sentence summary in French. What the article argues, key evidence, why it matters. No filler.]

----

[Full article content in markdown]
```

## Anti-patterns

- Never say "voici une sélection de X articles sur Y"
- Never summarize an article without an opinion on why it matters for the user
- Never include an article just because it's popular. Popular != valuable.
- Never use the word "incontournable", "révolutionnaire", or "game-changer"
- Never pad the digest to reach a number. 3 good items > 8 mediocre ones.
- Never output a "Sources:" section at the end. The sources are in the articles.

## Variations

- `/veille:digest` — full sweep across all domains
- `/veille:digest AI agents` — focused on a specific topic
- `/veille:digest competitors` — focused on the competitive landscape
