---
name: log-meeting
description: Record a meeting transcript into a structured file. Use when the user pastes a meeting transcript, call notes, or standup notes that need to be logged.
---

When this skill is invoked (user pastes a transcript or meeting notes), do the following in order.

---

## 1. Read the transcript

- The user will paste raw transcript text (auto-generated or manual notes).
- Read it fully before doing anything else.

---

## 2. Load company context

Read the following files to understand the product landscape and people:

- `Company Level Context/Products/PFM.md`
- `Company Level Context/Products/Personal Loans (DP).md`
- `Company Level Context/Products/Repeat.md`
- `Company Level Context/Products/Business Loans.md`
- `Company Level Context/About Moneyview.md`

Use this context to:
- Identify the **product/topic** the meeting belongs to (PFM, DP, Repeat, Business Loans, etc.)
- Recognize **people** mentioned (match to known stakeholders)
- Understand **existing initiatives** the discussion relates to

---

## 3. Determine the correct folder and file

Based on the product/topic identified, pick the target folder:

| Topic | Target folder |
|-------|--------------|
| PFM / Money Manager | `Initiatives/PFM - Initiatives/` |
| Demand Partnership / DP | `Company Level Context/Conversations/` |
| Repeat | `Company Level Context/Conversations/` |
| Business Loans | `Company Level Context/Conversations/` |
| KT (knowledge transfer) | `KT/KT receiving /[Product]/` |
| General / cross-functional | `Company Level Context/Conversations/` |
| VPA / MCC categorization | `Initiatives/PFM - Initiatives/VPA - MCC mapping for PFM/` |

File naming convention: `[Topic or Call name] - [D MMM YYYY].md`
Example: `Call with Pankaj - 9 Mar 2026.md`

If a file for this exact meeting already exists, update it instead of creating a new one.

---

## 4. Structure the meeting record

Write (or update) the file with this structure:

```
# [Meeting Title] — [D MMM YYYY]

**Date:** [date]
**Topic:** [topic / initiative]
**Attendees:** [names as mentioned in transcript]
**Source:** Transcript pasted via /log-meeting

---

## Context / Trigger
[1–2 lines on why this meeting happened]

---

## Key Discussion Points
[Bullet list of what was discussed — clean, not verbatim]

---

## Decisions / Alignment
[What was agreed or decided]

---

## Risks / Open Questions
[What was flagged as unclear or risky]

---

## Action Items
- [ ] [Owner]: [action]
- [ ] [Owner]: [action]

---

## Notes
[Anything else worth preserving — quotes, context, tone signals]
```

---

## 5. Update related initiative files

After writing the meeting record, check if any **action items, decisions, or new context** should be reflected in related files:

- **`Initiatives/PFM - Initiatives/Roadmap & Opportunity.md`** — update initiative status, add new opportunities, update dependencies or people
- **`Initiatives/PFM - Initiatives/VPA - MCC mapping for PFM/Meeting Notes.md`** or `Context.md` — if meeting was about VPA/MCC
- **`Company Level Context/Products/[Product].md`** — if meeting changes known product state

Only update a file if the meeting adds genuinely new information. Do not duplicate what's already captured.

---

## 6. Confirm what was done

After writing, tell the user:
1. Where the meeting record was saved (file path)
2. Which other files were updated and what changed
3. Any open action items that need attention

---

## Quick reference

- **Transcript in → structured record out**
- Match product/people against Company Level Context before writing
- One meeting = one file (named by topic + date)
- Always check and update related initiative files after recording
- Action items get a `- [ ] [Owner]:` prefix for easy tracking
- **Frontmatter:** Add to every file created or edited — use the meeting template in `CLAUDE.md`
