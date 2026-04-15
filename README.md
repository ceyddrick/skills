# Claude Code Skills

A curated collection of [Claude Code](https://claude.ai/code) Skills that turn recurring methods into reusable slash commands. Each Skill is a single `SKILL.md` file with instructions, conventions, and rules the agent follows every time you invoke it.

Full documentation for each Skill with examples, walkthroughs, and expected outputs: [cedricrittie.com/fr/ressources/skills](https://www.cedricrittie.com/fr/ressources/skills).

## Skills included

| Skill | Category | What it does |
|---|---|---|
| `/writing:xpost` | Writing | Drafts an X post in your voice from a link, idea, or rough text. |
| `/writing:unslop` | Writing | Strips AI writing patterns from a text (FR or EN auto-detected). |
| `/writing:coach` | Writing | Rewrites text applying Philip Yaffe's principles (clarity, concision, density). |
| `/veille:digest` | Research | Weekly content digest scored and filtered across your sources. |
| `/veille:events` | Research | Finds upcoming events (conferences, meetups) matching your topics and calendar. |
| `/mktg:cro-audit` | Marketing | Audits a landing page on 8 conversion dimensions with prioritized fixes. |
| `/mktg:expert-panel` | Marketing | Scores content with a 7-10 expert panel, iterates until 90/100 or 3 rounds. |
| `/mktg:trend-scout` | Marketing | Scans HN, Reddit, Google Trends and X for rising topics in a given domain. |
| `/skill:create` | Meta | The meta-Skill. Scaffolds a new Skill with naming conventions and frontmatter. |
| `/content:plan` | Marketing | Editorial orchestrator that decides what to publish, when, and why. |

## Installation

### One Skill at a time

```bash
# Pick the Skill you want, e.g. writing:coach
mkdir -p ~/.claude/skills/writing:coach
curl -sSL https://raw.githubusercontent.com/ceyddrick/skills/main/writing:coach/SKILL.md \
  -o ~/.claude/skills/writing:coach/SKILL.md
```

Restart Claude Code. Test with `/writing:coach`.

### Install all Skills at once

```bash
git clone https://github.com/ceyddrick/skills.git /tmp/skills-pack
for dir in /tmp/skills-pack/*/; do
  name=$(basename "$dir")
  mkdir -p ~/.claude/skills/"$name"
  cp "$dir/SKILL.md" ~/.claude/skills/"$name"/SKILL.md
done
rm -rf /tmp/skills-pack
```

Restart Claude Code.

## Repository layout

```
.
├── README.md
├── LICENSE
├── writing:xpost/
│   └── SKILL.md
├── writing:coach/
│   └── SKILL.md
└── ... (10 Skills total)
```

Each folder maps to a slash command of the same name. `~/.claude/skills/<name>/SKILL.md` is the contract between the file and the `/<name>` command.

## Customising

These Skills are written to be generic. Fork or edit the files to adapt them to your voice, your domains, your stack. The `description` line in the frontmatter is what Claude Code uses to route the command, so keep it meaningful.

If you build a variant that's broadly useful, PRs welcome.

## License

MIT. Use, modify, ship.

## Credits

Maintained by [Cédric Rittié](https://www.cedricrittie.com). Skills are battle-tested daily.
