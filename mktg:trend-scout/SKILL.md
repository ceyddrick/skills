---
description: Scan HN, Reddit, Google Trends, and X for trending topics relevant to a given domain. Scores trends by relevance and suggests content angles. Use for content marketing ideation on any product or topic.
allowed-tools: Read, Write, WebFetch, WebSearch
argument-hint: "<domain or product> [sources: hn,reddit,trends,x]"
---

# Trend Scout — Content Opportunity Detection

Scans multiple sources for trending topics and conversations relevant to your domain. Scores each trend by relevance and suggests content angles with recommended platforms.

## Configuration

### Step 0: Define the domain

Before scanning, the skill needs a **domain configuration**. Either:
- The user provides it explicitly: "trend-scout for project management tools"
- The skill reads the current project's CLAUDE.md or brand brief for context
- The user is asked: "What product/domain should I scan for?"

From the domain, derive:

### Relevance keywords (3 tiers)

**High relevance** (+25 points): product name, direct competitors, category name, core problem being solved
**Medium relevance** (+10 points): adjacent categories, related user behaviors, industry terms
**Low relevance** (+5 points): broad themes the audience cares about

Example for a project management tool:
- High: Asana, Monday, Linear, Jira, project management, task tracking, sprint planning
- Medium: team collaboration, remote work, agile, kanban, product roadmap, Notion
- Low: productivity, startup tools, developer tools, SaaS

### Sources

1. **Hacker News** -- top 30 stories
2. **Reddit** -- hot posts from subreddits relevant to the domain (ask or infer from context)
3. **Google Trends** -- trending searches via WebSearch
4. **X/Twitter** -- via WebSearch for "site:x.com" + keywords

### Competitor list

Derive from context or ask: "Who are the 3-5 main competitors to monitor?"

## Input

- Required: domain/product (explicit or from project context)
- Optional: topic focus to narrow the scan (e.g., "pricing backlash", "migration pain")
- Optional: source filter (e.g., "hn,reddit" to scan only those)

## Step 1: Scan Sources

### Hacker News
- WebFetch https://hacker-news.firebaseio.com/v0/topstories.json (get top 30 IDs)
- For each relevant-looking ID, fetch the story: https://hacker-news.firebaseio.com/v0/item/{id}.json
- Extract: title, URL, score, comment count
- Filter: only stories with relevance score >= 10

### Reddit
- For each subreddit, WebFetch https://www.reddit.com/r/{subreddit}/hot.json?limit=15
- Extract: title, score, comment count, URL, subreddit
- Filter: score > 20 and relevance score >= 10

### Google Trends
- WebSearch for trending topics in the domain
- Build search queries from the HIGH relevance keywords + "[current year]", "trends", "alternative to [competitor]"
- Extract: trending topics, related queries, rising searches

### X/Twitter
- WebSearch for: "site:x.com [product name]" OR "site:x.com [category]"
- Also search for: "site:x.com [competitor1]" OR "site:x.com [competitor2]" (competitor mentions)
- Extract: post content, engagement signals, author

## Step 2: Score Each Trend

For each item found:

```
Relevance Score = sum of keyword matches (HIGH: +25, MEDIUM: +10, LOW: +5)
```

Additional scoring bonuses:
- **Recency**: posted in last 24h: +15, last 48h: +10, last week: +5
- **Engagement**: HN score > 100: +10, Reddit score > 200: +10, high comment count: +5
- **Sentiment**: negative sentiment about competitors: +10 (opportunity), positive sentiment about our space: +5

Only include items with total score >= 20.

## Step 3: Generate Content Angles

For the top 10 trends, suggest:

1. **Angle**: what take could the brand/founder have on this?
2. **Format**: X post, long-form X, blog post, or feature idea for the product
3. **Hook**: a draft opening line
4. **Urgency**: time-sensitive (ride the wave now) or evergreen (can wait)
5. **Effort**: low (tweet), medium (long post), high (blog/feature)

Prioritize angles that:
- Position the product as relevant to the conversation being discussed
- Let the author share an informed opinion (not just promote)
- Are timely (ride a trending conversation)
- Match the author's voice and style

## Step 4: Output

```
---
## Trend Scout Report
**Date**: [YYYY-MM-DD]
**Sources scanned**: [list]
**Trends found**: [total] | **Relevant**: [filtered count]

### Top Opportunities

#### 1. [Trend title] (Score: XX)
- **Source**: [HN/Reddit/Trends/X] | **Engagement**: [score/comments]
- **Why it matters**: [1 line]
- **Angle**: [suggested take]
- **Format**: [X post / long-form / blog]
- **Hook**: "[draft opening line]"
- **Urgency**: [time-sensitive / evergreen]

#### 2. ...

[up to 10 trends]

### Competitor Mentions
[Any mentions of competitors from the configured list]

### Emerging Themes
[2-3 line summary of recurring themes across sources]

### Recommended Actions
1. [Most time-sensitive opportunity]
2. [Best content angle for this week]
3. [Feature/product insight from user conversations]
---
```

## Rules

- Don't fabricate trends. If a source returns nothing relevant, say so.
- Don't force relevance. A trending topic about AI is not automatically relevant to your domain.
- Competitor mentions are always relevant, even with low keyword scores.
- Prefer actionable angles over interesting-but-useless observations.
- The hook line should match the author's voice, not sound like a marketing team.
- When in doubt about relevance, include it with a note rather than filtering it out.
