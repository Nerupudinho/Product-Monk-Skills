---
name: funnel-update
description: Generate today's Repeat Funnel Update message. Use when the user pastes raw funnel numbers, a screenshot description, or partial data and wants it formatted into the standard Slack-ready Repeat Funnel Update.
---

When this skill is invoked, do the following in order.

---

## 1. Get today's date

Use today's date for the message header: `Repeat Funnel Update: DD-Mon-YYYY`

---

## 2. Read the data the user has provided

The user may provide:
- Raw numbers (pasted text)
- A screenshot / image of the Tableau dashboard
- Partial data (some segments missing)

Extract the following for each segment:

| Segment | Yesterday's Volume | MTD Total Volume | MoM Delta |
|---|---|---|---|
| MVL Repeat | | | |
| iOS Repeat | | | |
| Partner Repeat | | | |
| Combined (MVL + iOS) | | | |
| Combined (MVL + iOS + Partners) | | | |

**Notes on extraction from Tableau dashboard:**
- "Yesterday's volume" = the **T.** column value (volume row) from the dashboard dated T-1
- "MTD Total Volume" = Current Month MTD Avg × days elapsed (or exact MTD if available)
- "MoM Delta" = Current Month MTD − Previous Month MTD (same days)
- Dashboard may be filtered to one segment at a time (e.g. MVL_Repeat) — iOS and Partner data require separate views

---

## 3. Format the output

Use this exact format:

```
Repeat Funnel Update: DD-Mon-YYYY

MVL Repeat:
Yesterday's volume: X Cr
Total Volume: X Cr (+/- X Cr compared to prev month)

iOS Repeat:
Yesterday's volume: X Cr
Total Volume: X Cr (+/- X Cr compared to prev month)

Partner Repeat:
Yesterday's volume: X Cr
Total Volume: X Cr (+/- X Cr compared to prev month)

Combined Repeat (MTD):
MVL + iOS: X Cr
MVL + iOS + Partners: X Cr (+/- X Cr compared to prev month)

Note:
[Blockers or observations — if none provided, leave blank or omit]
```

**For any value you cannot derive from the data provided, write: `Need more information`**

Do not guess or estimate without clearly labelling it as an estimate.

---

## 4. Output the message

- Print the formatted message, ready to copy-paste into Slack
- Below the message, list what data is still missing (if any) and where to get it:
  - iOS / Partner volumes → switch Tableau filter to the respective program
  - Exact MTD total → use the MTD column directly if visible, not a calculated estimate

---

## 5. Ask if the user wants to log it

After outputting the message, ask:
> "Should I log this as today's funnel update entry?"

If yes, save it to `Initiatives/Repeat - Initiatives/Funnel Updates/YYYY-MM-DD.md` with the formatted content.
