---
description: Creates a new Claude Code skill. Use when the user wants to create, scaffold, or set up a new skill. Handles folder creation (with colons in names via terminal), SKILL.md structure, and conventions.
allowed-tools: Bash, Write, Read
---

# Skill Creator

Create a new Claude Code skill following standard conventions.

## Process

1. Ask the user:
   - **Name**: in `category:name` format (e.g. `coach:call`, `product:prd`, `ops:deploy`)
   - **Purpose**: what should this skill do? (1-2 sentences is enough)
   - **Allowed tools**: which tools can the skill use without asking permission? (default: Read, Write)

2. Create the skill folder and file:
   - Path: `~/Documents/YourVault/Context/Skills/{category:name}/SKILL.md` (or wherever the user stores skills)
   - MUST use terminal (Bash/mkdir/Write) because some editors (like Obsidian) cannot create folders with `:` in the name
   - The folder will be visible and editable in the editor once created

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
- **Folder naming**: `category:name` using colons — MUST be created via terminal, not via editors that block colons
- **Description field**: starts with a verb, explains when to trigger, one sentence
- **Tone of instructions**: direct, imperative, no fluff
- **Location**: your skills folder (typically symlinked to `~/.claude/skills/`)
- **After creation**: the skill is immediately available as a slash command `/category:name` in Claude Code

## Categories already in use

Check existing skills before creating:
```bash
ls ~/.claude/skills/
```

Common categories:
- `writing:` — text writing, editing, coaching
- `product:` — product management, PRDs, analysis
- `coach:` — structured thinking, calls, feedback
- `ops:` — infrastructure, server, deployment
- `obsidian:` — vault operations, notes, templates

## What NOT to do

- Never create the folder from an editor that forbids colons in folder names
- Never use a language other than English in the SKILL.md content
- Never skip the frontmatter (description + allowed-tools are required)
- Never create a skill without confirming name and purpose with the user first
