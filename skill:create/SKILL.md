---
description: Creates a new Claude Code skill. Use when the user wants to create, scaffold, or set up a new skill. Handles folder structure, SKILL.md conventions, naming, and progressive disclosure.
allowed-tools: Bash, Write, Read
---

# Skill Creator

Create a new Claude Code skill following standard conventions.

## Process

1. Ask the user:
   - **Name**: in `category-name` format (e.g. `coach-call`, `product-prd`, `ops-deploy`)
   - **Purpose**: what should this skill do? (1-2 sentences is enough)
   - **Allowed tools**: which tools can the skill use without asking permission? (default: Read, Write)

2. Create the skill folder and file:
   - Path: `<skills folder>/{category-name}/SKILL.md` (the skills directory, typically symlinked to `~/.claude/skills/`)
   - The dash separator is sync-safe: tools that block `:` in folder names (some note editors) handle a dash fine
   - Run `ls` on the skills folder first to check existing categories

3. Write the SKILL.md following this template:

```markdown
---
description: [One clear sentence. Start with a verb. Explain WHEN to trigger this skill.]
allowed-tools: [Comma-separated list of tools]
---

# [Skill title]

[Core instructions for Claude when this skill is invoked.]

## [Sections as needed]

[Keep instructions precise and actionable. No filler.]
```

## Conventions

- **Language**: all skill files are written in English (instructions, frontmatter, comments)
- **Folder naming**: `category-name` using a dash separator. Dash (not colon) so the folder syncs safely across editors and devices, including tools that block `:` in folder names
- **Description field**: starts with a verb, explains when to trigger, one sentence. A vague description ("Helps with documents") gives the agent no way to distinguish this skill from others — name the concrete triggers
- **Tone of instructions**: direct, imperative, no fluff
- **Location**: your skills folder (typically symlinked to `~/.claude/skills/`)
- **After creation**: the skill is immediately available as a slash command `/category-name` in Claude Code

## Progressive disclosure

Keep SKILL.md concise. As a rule of thumb, if it grows past ~100 lines, split the detail into companion files loaded on demand:

- `REFERENCE.md`, `EXAMPLES.md`, `FORMAT.md` — pulled in only when the relevant step runs
- `scripts/` — for deterministic logic. A bundled script saves tokens and is more reliable than code regenerated each run

Keep references one level deep (SKILL.md points to companion files, companion files do not chain further).

## Categories already in use

Check existing skills before creating:
```bash
ls ~/.claude/skills/
```

Common categories:
- `writing-` — text writing, editing, coaching
- `product-` — product management, PRDs, analysis
- `coach-` — structured thinking, calls, feedback
- `ops-` — infrastructure, server, deployment
- `veille-` — monitoring, digests, triage
- `mktg-` — marketing copy, CRO, expert panels

## Review checklist

Before finishing, verify:
- [ ] Description starts with a verb and names concrete triggers
- [ ] Folder uses the `category-name` dash convention
- [ ] No time-sensitive info baked in (dates, "current" versions)
- [ ] Terminology is consistent throughout the file
- [ ] SKILL.md stays concise; detail externalised if past ~100 lines
- [ ] References are one level deep
- [ ] Frontmatter has both `description` and `allowed-tools`

## What NOT to do

- Never use a language other than English in the SKILL.md content
- Never skip the frontmatter (description + allowed-tools are required)
- Never bake time-sensitive info into a skill (it goes stale)
- Never create a skill without confirming name and purpose with the user first
