---
name: plan-day
description: Plan the day by combining Google Calendar events with the current task list. Applies the recurring meetings guide to decide what to attend/skip, maps tasks to time blocks, and generates three files — today's task file (Overdue/Due Today/In Progress), this-week.md, and next-week.md. Use when Ganesh wants a day plan or asks "what's my day looking like".
---

When this skill is invoked, do the following in order.

## 1. Read the latest task file

- Look in `Tasks/` for the latest `YYYY-MM-DD.md` file (sort descending, take first).
- Read the **Prioritized Task List** — extract all active tasks (rows where `#` is not `—`).
- Note today's date as **YYYY-MM-DD** from system context.

## 2. Fetch today's calendar

- Use the Google Calendar MCP tool: `gcal_list_events`
- Parameters: `timeMin = YYYY-MM-DDT00:00:00`, `timeMax = YYYY-MM-DDT23:59:59`, `timeZone = Asia/Kolkata`
- Collect all events: summary, start time, end time, myResponseStatus, organizer, numAttendees.

## 3. Apply the recurring meetings guide

For each calendar event, apply the rules below to decide **Attend / Skip / On demand**. Do NOT ask Ganesh about recurring meetings — these decisions are known.

| Meeting (by summary pattern) | Decision | Notes |
|------------------------------|----------|-------|
| PL - Daily Standup | ✅ Attend | Need funnel + BAU/MAU data ready. Manoj sometimes joins. |
| Analytics Catchup | ✅ Attend | Ishan + Rishab (analyst). Flag any dashboard asks for Rishab. |
| GBT Scrum | ⚠️ On demand | Skip unless specific GBT work. Only if Srinivas needs Ganesh. |
| PFM - Daily Standup | ✅ Attend | Ganesh's team from Mar 2026. |
| CKYC Updates | ✅ Attend | Daily production call until stable. |
| Catchup (organiser = ishan.tayal) | ✅ Attend | 1:1 with manager. High priority. |
| KT (organiser = harsh.katare) | ✅ Attend | Incoming PFM KT. Clarify KT questions. |
| Daily Standup IM <> MV | ❌ Skip | Indmoney standup. Sasi's domain. |
| CrossPOD Sprint Items / BB Standup | ⚠️ On demand | DP-related. Skip unless live DP sprint item. |
| Daily Standup — Demand Partners | ⚠️ On demand | DP wind-down. Sasi to own. |
| DP Sprint Planning | ⚠️ Context-only | Join only to hand context to Sasi. Keep short. |
| PWA Partner Journeys | ❌ Skip | Sasi's domain. DP legacy. |
| MV changes UAT (Airtel/external) | Check status | Verify if already declined. If declined, skip. |
| Demand Partner - Product Brainstorming | ✅ Attend | Likely Sasi KT/handover call. |
| Lunch | — | Block; do not schedule over. |
| Democratising Querying Catchup | ✅ Attend | Quick 15 min. Attend. |

For any **new or unrecognised** meeting (not in the table above), include it and mark as `❓ Check` — let Ganesh decide.

## 4. Identify hard time constraints and prep needs

- Hard time constraints = meetings Ganesh will attend, sorted by time.
- For each attended meeting, note any **prep needed**:
  - PL Daily Standup → check Repeat funnels + daily BAU + monthly MAU/RVA gap before joining
  - Analytics Catchup → check if any dashboard asks to flag for Rishab
  - Ishan 1:1 → prepare talking points / updates
  - KT with Harsh → consolidate and bring KT questions
  - CKYC Updates → note status and any action items to broadcast

## 5. Map tasks to time blocks

- Anchor the day around confirmed meetings.
- Fill gaps between meetings with task work:
  - Morning (pre-standup) → standup data prep
  - Post-standup gap → deep work (PFM KT, roadmap review, etc.)
  - Lunch → no tasks
  - Post-CKYC → focus blocks (roadmap, OKRs)
  - Evening → admin hygiene (OKRs, Darwin Box)
- Flag any **conflicts** (two meetings at the same time) and note which one to attend based on the guide above.

## 6. Categorize tasks into three buckets

Before writing the task file, classify every active task into one of three buckets:

### Overdue
Tasks that have a deferred date in the Notes column (e.g. "⏳ Mon 16 Mar") **where that date is before today**. These were scheduled for an earlier day and not done.

### Due Today
Tasks that meet any of these conditions:
- Marked `🔄 In progress today` in the Notes column
- Have a deferred date that matches today (e.g. "⏳ Mon 16 Mar" when today is 16 Mar)
- Priority = **Production risk** or **Sprint dependency** AND require an action today (not just monitoring)

### In Progress Initiatives
Everything else — active ongoing work, monitoring tasks, future-deferred items, items blocked on something else.

Completed tasks (✅) go into a separate **Completed** section at the bottom, same as before.

---

## 7. Present the day plan

Output two things:

### A. Calendar at a glance (table)

| Time | Event | Attend? | Prep needed |
|------|-------|---------|-------------|
| HH:MM–HH:MM | Event name | ✅ / ❌ / ⚠️ | Prep note or — |

### B. Suggested focus blocks (narrative)

Short bullet list of what to do in the gaps between meetings.

---

## 8. Write the task file

Write (or update) `Tasks/YYYY-MM-DD.md` using the structure below. Use today's date if the file doesn't exist.

```
---
date: YYYY-MM-DD
status: in-progress
---

# Tasks - DD Mon YYYY

## Hard time constraints today

| Time | Meeting |
|------|---------|
...

**Time map:** [short narrative of day shape]

---

## Overdue

| - [ ] | # | Initiative/Topic | Action Required | Stakeholders | Notes/Priority | My Updates | Need Clarity | Initiative File |
|-------|---|---|---|---|---|---|---|---|
...

---

## Due Today

| - [ ] | # | Initiative/Topic | Action Required | Stakeholders | Notes/Priority | My Updates | Need Clarity | Initiative File |
|-------|---|---|---|---|---|---|---|---|
...

---

## In Progress Initiatives

| - [ ] | # | Initiative/Topic | Action Required | Stakeholders | Notes/Priority | My Updates | Need Clarity | Initiative File |
|-------|---|---|---|---|---|---|---|---|
...

---

## Completed

| ✅ | Initiative/Topic | Done date | Stakeholders | Notes | Initiative File |
|---|---|---|---|---|---|
...
```

Rules:
- Every task row starts with `- [ ]` as the first column — a checkbox Ganesh can tick off.
- **My Updates** column is always blank when the file is first written — Ganesh fills it in.
- **Need Clarity** column is always blank when the file is first written — filled in by the AI (see Step 8b).
- Overdue tasks keep their original row content — do not rewrite them.
- Do NOT change any task content — only reclassify into the right section.
- If Overdue is empty, omit the section header.
- Numbering (#) restarts from 1 within each section.

---

## 8b. Process "My Updates" (run when the task file already has updates)

When reading a task file that has content in the **My Updates** column, do the following for each populated row:

### Step 1 — Propagate to initiative file
- Identify the initiative file from the **Initiative File** column of that row.
- Open the initiative file and append the update as a dated note at the bottom under a `## Updates` section (create it if missing):
  ```
  **[DD Mon YYYY]:** [Ganesh's update text]
  ```
- Do not rewrite or summarise — preserve Ganesh's exact words.

### Step 2 — Populate "Need Clarity"
- Read the update and the task context (Action Required + Notes/Priority).
- If anything is ambiguous, incomplete, or raises a question that would affect the next action — write a short, specific question in the **Need Clarity** column of that same row.
- If the update is fully clear, leave **Need Clarity** blank.
- Keep questions tight — one question per row maximum.

### Step 3 — Confirm
After processing all updates, tell Ganesh:
1. Which initiative files were updated and what was appended
2. Which rows have a "Need Clarity" question and what it is

## 9. Generate `Tasks/this-week.md`

Fetch this week's calendar (Monday–Friday of the current week):
- `timeMin = [this Monday]T00:00:00`, `timeMax = [this Friday]T23:59:59`, `timeZone = Asia/Kolkata`

Then write `Tasks/this-week.md` using this format:

```
# This Week — DD Mon–DD Mon YYYY

## Monday DD Mon
**Meetings:** [list attended meetings, HH:MM name]
**Tasks:** [tasks deferred/assigned to this day]

## Tuesday DD Mon
**Meetings:** ...
**Tasks:** ...

## Wednesday DD Mon
...

## Thursday DD Mon
...

## Friday DD Mon
...

---

## Anytime This Week
[Tasks with no specific day assigned but clearly belong this week — production risk, sprint items, high-visibility work]
```

Rules:
- Only list meetings Ganesh will **attend** (apply recurring meetings guide).
- Tasks go under a day if their Notes column has a deferred date matching that day.
- Tasks with no day anchor but high priority go under **Anytime This Week**.
- If a day has no meetings and no tasks, show it as `*(no tasks)*`.
- File name is always `Tasks/this-week.md` — overwrite on each run.

---

## 10. Generate `Tasks/next-week.md`

Fetch next week's calendar (Monday–Friday of next week):
- `timeMin = [next Monday]T00:00:00`, `timeMax = [next Friday]T23:59:59`, `timeZone = Asia/Kolkata`

Then write `Tasks/next-week.md` using this format:

```
# Next Week — DD Mon–DD Mon YYYY

## Confirmed Next Week
[Tasks with Notes column containing "next week" or a date in next week's range]

| # | Initiative/Topic | Action Required | Stakeholders | Notes/Priority | Initiative File |
|---|---|---|---|---|---|
...

## Calendar (next week)
[Meetings already in calendar for next week — just a simple list by day]
| Day | Time | Event |
|-----|------|-------|
...

## Likely Carry-Forward
[In Progress Initiatives that are multi-week and will likely continue — do not invent, only include items clearly ongoing]
```

Rules:
- File name is always `Tasks/next-week.md` — overwrite on each run.
- **Confirmed Next Week** = tasks with explicit next-week deferral dates only. Do not guess.
- **Likely Carry-Forward** = copy the In Progress Initiatives section header and task count only — do not duplicate full rows.

---

## Quick reference

- Calendar tool: `gcal_list_events(timeMin, timeMax, timeZone="Asia/Kolkata")`
- Task folder: `Tasks/YYYY-MM-DD.md`
- Weekly files: `Tasks/this-week.md`, `Tasks/next-week.md` (overwritten each run)
- Recurring meetings guide: apply from this skill's table — do not ask Ganesh about known recurring meetings
- Output: calendar table + focus blocks + today task file (3 sections) + this-week.md + next-week.md
- Overdue = deferred date has passed | Due Today = in-progress today + deferred-to-today + top-priority actions | In Progress = everything else
- **Frontmatter:** Add to every file written — use the task file template in `CLAUDE.md`
