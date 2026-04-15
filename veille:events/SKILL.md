---
description: Discover upcoming events (conferences, meetups, webinars) relevant to the user's interests. Scans Luma, Meetup, Eventbrite, Gmail, and web for relevant events in a target city and remote. Use when the user wants to find upcoming events or asks about what's happening.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, WebSearch, WebFetch, mcp__chrome-devtools__*, mcp__claude_ai_Gmail__*, mcp__claude_ai_Google_Calendar__*
---

# Veille Events

Find upcoming events worth attending. Not a raw dump of everything happening. A curated, scored selection of events that matter for the user's role and domain.

## Sources

### 1. Web scraping (Chrome DevTools MCP)

Scrape these platforms for events in the user's target city and remote/online:

**Luma (lu.ma)**
- Navigate to `https://lu.ma/{city}` and scrape listed events
- Also search `https://lu.ma/search?q={keyword}` for each priority keyword
- Extract: title, date, location, URL, description snippet, organizer

**Meetup (meetup.com)**
- Navigate to the relevant city + tech category page
- Try multiple category IDs and keyword searches for the user's priority topics
- Extract: title, date, location, URL, attendee count, group name

**Eventbrite**
- Navigate to the relevant city + tech category page
- Search for the user's priority topics
- Extract: title, date, location, URL, price (free/paid), organizer

For each platform:
1. Use `mcp__chrome-devtools__new_page` to open a page
2. Use `mcp__chrome-devtools__navigate_page` to go to the URL
3. Use `mcp__chrome-devtools__take_snapshot` to get the DOM
4. Parse the snapshot for event data
5. Use `mcp__chrome-devtools__close_page` when done

### 2. WebSearch (global conferences & keynotes)

Run targeted searches for major upcoming conferences and keynotes relevant to the user's domain. Adapt year to current year. Focus on events happening in the next 3 months.

### 3. Gmail scanning

Use the Gmail MCP to find event invitations and announcements:

- `mcp__claude_ai_Gmail__gmail_search_messages` with queries:
  - `subject:(invitation OR event OR conference OR meetup OR webinar) newer_than:14d`
  - `subject:(inscri OR register OR RSVP) newer_than:14d`
  - `from:(eventbrite OR meetup OR luma OR lu.ma) newer_than:14d`
  - `subject:(keynote OR summit OR conf) newer_than:14d`

- Read the top results with `mcp__claude_ai_Gmail__gmail_read_message`
- Extract event details: title, date, location, URL, organizer

### 4. Google Calendar check

Use `mcp__claude_ai_Google_Calendar__gcal_list_events` to check what's already on the calendar in the relevant time window. This prevents recommending events the user already registered for.

## Event preferences

Load preferences from an `event-preferences.json` file in this skill folder.

These preferences define:
- **Categories**: what topics to look for (weighted by priority)
- **Keywords**: search terms in the user's preferred languages
- **Location**: geographic filters
- **Exclusions**: what to skip

## Scoring

Score each event 1-10 based on these criteria:

| Criterion | Weight | Description |
|-----------|--------|-------------|
| Topic relevance | 35% | How well does it match the user's categories and keywords? |
| Speaker quality | 20% | Known practitioners > unknown speakers > corporate pitches |
| Format | 15% | Hands-on workshop > talk > panel > webinar |
| Accessibility | 15% | Free > affordable. Local/remote > travel required |
| Timing | 10% | Weekday evening or full-day > weekend. Not conflicting with calendar |
| Social proof | 5% | Attendee count, past edition reputation |

**Score thresholds:**
- 7+ : Strongly recommend
- 5-6 : Worth considering
- Below 5 : Don't show unless very few results

## Deduplication

Events may appear across multiple sources. Deduplicate by:
1. Exact URL match
2. Title similarity (normalize case, strip dates/locations, Jaccard similarity > 0.6)
3. Same date + similar title = likely duplicate

When merging duplicates, keep the richest data. Note cross-source appearance as a confidence boost (+0.5 to score).

## Workflow

### 1. Load context

- Read `event-preferences.json` for preferences
- Check Google Calendar for the target time window (next 3 months by default)
- Note already-registered events to exclude from results

### 2. Collect events

Run all sources in parallel where possible:
- Chrome MCP scraping (Luma, Meetup, Eventbrite)
- WebSearch for global conferences
- Gmail scan for invitations

### 3. Process

- Deduplicate across sources
- Score each event
- Filter out exclusions (from preferences)
- Filter out events already on calendar
- Sort by score descending

### 4. Output

Display a scored table in conversation:

```
## Evenements a venir

| # | Score | Titre | Date | Lieu | Type | Source |
|---|-------|-------|------|------|------|--------|
| 1 | 9.2 | [Event Name](url) | 15 mai | Paris 3e | Conference | Luma + Eventbrite |
| 2 | 8.5 | [Event Name](url) | 22 mai | Remote | Webinar | Gmail |
| ... |

### Details

#### 1. Event Name (9.2/10)
- Date : ...
- Lieu : ...
- Prix : Gratuit / 50EUR / ...
- Speakers : ...
- Pourquoi : [1-2 sentences on why this is relevant for the user]
- Source : Luma, Eventbrite

[repeat for each event]
```

Then ask:
```
Quels evenements tu veux que j'ajoute au calendrier ? (numeros, "tous", ou "non")
Creer des notes dans le vault ? (numeros, "tous", ou "non")
```

### 5. Add to calendar

For each selected event, use `mcp__claude_ai_Google_Calendar__gcal_create_event` with:
- Title: event name
- Date/time: from event data
- Location: venue or "Remote" + link
- Description: brief description + source URL
- Reminder: 1 day before

### 6. Create vault notes

For each selected event, create a note in the user's notes folder with:

```markdown
---
categories:
  - Events
tags:
  - events
date: [event date]
location: [venue or Remote]
url: "[event URL]"
source: [where we found it]
score: [score/10]
registered: false
---

# [Event Name]

**Date** : [full date and time]
**Lieu** : [location details]
**Prix** : [price or free]
**Organisateur** : [organizer]

## Description

[Event description]

## Speakers

[If available]

## Pourquoi y aller

[Why this is relevant for the user, based on scoring rationale]
```

## Variations

- `/veille:events` — full scan across all sources, next 3 months
- `/veille:events AI` — focused on AI events only
- `/veille:events this week` — narrow time window to current week
- `/veille:events remote` — only remote/online events

When an argument is provided, adjust search queries and scoring weights accordingly.

## Anti-patterns

- Never list events without scores and rationale
- Never include events that already passed
- Never include job fairs, comedy shows, networking-only events (unless preferences say otherwise)
- Never include events with no date or no URL
- Never show more than 15 events. If more found, show top 15 only.
- Never pad results. If only 3 good events found, show 3.
- Never include "corporate webinar" lead-gen traps disguised as events
