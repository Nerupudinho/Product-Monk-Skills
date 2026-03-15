---
name: update-open-items
description: Update Open Items.md with status changes, new questions/actions, or resolved items. Use when the user says something was done, adds a new open item, or changes the status of an existing item.
---

When this skill is invoked, do the following in order.

## 1. Read the file

Open `Open Items.md` and read it fully. Note the product sections (Repeat, PFM, Business Loans) and subsections within each:
- **Ask Harsh This Week** — questions to clarify in KT
- **Ganesh Actions** — table with `# | Action | With | Status`
- **Rishabh (Analyst) Asks** — data build requests
- **Other Owners** — actions owned by others
- **Open Questions** — questions without a clear owner yet
- **Resolved** — bullet list of completed items

---

## 2. Parse the user's input

Map each piece of freeform input to an operation:

| User says | Operation |
|-----------|-----------|
| "X was done" / "did X" / "completed" | Mark done (see §3) |
| "add X as open question / action" | Add new item (see §4) |
| "blocked on X" | Update status column to `Blocked — [reason]` |
| "deferred" / "not doing this" | Update status column to `Deferred` |
| "reassign to [person]" | Update the With/Owner column |
| "add note: [text]" | Append note to the action text |

If the product section is ambiguous, ask before editing.

---

## 3. Marking an item done

When an item is marked done:

**In the table row:**
- Strikethrough the action text: `~~action text~~`
- Change Status column to: `✅ Done`

**In the Resolved section** (same product):
- Add a new bullet: `- ✅ [Short description] — [date if known]`

Example:
```
| 13 | ~~Get Firebase access (requested 3 Mar; Pankaj to share)~~ | Pankaj | ✅ Done |
```
```
- ✅ Firebase access — received (10 Mar)
```

---

## 4. Adding a new item

**New open question** → add to the product's `### Open Questions` table (create the subsection if it doesn't exist):
```
| # | Question | Who to ask |
|---|----------|-----------|
| N | [question] | [person] |
```

**New Ganesh action** → add to `### Ganesh Actions` table with Status `Open`:
```
| N | [action] | [person / —] | Open |
```

**New ask for Rishabh (analyst)** → add to `### Rishabh (Analyst) Asks` with Status `To build` or `To find`.

**New other-owner action** → add to `### Other Owners`.

Always renumber rows within the subsection if inserting mid-table.

---

## 5. Update the "Last updated" line

Change line 3 to: `Last updated: [today's date]`

---

## 6. Confirm what changed

Tell the user:
1. Each item updated and what changed (done / added / status change)
2. If anything was added to Resolved
3. Any items still open that seem time-sensitive

---

## Quick reference

- Target file is always `Open Items.md` at the repo root
- Done = strikethrough in table + bullet in Resolved
- New question → Open Questions subsection; new action → Ganesh Actions
- Always update the Last updated date
- One pass — do all changes in a single edit
