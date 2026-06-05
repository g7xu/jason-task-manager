# task-manager (Claude Code skill)

A personal [Claude Code skill](https://docs.claude.com/en/docs/claude-code/skills) that runs my
task-management workflow in Notion: a **well-formed-task** framework plus daily **morning-plan**
and **end-of-day-review** rituals, backed by a Notion "Task Command Center" (Tasks + Daily Log
databases with Board / List / Calendar views).

## What it does

- Auto-loads when I say "good morning", "daily update", "plan my day", "end of day", or ask to
  add / import / reschedule / review tasks.
- Creates every task in a consistent shape: outcome-first, atomic, verb-led title, with Inputs,
  Constraints, Dependencies, and a measurable **Done-when**.
- Runs the daily ritual and keeps the Notion databases tidy.

## Install

Clone into your Claude Code skills directory (the folder name becomes the skill name):

```bash
git clone <this-repo-url> ~/.claude/skills/task-manager
```

Then add your Notion IDs:

```bash
cd ~/.claude/skills/task-manager
cp config.example.json config.local.json
# edit config.local.json with your real IDs (it is git-ignored)
```

To find your IDs, open each database/view in Notion and copy the ID from its URL, or ask Claude
to `notion-search` for your command-center page and read its child databases.

## Layout

```
task-manager/
├── SKILL.md                     # triggers + workflow logic (what Claude loads)
├── config.example.json          # placeholder IDs (committed)
├── config.local.json            # your real IDs (git-ignored)
├── reference/
│   ├── well-formed-task.md       # the framework + body template + examples
│   └── daily-ritual.md           # morning / end-of-day step-by-step
└── README.md
```

## Requirements

- The **Notion** connector enabled in Claude Code (the `claude.ai Notion` MCP tools).
- A Notion task system matching the schema in `SKILL.md` §4. (Ask Claude to build one if you
  don't have it yet.)

## Maintaining

Edit `SKILL.md` or the `reference/` files and commit. Keep `SKILL.md` lean — push detail into
`reference/` files, which Claude reads on demand.
