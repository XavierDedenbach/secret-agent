# Subtask interview (shared)

Used by `notion-weekly-plan-personal` and `notion-weekly-plan-professional` at step 4.

---

## Mental checklist

Track every goal and sub-task as **open / captured / TBD**. Update from **every** owner message before asking the next question.

Default: **one question at a time**, but only for items still genuinely open after parsing the latest message.

---

## Interpreting owner responses

Owners rarely answer one sub-task at a time. Parse generously — do **not** re-ask what they already said.

| Pattern | What to do |
|---------|------------|
| **Multi-goal answer** | Extract all goals/sub-tasks covered in one message; mark each captured; continue with the first still-open item (or where the owner says to go). |
| **Skip ahead** ("we're on goal 4") | Trust their pacing. Backfill any missed captures from prior messages, then continue at the goal they named. |
| **Inline sub-tasks** ("the subtasks are X, Y, Z") | Accept the list. Only ask follow-ups for items still vague; do not re-ask for the list itself. |
| **Rich purpose, no sub-tasks** | For habit/behavior goals, purpose + success criteria may be enough. Do not invent sub-tasks unless the owner wants them. |
| **TBD / unspecified** | Record sub-task as TBD; do not block the interview on it. |
| **Correction** ("I told you already") | Re-read the conversation, capture missed answers, acknowledge briefly, move on — never repeat the same question. |
| **Approval** ("approved") | Mark that domain complete; do not re-open interview unless owner requests edits. |
| **Cross-domain item** | If personal plan captured a work action (e.g. "tell team I'm off Monday"), carry it to professional plan — do not re-interview unless details are missing. |

---

## Per sub-task loop

For each goal, for each sub-task (including any the owner already mentioned):

1. Read back the sub-task name (skip if owner just answered it in the same turn).
2. If still open, ask **one** follow-up:
   - Personal: done criteria, date, person, deliverable, habit vs one-time
   - Professional: done criteria, owner, due date, dependency, deliverable link, MOR-###
3. Capture the answer — refine the sub-task bullet in Notion (detail, dates, names, checkboxes, ticket links).

If the owner lists a goal with no sub-tasks and hasn't given enough to execute, ask: **"What are 1–3 concrete sub-tasks for \<goal\>?"** — unless purpose alone is sufficient (habit goals).

If a sub-task is vague ("continue the habit", "make progress"), ask **one** clarifying question unless the owner already defined success in the same or a prior message.

Loop until every goal has at least one concrete sub-task **or** explicit purpose-only treatment, and each non-TBD sub-task has been captured.

---

## Professional-only extensions

Also apply one follow-up per row when the owner adds or updates:

| Section | Example follow-up |
|---------|-------------------|
| **Milestones** | "What's the blocker or next action on **\<milestone\>**?" |
| **Sharks** | "What would turn this shark into a shipwreck this week?" |
| **Shipwrecks** | "What's the recovery action and owner?" |
| **CEO weekly items** | "Timeboxed when — and what does done look like?" |

**Human-first planning (professional):** Fixed order — owner vision for upcoming week (step 2) → retro with Linear last week (step 3) → Linear reconcile this week (step 4a). No Linear or retro before step 2. See `notion-weekly-plan-professional`.

Do not write the Notion page body until subtask interviews (and brief standing-section prompts) are complete. Draft in chat first if helpful.

---

## Review & approve (step 6 — both domains)

Always end each domain session with the Notion link and an explicit approval request:

```markdown
Your <personal|professional> weekly plan for **<M/D> – <M/D>** is ready for review:

**[<page title>](<full Notion URL>)**

Please open the page and reply:
- **"approved"** — plan is locked for the week, or
- **edits** — tell me what to change and I will update Notion.
```

Rules:
- The Notion link is the **last substantive output** of that domain's session.
- Do not consider the skill complete until the owner approves or requests edits.
- If edits requested, update Notion, then **re-send the link** and ask for approval again.
- Optional: include a brief summary table above the link, but the link must always be present.
