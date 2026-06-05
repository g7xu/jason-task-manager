# 🗂️ jason-task-manager

A [Claude Code skill](https://docs.claude.com/en/docs/claude-code/skills) **I (Jason) built** to
run my own Notion task system. Claude auto-loads it whenever I talk about my tasks, then captures
every to-do in a consistent, **well-formed** shape and runs my daily planning rituals.

> Built on a Notion **Task Command Center** (Tasks + Daily Log databases with Board / List /
> Calendar views) and the `claude.ai` Notion connector.

---

## ✨ What it does

Just talk naturally — the skill triggers on what I say:

| I say… | Claude does… |
| --- | --- |
| `good morning` · `daily update` · `plan my day` | Pulls what's due today + overdue, proposes an ordered plan, writes today's **Daily Log** |
| `end of day` · `wrap up` | Marks finished tasks done, rolls the rest to tomorrow, fills the **End-of-Day Review** |
| `add a task…` · `I need to do X` | Creates it **well-formed** (see below) |
| `import these` (paste Todoist/CSV) | Bulk-creates tasks with dates, priorities, and projects mapped |

## 🧱 The "well-formed task" framework

Every task Claude creates satisfies five rules — so nothing is vague or un-actionable:

1. **Outcome-first** — written from the end state ("…so that ___")
2. **Atomic** — one bounded action (needs "and"? → split it)
3. **Action-oriented** — the title starts with a verb
4. **Context-complete** — Inputs, Constraints, and Dependencies captured
5. **Measurable** — a testable **Done-when**

<details>
<summary>Example of a well-formed task</summary>

```
Title:      Draft Q3 marketing budget v1
Due:        Jun 12   Priority: P2   Project: Work
Done-when:  Sheet with all 6 channels + totals, shared with Sam
Depends on: Finalize headcount plan

🎯 Outcome:     Sam can approve Q3 spend by the planning meeting
📥 Inputs:      last year's actuals, channel list, finance's $ cap
🚧 Constraints: ≤ $50k, Google Sheet, by Jun 12
```
</details>

## 🚀 Install

Clone into your Claude Code skills directory (the folder name becomes the skill name):

```bash
git clone git@github.com:g7xu/jason-task-manager.git ~/.claude/skills/jason-task-manager
```

Add your Notion IDs (this file is git-ignored — your IDs never leave your machine):

```bash
cd ~/.claude/skills/jason-task-manager
cp config.example.json config.local.json
# edit config.local.json with your real IDs
```

> 💡 Don't have the IDs handy? Ask Claude to `notion-search` for your **Task Command Center**
> page and read its child databases — it'll fill them in for you.

## 📁 Layout

```
jason-task-manager/
├── SKILL.md                  # triggers + workflow logic (what Claude loads)
├── config.example.json       # placeholder IDs (committed, public-safe)
├── config.local.json         # your real IDs (git-ignored, local only)
├── reference/
│   ├── command-center-structure.md  # what the Notion setup should look like
│   ├── well-formed-task.md          # the framework + body template + examples
│   └── daily-ritual.md              # morning / end-of-day step-by-step
└── README.md
```

`SKILL.md` stays lean; the heavy detail lives in `reference/` files that Claude reads on demand.

## ✅ Requirements

- **Claude Code** with the **Notion** connector enabled (`claude.ai Notion` MCP tools)
- A Notion task system matching the schema in [`SKILL.md`](SKILL.md) §4 — ask Claude to build
  one for you if you don't have it yet

## 🔧 Maintaining

```bash
cd ~/.claude/skills/jason-task-manager
# edit SKILL.md or the reference/ files
git add -A && git commit -m "tweak workflow" && git push
```

Keep `SKILL.md` focused on *when* and *what*; push the *how* into `reference/`.

---

<sub>🤖 Scaffolded with [Claude Code](https://claude.com/claude-code).</sub>
