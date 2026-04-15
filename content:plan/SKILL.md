---
description: Strategic content orchestrator for the user's online presence. Scans articles, clippings, veille, trends, and X to plan what to talk about, when, and why. Outputs content ideas and editorial calendar. Use when the user wants to plan content, find post ideas, or build an editorial strategy.
allowed-tools: Read, Write, Edit, Bash, Glob, Grep, WebFetch, WebSearch
argument-hint: "[week | month | react <topic> | from <url> | ideas]"
---

# Content Plan — Strategic Content Orchestrator

Plan what the user should talk about online based on their positioning, their sources, and what's happening in the world. This is NOT a post writer. This is the brain that decides what deserves the user's voice.

## Who the user is online

Read the voice profile at `~/.claude/skills/writing:xpost/voice-profile.md` for beliefs, tone, and positioning. The profile should capture:

- **Brand**: one-line positioning (who the user is and what they're known for)
- **Audience**: who they're writing for
- **Differentiator**: what makes their voice distinct from generic tech content
- **Site**: their blog or personal site URL

## Sources to scan

When planning content, draw from ALL of these:

### 1. The user's articles (their blog)
- Read articles in the user's blog content folder (e.g. `~/Projects/your-site/src/content/blog/*.md`)
- Each article has multiple postable angles (not just "here's my article")
- Extract: hooks, data points, contrarian takes, how-to snippets, before/after examples

### 2. Clippings (user's notes)
- Read files in the user's clippings folder
- These are curated content the user found interesting during veille
- Look for patterns, connections between clippings, angles the user could add value on

### 3. Veille digest
- Invoke `veille:digest` or read recent digest outputs
- Surface trending topics in the user's domains

### 4. Trend scout
- Invoke `mktg:trend-scout` for current trends on HN, Reddit, X
- Filter for topics where the user has a legitimate perspective

### 5. X feed context
- Search X (via WebSearch) for conversations in the user's space
- Find threads where the user's expertise adds value
- Identify debates or announcements worth reacting to

### 6. Ongoing work context
- Read the user's project/ideas folder for ongoing projects, ideas, writing intentions
- Read any "writing intentions" document for article ideas in progress

## Planning modes

### `/content:plan week`
Generate a 7-day content plan with 5-7 post ideas.

Process:
1. Scan all sources (articles, clippings, trends, X conversations)
2. Filter through the user's positioning: would this topic benefit from their voice?
3. For each idea, output:
   - **Topic**: what's the subject?
   - **Angle**: what's the user's specific take? (not just "AI is cool" but a concrete point of view)
   - **Source**: where did this come from? (article, clipping, trend, reaction)
   - **Format**: tweet, long-form, article promo, data observation, opinion?
   - **Why now**: why is this timely?
   - **Priority**: high / medium / low
4. Suggest a cadence (not every day, quality over quantity)

### `/content:plan month`
Higher-level thematic planning. Identify 3-4 themes for the month based on:
- The user's upcoming articles or guides
- Industry trends and events
- Gaps in what the user has posted recently
- Seasonal or calendar opportunities

### `/content:plan from <url>`
Decompose a single article or resource into 3-5 postable angles.

Process:
1. Fetch and read the content
2. Extract the core ideas
3. For each idea, propose a post angle that stands alone (not just a link dump)
4. Vary the formats: one hook-first, one data-first, one opinion, one how-to, one callback

### `/content:plan react <topic>`
Plan a reaction post on a specific topic or event.

Process:
1. Search X and web for the topic
2. Understand the current conversation
3. Find the user's unique angle (what can they say that others aren't saying?)
4. Propose 2-3 angles with different takes

### `/content:plan ideas`
Brainstorm mode. Generate 10+ raw post ideas from current sources without filtering too hard. Useful for filling the pipeline.

## Output format

All plans are written to the user's content planning folder with this structure:

```
Content/
  calendar-YYYY-WNN.md       ← weekly plan (e.g. calendar-2026-W15.md)
  calendar-YYYY-MM.md        ← monthly themes
  ideas.md                   ← running backlog of ideas (append, don't overwrite)
```

### Weekly calendar format

```markdown
# Content Calendar — Week NN (dates)

## Theme(s) of the week
[1-2 sentence thematic direction]

## Posts

### [Day] — [Priority: H/M/L]
**Topic**: [subject]
**Angle**: [the user's specific take]
**Format**: [tweet | long-form | article promo | data | opinion | reaction]
**Source**: [article title | clipping name | trend | X conversation]
**Hook draft**: [1-2 line draft of the opening hook, just to capture the idea]
**Why now**: [timeliness]

---
[repeat for each post]

## Backlog
[Ideas generated but not scheduled — move to ideas.md if not used]
```

### Ideas backlog format

```markdown
# Content Ideas Backlog

## Added [YYYY-MM-DD]

- **[Topic]** — [Angle] — [Source] — [Format suggestion]
- **[Topic]** — [Angle] — [Source] — [Format suggestion]
```

## Rules

- Quality over quantity. 3 great posts per week beats 7 mediocre ones.
- Every idea must pass the "voice test": would the user actually have an opinion on this? If they're just relaying information, skip it.
- Never plan content that's pure self-promotion. Even article promos must lead with the reader's problem.
- Always consider: what can the user say that a generic AI/tech account cannot?
- Prioritize ideas where the user has direct experience ("j'ai teste", "on a fait ca chez nous").
- The plan is a suggestion, not a mandate. The user picks what resonates.
- Never overwrite ideas.md. Always append with a date header.
- Write plans in the user's primary posting language.
