---
name: update-action-items
description: Update action items in a recently logged meeting file. Use when the user gives status updates on action items (done/pending/blocked), corrects a name, or adds a note to a previously logged meeting.
---

When this skill is invoked, do the following in order.

## 1. Identify the target meeting file

- If the user specifies a meeting or file, use that.
- Otherwise, find the **most recently modified** `.md` file across these folders:
  - `Initiatives/PFM - Initiatives/`
  - `KT/KT receiving /`
  - `Company Level Context/Conversations/`
- Confirm the file with the user before making changes if it is not obvious.

## 2. Read the file

- Open the file and read the full **Action Items** section.
- Number each action item in your head (1, 2, 3…) in the order they appear — the user will refer to them by number.

## 3. Parse the user's updates

The user will give freeform input. Map each piece to one of these update types:

| User says | What to do |
|-----------|-----------|
| "done" / "did this" / "I did" | Mark checkbox `[ ]` → `[x]` |
| "need to do" / "pending" / "not done" | Leave `[ ]` as is; add note if given |
| "blocked" | Leave `[ ]`; append `— Blocked: [reason]` to the line |
| "Ishan not Ian" / name correction | Replace the wrong name throughout the file |
| "discuss with X in next call" | Append `— discuss with [X] in next call` to the action item line |
| "deferred" | Append `— Deferred` to the line |
| Skipped item (no mention) | Leave unchanged |

## 4. Apply all updates to the file

- Edit the meeting file with all changes in one pass.
- If a name correction was given (e.g. "Shavia" → "Srinivas"), replace it **throughout the entire file**, not just in action items.
- Do not change any other content in the file.

## 5. Propagate corrections if needed

If a **name correction** was made:
- Check if that wrong name appears in any related initiative or context files that were updated during the same `/log-meeting` session.
- Fix it in those files too.
- List every file touched.

## 6. Confirm what changed

Tell the user:
1. Which action items were updated and how
2. Any name corrections applied and in which files
3. Items still open that need attention

---

## Quick reference

- User refers to items by number → map to order in Action Items section
- Name corrections propagate to the whole file and related files
- One pass, no back-and-forth unless the target file is ambiguous
- **Frontmatter:** If the file being edited lacks frontmatter, add it before making other changes — use the meeting template in `CLAUDE.md`
