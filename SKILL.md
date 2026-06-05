---
name: jason-task-manager
description: Jason's personal task-management skill for his Notion "Task Command Center". Use when he says "good morning", "daily update", "plan my day", "end of day"/"wrap up", or asks to add, import, reschedule, or review tasks. Enforces his well-formed-task framework (outcome-first, atomic, verb-led title, measurable Done-when) and runs the morning-plan and end-of-day-review rituals.
---

# Jason's Task Manager

> A Claude Code skill Jason built to run his own Notion task system.

This skill manages the user's tasks in their Notion **Task Command Center** via the
`claude.ai Notion` MCP tools (`notion-fetch`, `notion-create-pages`,
`notion-update-page`, `notion-update-view`, `notion-update-data-source`, `notion-search`).

## 0. Load config first

All Notion IDs live in **`config.local.json`** (git-ignored, machine-specific).

1. Read `config.local.json` in this skill's directory.
2. If it's missing, copy `config.example.json` → `config.local.json` and ask the user to
   fill in their IDs — or offer to discover them by `notion-search` for
   "Task Command Center" and reading the page's child databases.

Never commit `config.local.json`. The committed `config.example.json` holds placeholders only.

## 1. The well-formed-task framework (apply to EVERY task you create)

A good task is: **outcome-first · atomic · action-oriented · context-complete · measurable.**

- **Title** = verb + object, one atomic action. If it needs the word "and", split it.
- Set the **Done-when** property — a testable success criterion.
- In the page **body**, fill: 🎯 Outcome · 📥 Inputs · 🚧 Constraints. Link prerequisites
  via the **Depends on** relation.

Full body template and worked examples: `reference/well-formed-task.md`.
When the user hands you a rough task ("I need to do X"), upgrade it into this shape — ask
only for what you genuinely can't infer.

## 2. Daily ritual

- **Morning** — triggers: "good morning", "daily update", "plan my day".
- **Evening** — triggers: "end of day", "wrap up", "evening review".

Exact step-by-step (including refreshing the Today view's date): `reference/daily-ritual.md`.
Summary:

- **Morning:** refresh the **Today & Overdue** view filter to today's date; pull tasks
  due ≤ today & not Done; propose an ordered plan; create today's **Daily Log** entry with a
  Morning Plan section.
- **Evening:** mark finished tasks **Done**; roll incomplete ones to tomorrow (update **Due**);
  fill the **End-of-Day Review** in today's Daily Log; set **Tasks Done** + **Mood**.

## 3. Adding & importing tasks

- **One task:** create it well-formed (section 1).
- **Import from Todoist:** the user pastes their list or a CSV (the Todoist MCP only exposes a
  UI widget here — there is no readable task tool, so import is always a manual paste). Bulk
  `notion-create-pages` into the Tasks data source, mapping: `p1..p4` → `P1..P4`, due date →
  **Due**, project/label → **Project**, and infer a **Done-when** where obvious.

## 4. Schema & gotchas

Tasks data source properties:
`Task` (title) · `Status` (Not started / In progress / Done) · `Priority` (P1–P4) ·
`Project` (Inbox / Work / Personal / Errands) · `Due` (date) · `Notes` (text) ·
`Done-when` (text) · `Depends on` ↔ `Blocks` (dual self-relation).

- **Dates:** use expanded props — `date:Due:start`, `date:Due:end`, `date:Due:is_datetime`.
- **Relations:** value is a JSON array of related page URLs, e.g. `"[\"https://app.notion.com/p/…\"]"`.
- **Today view has no auto-"today":** the view DSL rejects the `today` keyword, so each morning
  update the filter with a literal date via `notion-update-view`:
  `FILTER "Due" <= "YYYY-MM-DD"`.
- **View DSL limits:** no relative-date keywords; `status`-type sub-filters silently drop;
  for self-relations, add ONE side only (two `DUAL` statements create duplicate columns).
- **Checkbox values** in updates use `__YES__` / `__NO__`; properties literally named `id`/`url`
  need a `userDefined:` prefix.
