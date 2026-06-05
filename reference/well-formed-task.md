# The Well-Formed Task

Every task should satisfy five principles:

1. **Outcome-first** — start from the end state ("…so that ___"). Captured in the body 🎯 Outcome.
2. **Atomic** — one bounded unit of work. If the title needs "and", split into two tasks.
3. **Action-oriented** — the title starts with a verb: *Draft, Email, Review, Call, Fix…*
4. **Context-complete** — the doer has what they need to start:
   - **Inputs** — files, data, links, decisions required up front.
   - **Constraints** — deadline (also the **Due** property), format, budget, length, quality bar.
   - **Dependencies** — what must finish first, set via the **Depends on** relation.
5. **Measurable** — a testable **Done-when** so completion is unambiguous.

## Body template

Use this for the page body of every task (delete the italic hints as you fill them in):

```markdown
### 🎯 Outcome
*The end state this task delivers — the "so that…". One sentence.*

### 📥 Inputs
*What you need before starting: files, data, links, decisions.*
-

### 🚧 Constraints
*Deadline, format, budget, length, quality bar. (Deadline also goes in the Due property.)*
-

### 🔗 Dependencies
*Set the Depends on property to the task(s) that must finish first.*

### ✅ Done-when
*Measurable success criteria. Also copy the one-liner into the Done-when property so it shows on the Board.*
-
```

## Worked example

> **Title:** Draft Q3 marketing budget v1
> **Due:** Jun 12 · **Priority:** P2 · **Project:** Work
> **Done-when:** Sheet with all 6 channels + totals, shared with Sam
> **Depends on:** Finalize headcount plan
>
> 🎯 **Outcome:** Sam can approve Q3 spend by the planning meeting.
> 📥 **Inputs:** last year's actuals, the channel list, finance's $ cap.
> 🚧 **Constraints:** ≤ $50k, delivered as a Google Sheet, by Jun 12.

## Rough → well-formed

When the user gives a vague task, upgrade it. Infer what you reasonably can; ask only for the
genuinely unknowable (usually the Done-when or a hard deadline).

- "sort out the website" → **Fix broken links on the marketing site** · Done-when: *all links
  return 200 in the link-checker* · Inputs: *staging URL, link-checker tool*.
- "follow up with the lawyer" → **Email lawyer re: contract clause 4** · Done-when: *reply
  received confirming the edit* · Inputs: *the draft contract, the specific concern*.
