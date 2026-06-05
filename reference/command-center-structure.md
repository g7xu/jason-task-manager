# The Task Command Center — expected structure

This is what the Notion **Task Command Center** should look like. Use it to **verify** the setup,
**repair** anything missing, or **rebuild from scratch** (then write the new IDs into
`config.local.json`). All IDs come from `config.local.json`.

## Page tree

```
📋 Task Command Center  (page — command_center_page_id)
├── Intro + "🔁 Daily ritual" + "✍️ Anatomy of a well-formed task" guidance
├── 📋 Tasks      (database, INLINE — tasks_database_id / tasks_data_source_id)
│      tabs: Board · List · Calendar · Today & Overdue · (Default table)
└── 🌙 Daily Log  (database — daily_log_database_id / daily_log_data_source_id)
```

> ⚠️ Tasks is **inline** on the Command Center page (Jason's choice) — it may need a one-time
> tab-nudge to paint the board on load. Do **not** replace it with an API-created linked-view embed
> (those crack). The working **Board** is Jason's UI-made *by-option* view. See SKILL.md §5.

## Tasks database

**Properties**

| Property | Type | Notes |
| --- | --- | --- |
| `Task` | title | verb-led, atomic |
| `Status` | status | `Not started` / `In progress` / `Done` |
| `Priority` | select | `P1` red · `P2` orange · `P3` blue · `P4` gray |
| `Project` | select | `Inbox` · `Work` blue · `Personal` green · `Errands` yellow |
| `Due` | date | deadline |
| `Notes` | text | freeform |
| `Done-when` | text | measurable success criteria (shown on cards) |
| `Depends on` ↔ `Blocks` | relation | dual self-relation = dependencies |

**Views**

| View | Type | Config |
| --- | --- | --- |
| Board | board | group by `Status`, sort `Priority` ASC, show Priority/Project/Due/Done-when |
| List | list | sort `Due` ASC, show Status/Priority/Project/Due/Done-when |
| Calendar | calendar | by `Due` |
| Today & Overdue | list | `FILTER "Due" <= "<today>"`, sort `Priority` ASC (date refreshed each morning) |
| Default | table | all properties |

The Board and List views also carry
`FILTER "Task" != "🧱 Template — Well-formed task (duplicate me)"` so the template row is hidden.

**Template row** — a regular row titled `🧱 Template — Well-formed task (duplicate me)` whose body
holds the 🎯 Outcome / 📥 Inputs / 🚧 Constraints / 🔗 Dependencies / ✅ Done-when sections (see
`reference/well-formed-task.md`). Native Notion templates can't be created via the API, so this is
a duplicate-me row; the user may convert it to a real default template in the UI.

## Daily Log database

**Properties:** `Log` (title, e.g. "Wed, Jun 4 2026") · `Date` (date) · `Tasks Done` (number) ·
`Mood` (select: `On track` green / `Behind` orange / `Blocked` red).

**Body of each entry:** a `☀️ Morning Plan` section and a `🌙 End-of-Day Review` section. One entry
per day — always check for an existing entry before creating one.

## Rebuilding from scratch

If the page/databases don't exist:

1. `notion-create-pages` → the Command Center landing page.
2. `notion-create-database` → Tasks and Daily Log with the schemas above.
3. `notion-create-view` → the Tasks views (Board/List/Calendar/Today & Overdue). Keep the database
   **full-page** (not inline, no API-created linked embeds) — those render unreliably; the user
   clicks into Tasks from the landing page. Board views must have **no sort** (so cards can drag).
4. Create the template row.
5. Write every new ID into `config.local.json`.

> When adding the `Depends on` self-relation, add **one** side only — two `DUAL` statements create
> duplicate columns that then need cleanup.
