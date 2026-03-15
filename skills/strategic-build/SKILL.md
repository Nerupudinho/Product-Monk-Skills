---
name: strategic-build
description: Evaluate whether something is worth building. Applies LNO framework (Leverage/Neutral/Overhead), Three Levels of Product Work (Impact/Execution/Optics), Pre-Mortem, and Feature vs Empowered Team framing. Use when the user asks "should I build this?", is evaluating a feature request, making architectural decisions, or wants to distinguish high-impact from busy-work.
---

When this skill is invoked, apply the following frameworks in order to evaluate the work item or decision at hand.

---

## 1. Understand the Request

Ask (or infer) what the user is evaluating:
- A feature or initiative to build
- An architectural/technical decision
- A work request from a stakeholder
- Prioritisation between options

---

## 2. Apply the Four Frameworks

### Framework 1: LNO (Leverage / Neutral / Overhead)

Classify the work:

| Type | Definition | Ratio Target |
|------|-----------|-------------|
| **Leverage** | Compounds over time; enables future work; reused 10+ times | 70% |
| **Neutral** | Maintains current state; one-time impact | 20% |
| **Overhead** | Busy-work; "product theater"; process for process's sake | ≤10% |

Ask:
1. Will this be used 10+ times? → Leverage candidate
2. Does it unblock future work? → Leverage candidate
3. Is this maintaining vs building? → Likely Neutral
4. Does it just "look like PM work"? → Overhead — avoid

**Rule of thumb for reusability:** Build specific for the first 2 use cases. Refactor into a shared component at the 3rd.

---

### Framework 2: Three Levels of Product Work

| Level | Focus | Failure Mode |
|-------|-------|-------------|
| **Level 1 — Impact (Why)** | What outcome matters? Success metric? | Building without clear success criteria |
| **Level 2 — Execution (How)** | Technical approach, quality bar | Great execution on the wrong problem |
| **Level 3 — Optics (Perception)** | Stakeholder comms, status updates | Theater — looks good but no impact |

**Critical rule:** Validate Level 1 (Impact) before optimising Level 2 (Execution). Most teams skip this.

---

### Framework 3: Pre-Mortem

Prompt the user to imagine failure:
> "It's 6 months from now. This completely failed. Why?"

Steps:
1. Brainstorm all failure reasons
2. Identify top 3 risks
3. Define mitigation for each
4. Decide: Build / Redesign / Skip

---

### Framework 4: Feature Team vs Empowered Team

| Feature Team (avoid) | Empowered Team (aim for) |
|---------------------|------------------------|
| Given features to build | Given problems to solve |
| Success = shipped on time | Success = outcome achieved |
| PM is project manager | PM discovers solutions |
| Roadmap = list of features | Roadmap = list of outcomes |

If the request smells like a feature team ask, reframe: **feature request → user problem**.

---

## 3. Decision Tree

```
DECISION: Should I build this?
│
├─ LNO: Is this Leverage? ──YES──────────────────→ PRIORITIZE
├─ LNO: Is this Overhead? ──YES──────────────────→ SKIP
├─ LNO: Is this Neutral? ───YES─────────────────→ (continue)
│
├─ Level 1 (Impact) clear? ──NO─────────────────→ PAUSE & DEFINE
├─ Level 1 clear ────────────YES────────────────→ (continue)
│
├─ Pre-mortem: Top risks mitigated? ──NO────────→ REDESIGN
├─ Risks acceptable ──────────────────YES───────→ (continue)
│
├─ Problem-focused framing? ──YES───────────────→ BUILD
└─ Feature-focused framing? ──YES───────────────→ REFRAME AS PROBLEM FIRST
```

---

## 4. Output Templates

### LNO Assessment

```markdown
# Work Item: [Name]

## LNO Classification
- [ ] Leverage — compounds, enables future work
- [ ] Neutral — necessary, one-time impact
- [ ] Overhead — busy-work, avoid

## Evidence
- Times it will be used: [number]
- Future work it enables: [list]
- Business impact if skipped: [high / medium / low]

## Decision
- Priority: [High / Medium / Low]
- Rationale: [LNO reasoning]
```

### Three Levels Check

```markdown
# Feature: [Name]

## Level 1: IMPACT (Why)
- Problem: [describe]
- Success metric: [specific number]
- Business outcome: [revenue / retention / acquisition]
- ✓ Clear? [yes / no — if no, stop here]

## Level 2: EXECUTION (How)
- Technical approach: [describe]
- Quality bar: [standards]
- Timeline: [estimate]
- Only proceed if Level 1 is clear

## Level 3: OPTICS (Communication)
- Stakeholders: [list]
- Update cadence: [frequency]
- Launch story: [narrative]
```

### Pre-Mortem

```markdown
# Pre-Mortem: [Feature Name]

Scenario: It's 6 months from now. This completely failed.

## Why It Failed (Brainstorm)
1.
2.
3.
4.
5.

## Top 3 Risks + Mitigations
1. Risk: [most likely] → Mitigation: [how to prevent]
2. Risk: [second] → Mitigation:
3. Risk: [third] → Mitigation:

## Go/No-Go
- [ ] Risks acceptable and mitigated
- [ ] Still confident in approach
- Decision: [Build / Redesign / Skip]
```

---

## 5. Red Flags (Stop & Reassess)

- Can't articulate the "why" (Level 1 unclear)
- Building because a stakeholder wants it, not because of a user problem
- No clear success metric
- Feels like busy-work / product theater

---

## Key Principles

> "Not all tasks are created equal. Some compound (Leverage), some maintain (Neutral), some drain (Overhead)." — Shreyas Doshi

> "Most execution problems are actually strategy problems." — Shreyas Doshi

> "If you're just delivering output, you're a project manager. Product managers deliver outcomes." — Marty Cagan

> "Do pre-mortems when you can still change course, not post-mortems when it's too late." — Shreyas Doshi
