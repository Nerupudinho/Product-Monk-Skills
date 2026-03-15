---
name: meeting-prep
description: Prepare for an upcoming meeting. Given a person and topic, read relevant context and create a structured prep doc with alignment questions, current state, and specific asks. Use when the user says "I have a meeting with X about Y" or "help me prep for X".
---

When this skill is invoked, do the following in order.

---

## 1. Understand the meeting

Ask the user (or infer from their message):
- **Who** is the meeting with?
- **What topic** will be covered?
- **When** is it? (to name the file correctly)
- **What is the goal?** — alignment, decision, update, ask, or relationship-building?

If the user's message already has enough context, proceed without asking.

---

## 2. Load relevant context

Read these files every time:
- `Company Level Context/About Ganesh.md` — role, stakeholders, transition context
- `Open Items.md` — open questions and actions relevant to this person/topic

Then, based on the topic, read the relevant product and initiative files:

| Topic | Files to read |
|-------|--------------|
| Repeat | `Company Level Context/Products/Repeat.md`, `Initiatives/Repeat - Initiatives/Context.md`, `Initiatives/Repeat - Initiatives/Roadmap & Opportunity.md` |
| PFM | `Company Level Context/Products/PFM.md`, `Initiatives/PFM - Initiatives/Context.md`, `Initiatives/PFM - Initiatives/Roadmap & Opportunity.md` |
| Business Loans | `Company Level Context/Products/Business Loans.md`, `KT/KT receiving /Business Loans/Context.md` |
| 1:1 with manager (Ishan) | Read the most recent file in `Company Level Context/Conversations/Meet with Ishan/` |
| Cross-functional / stakeholder | Read the most recent file in `Company Level Context/Conversations/` matching that person |

Also check if a prior meeting file exists for this person — if yes, read it to understand what was last discussed.

---

## 3. Determine the file path

Save the prep doc to:

| Person type | Target folder |
|-------------|--------------|
| Ishan (manager) | `Company Level Context/Conversations/Meet with Ishan/` |
| Any named stakeholder | `Company Level Context/Conversations/[Person name]/` |
| KT session | `KT/KT receiving /[Product]/` |

File naming: `[D MMM YYYY].md` inside the person's folder.
If the folder doesn't exist, create it.

---

## 4. Write the prep doc

Structure:

```
# Meeting with [Person] — [D MMM YYYY]

**Agenda:** [topic]
**Goal:** [what success looks like]

---

## 1. Align First

[3–5 questions Ganesh wants to ask to understand the other person's view before presenting his own]

---

## 2. Current State

[The most relevant data or status summary — keep it short, max 1 table or 3–4 bullets. Only include what's directly relevant to this meeting topic.]

---

## 3. Active Initiatives to Reference

[2–3 bullet points on relevant active work, with status. Don't repeat Current State.]

---

## 4. Opportunities / Topics to Raise

[Numbered list of things Ganesh wants to discuss or get input on. Group as "decisions needed" vs "FYI" if helpful.]

---

## 5. Specific Ask from [Person]

[What Ganesh needs from this person specifically — access, decision, context, unblocking, etc.]

---

## Post-call

- [ ] [Action 1 to follow up on]
- [ ] [Action 2]
```

---

## 5. Highlight open items for this person

After writing the doc, scan `Open Items.md` for any existing open questions or actions involving this person. List them at the bottom of the prep doc under:

```
## Open Items to Close

| # | Item | Status |
|---|------|--------|
| ... | ... | ... |
```

Only include items directly relevant to this meeting.

---

## 6. Confirm what was done

Tell the user:
1. Where the prep doc was saved
2. Top 2–3 things to lead with in the meeting
3. Any open items from `Open Items.md` that this meeting is a good opportunity to close

---

## Quick reference
- **Frontmatter:** Add to every prep doc created — use the prep doc template in `CLAUDE.md`
