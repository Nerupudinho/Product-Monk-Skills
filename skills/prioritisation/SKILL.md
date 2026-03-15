---
name: prioritisation
description: Run daily task prioritisation — go through the current task list, collect status for each task one by one, then write an updated Tasks file. Use when the user wants to prioritise their day or update task statuses.
---

When this skill is invoked, do the following in order.

## 1. Find the latest task file

- Look in the **`Tasks/`** folder.
- **Date task files** = files whose names match **`YYYY-MM-DD.md`** (e.g. `2026-03-06.md`). Ignore other files (e.g. Work Log.md, Daily Todo List.md, Planner.mdc).
- **Latest** = among those, the file with the largest date. With YYYY-MM-DD naming, sort by filename descending and take the first (e.g. `2026-03-06.md` is latest before `2026-03-03.md`).
- The **content** inside the file may still use a human-readable header (e.g. `# Tasks - 6 Mar 2026`); only the **filename** is YYYY-MM-DD.
- If the folder has no `YYYY-MM-DD.md` file, say so and stop.

## 2. Parse the task list

- Open that file and read the **Prioritized Task List** table.
- Extract every **task row** (table rows with data).
- **Skip**: the header row and any row where the first column is `—` (those are already closed/handled).
- For each remaining row, treat it as one task (use **Initiative/Topic** and a short **Action Required** summary as the label).

## 3. Go through each task one by one

For **each** task:

1. **Show the task**: briefly state the initiative/topic and the action (e.g. 1–2 lines).
2. **Ask for status** and give **exactly these options** (so the user can pick one, e.g. by number or name):

   - **Done** – Completed / handled today.
   - **In progress** – Actively working on it.
   - **Pending** – Not started yet.
   - **Blocked** – Waiting on someone/something.
   - **Deferred** – Not doing today; deprioritised.
   - **Cancelled** – No longer doing this.

3. **Wait for the user's choice** before moving to the next task. Do not assume or skip.
4. **Record** the chosen status for that task (in memory or a small list) and then go to the next task.

Process **one task per message** so the user can click or type one option at a time. Do not ask status for multiple tasks in the same message.

## 4. After all tasks are done

- **Get today's date** from the system and express it as **YYYY-MM-DD** (e.g. 2026-03-06). Use it to decide where to write.
- **Compare dates**: Is today's date (YYYY-MM-DD) the **same** as the date in the latest task file's filename (e.g. `2026-03-06.md` → 2026-03-06)?
  - **Same date** → Update **the same file** (`Tasks/<latest>.md`).
  - **Different date** → **Create a new file** `Tasks/YYYY-MM-DD.md` for today (e.g. `Tasks/2026-03-06.md`) and write the updated content there. Do not overwrite the older file.
- **Apply the prioritization rule** when writing the file: **read and follow** `.cursor/rules/prioritization.mdc`. Use: (1) the exact **Priority Framework Applied** line from the rule: `Production risk > Sprint dependency > Leadership visibility > Reputation/compliance > Handover enablement > Admin hygiene > Exploration`; (2) the rule's **category labels** in Notes/Priority (Production Risk, Reputation/Compliance, Handover Enablement, Admin Hygiene, etc.) with category + reason for rank + time constraint; (3) **Hard time constraints** (or "None specified" + brief time map); (4) the rule's **output format** (table structure, verb-first Action Required).
- **Apply status updates** (in the file you chose above):
  - For **Done** / **Cancelled**: move the row to the bottom of the table (or the "handled" section if present), set the `#` column to `—`, and in Action Required or Notes add ~~strikethrough~~ and a note like "Handled" / "Closed" / "Cancelled" plus today's date if useful.
  - For **In progress** / **Pending** / **Blocked**: keep the row in the main list and add or update the Notes/Priority column with the status (e.g. "In progress", "Blocked – waiting on X").
  - For **Deferred**: either move to a "Deferred" section at the bottom or mark clearly in Notes as "Deferred" and optionally remove from the active numbered list.
- Structure is defined by the prioritization rule; preserve "Priority Framework Applied" / "Hard time constraints" sections.
- Write the updated content to the correct file (same file if same date, new file if different date). The final file must conform to `.cursor/rules/prioritization.mdc` (priority order, category labels, structure).

## 5. Quick reference

- **Task folder**: `Tasks/`
- **Date task files**: `YYYY-MM-DD.md` (e.g. `2026-03-06.md`). Latest = first when sorted by filename descending.
- **One task per message**, then wait for user to pick a status.
- **Status options**: Done | In progress | Pending | Blocked | Deferred | Cancelled.
- **Then**: get today's date as YYYY-MM-DD; same date → update that file; different → create new `Tasks/YYYY-MM-DD.md`. **When writing the file, apply** `.cursor/rules/prioritization.mdc` (framework, categories, format).
- **Frontmatter:** Add to every task file created or edited — use the task file template in `CLAUDE.md`
