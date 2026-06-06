---
description: Serialize the current Claude Code session into a handoff document so a fresh session can resume the work with zero context loss. Use when the user says hand off, pass the baton, wrap up the session, save context before /clear, or context is running low.
allowed-tools: Read, Write, Bash
---

# ops-handoff

Capture the state of the current session into a dated handoff note, so a new session resumes without re-discovering everything.

## Positioning

- A handoff is a **task-in-progress transfer**: ephemeral and dated. It is NOT long-term memory.
- Long-term, stable facts belong in your persistent memory file. Do not duplicate them here.
- A handoff complements memory: it captures the volatile working state that memory deliberately omits.

## Where to save

Save to: `~/handoffs/YYYY-MM-DD-HHmm-[subject].md`

- `subject` is a short kebab-case slug of the current task (e.g. `payments-refactor`).
- Save in a folder that persists and syncs across devices (a notes vault, a synced directory), not OS temp.
- Create the folder if missing: `mkdir -p ~/handoffs`.
- Generate the timestamp with `date "+%Y-%m-%d-%H%M"`.

## Core principle: reference, never duplicate

If information already lives in another artefact (note, source file, PR, URL), **link to it by path or URL**. Do not copy its content into the handoff. The handoff is an index of state, not a snapshot of everything.

## What to capture

Write these sections in order. Keep each tight.

1. **Goal** — the task in progress, in one or two sentences.
2. **Decisions made** — choices locked in this session, with the reasoning if non-obvious.
3. **Current state** — where things stand right now (what works, what is half-done).
4. **Next steps** — the concrete actions the next session should take, ordered.
5. **Files & notes touched** — absolute paths / links / URLs. Do not paste their contents.
6. **Open questions** — unresolved points, blockers, things needing the user's input.
7. **Suggested skills** — which skills to invoke next session to continue (e.g. `/product-prd-write`, `/skill-create`). List only relevant ones.

## Redaction

Never copy secrets, credentials, tokens, or private keys into the handoff. Reference where they live instead (e.g. "API key in the password manager / `.env`"). If a touched file contains secrets, link the file but redact the values.

## Template

```markdown
# Handoff — [subject] — YYYY-MM-DD HHmm

## Goal
...

## Decisions made
- ...

## Current state
...

## Next steps
1. ...

## Files & notes touched
- `/abs/path/to/file` — what changed / why it matters
- [link or note reference]

## Open questions
- ...

## Suggested skills
- `/skill-name` — why
```

## After writing

Print the absolute path of the saved handoff so the user can open or share it. Do not summarise the whole content back; the file is the artefact.
