---
name: notion-weekly-plan-professional
description: >-
  Professional weekly focus dashboard in Notion — owner describes the week first,
  retro with Linear, reconciles due tickets, sets technical/team goals with Purpose,
  interviews sub-tasks, writes Notion page with Daily Focus Journal, ends with link
  for approval. Mid-week: fill tomorrow's journal (top two + stretch). Use for work
  weekly plan, technical goals, team updates, professional replan, sharks/shipwrecks,
  daily focus journal, or tomorrow's focus.
---

# Professional Weekly Plan

Executes the **professional** half of Xavier's Notion focus dashboard. For routing, see [weekly-plan/SKILL.md](../weekly-plan/SKILL.md). For philosophy, see [weekly-plan/philosophy.md](../weekly-plan/philosophy.md).

Shared config: [weekly-plan/notion.yaml](../weekly-plan/notion.yaml) · Templates: [weekly-plan/format-analysis.md](../weekly-plan/format-analysis.md)

State file: `weekly-plan/state/OWNER_GOALS.md`

**Approval rule (non-negotiable):** The owner approves **only** after opening the live Notion page. Chat recaps are not the plan. Never ask “reply approved and I’ll write the page.” If the interview is done, write the page immediately, send the URL, and wait. An “approved” before that URL exists is invalid.

---

## Checklist

```
Professional Weekly Plan:
- [ ] 1. Bootstrap (skip if weekly-plan router already ran)
- [ ] 2. Owner vision — unprompted scope for upcoming week (human speaks first)
- [ ] 3. Retro — last week (Notion page + Linear previous week)
- [ ] 4. Linear reconciliation — this week's due items vs owner goals
- [ ] 5. Plan interview — fill gaps (purpose, ladder, milestones, sharks)
- [ ] 6. Subtask interview — one follow-up per sub-task per goal
- [ ] 7. Write Notion page + OWNER_GOALS.md (always include Daily Focus Journal)
- [ ] 8. Review & approve — send the live Notion URL; owner approves only after opening that page
- [ ] 9. After approval — ask Released, then ask whether to set tomorrow's daily focus
```

**Session order is fixed:** vision → retro → Linear reconcile → gaps → subtasks → write → approve.

Ask **one question at a time** (except step 2, where the owner speaks freely). Target **4–6 goals** under Xavier.

**Do not pull Linear or run retro before step 2 completes.** Early task-level input narrows the owner onto tickets instead of the broader picture they have been thinking about.

**Do not skip step 6.** Do not write the Notion page body until subtask interviews are complete. A chat recap is optional as an interview aid — **never request approval on chat**.

**Do not mark the session complete until step 8.** The only acceptable approval is the owner viewing the Notion page (the URL you send) and then saying approved or requesting edits. If they say the interview is done before the page exists, write the page immediately and send the link — do not wait for a chat "approved."

Shared interview rules: [subtask-interview.md](../weekly-plan/subtask-interview.md)

---

## Step 1: Bootstrap

Skip if OWNER_GOALS.md refreshed today.

1. Goal Tracker query (same as personal skill).
2. Find pages — query `weekly_plan.professional.data_source_id` for last/this week.
3. Load CEO Responsibilities: `Status = Active` AND `Frequency = Weekly` — surface as timeboxed items during planning.

---

## Step 2: Owner vision (human first — upcoming week)

Open with **one** open question — no Linear, no retro, no milestone/shark prompts:

> "What's on your mind for this week's professional plan? Paint the picture — themes, outcomes, what's most important — in your own words."

Rules:
- Let the owner speak freely. Capture goals, themes, priorities, and any sub-tasks they volunteer.
- Do **not** interrupt with clarifying questions until they signal done (or pause clearly).
- Parse generously into a **draft goal list** (titles + any purpose/sub-tasks already stated).

Cross-domain: if personal plan already captured work items (e.g. Monday off), note them — do not re-ask.

---

## Step 3: Retro (last week)

Run **after step 2**, before Linear reconciliation for this week.

### Notion retro

Target: **last week's Professional page** (Aug 3–9 if planning Aug 10–16). If no page exists (gap since Jun 2026), acknowledge and use Linear + owner narrative instead.

1. Under H3 `Xavier`, read numbered items from "Goals for This Week".
2. Per goal ask: "Did you complete **\<title\>**? (✅ / 🆗 / 🛑 / ❌)" + "Anything to capture?"
3. Write grades via `API-update-a-block`. Deferrals: append `🛑 (Deferred to week of M/D)`.
4. Capture "Added during the week" mid-week goals if any.
5. Grade legacy Katie/Jon sections if they exist — do not create new person sections.
6. Log PROFESSIONAL entries to OWNER_GOALS.md Completion Log.
7. Set last week's DB `Pass` to Pass or No Pass when page exists.

### Linear retro (previous week)

Query Linear for issues **assigned to the owner** that were active or due **last calendar week** (completed, in progress, or missed). Use to jog memory and validate grades:

```markdown
Linear last week (assigned to you):
| Linear | Title | Status | Due |
|--------|-------|--------|-----|
| MOR-### | … | Done / In progress / … | … |
```

Ask: "Anything here that should change how we grade last week?" Do not let Linear retro override owner judgment.

---

## Step 4: Plan interview

Target: **this week's Professional page** (create DB row during bootstrap if missing; body written in step 7).

### Create row (during bootstrap)

```text
Name: "<M/D/YY> - <M/D/YY> Technical Goals and Updates"
Start Date, Pass: "In Progress", Role: "Work"
Primary Focus: <infer from owner vision in step 2, or ask once after step 2>
Released: false
```

### Step 4a: Linear reconciliation (this week)

**After steps 2 and 3**, query Linear for issues **assigned to the owner** with due date in **this calendar week** (Mon–Sun, America/Los_Angeles). Use Linear MCP.

Present items not yet mapped to a draft goal from step 2:

```markdown
You described **N** goals for the week. Linear also has **M** items due this week assigned to you:

| Linear | Title | Due |
|--------|-------|-----|
| MOR-### | … | … |

For each (or in bulk if the owner prefers): **Which goal does this fit under, should it be its own goal, or should we change the due date?**
```

Rules:
- Match Linear items to owner goals where obvious; only ask about ambiguous or unmapped items.
- If owner says "change due date", update Linear when possible (or note for manual update).
- If owner says "own goal", add to draft goal list before step 4b.
- Do not treat Linear as the source of weekly goals — owner vision leads, Linear reconciles.

### Step 4b: Fill gaps (structured interview)

Only **after** steps 2, 3, and 4a, ask what's still missing:

For each goal (4–6 typical), if not already captured:
1. **Purpose** (mandatory)
2. 6-month ladder (if active this session)
3. Link existing **MOR-###** from reconciliation (do not re-ask if already mapped)

Then **Step 6** for subtasks. Do not write numbered goals to Notion yet.

### Standing sections (brief prompts)

| Section | Prompt |
|---------|--------|
| **Important Upcoming Milestones** | Copy unresolved from last week; update Status/Scope/Blockers/Due Date |
| **Deferred** | Copy standing items |
| **Daily Focus Journal** | Always generate the empty Mon–Sun skeleton. Fill only days the owner already volunteered (e.g. Monday off). Do **not** interview all seven days during Sunday planning. |
| **Highlights** | "Any wins this week?" |
| **Sharks and Shipwrecks** | Sharks = tracked risks; Shipwrecks = materialized issues |

### CEO weekly responsibilities

Surface active weekly-frequency CEO items as timeboxed goals or calendar blocks.

### Released

Ask after approval in step 8: **"Mark plan as Released?"** → set `Released` checkbox.

---

## Step 6: Subtask interview (required)

Follow [subtask-interview.md](../weekly-plan/subtask-interview.md) — mental checklist, interpretation table, per-sub-task loop, and professional extensions (milestones, sharks, CEO items).

Professional follow-ups emphasize: done criteria, owner, due date, dependency, deliverable link, **MOR-###** when applicable.

Loop until every Xavier goal has concrete sub-tasks (or purpose-only treatment) and standing sections are captured or explicitly carried forward unchanged.

---

## Step 7: Write Notion + OWNER_GOALS

1. Append skeleton — **Xavier only** on new pages. See [format-analysis.md](../weekly-plan/format-analysis.md) § Professional.
2. Insert numbered goals **after** template button blocks.
3. Always insert **Daily Focus Journal** after Goals for This Week and before Important Upcoming Milestones. See § Daily Focus Journal below.
4. Update OWNER_GOALS.md.
5. **Do not treat the session as approved yet** — proceed to step 8 and send the live URL.

---

## Step 8: Review & approve (mandatory final step)

Follow [subtask-interview.md](../weekly-plan/subtask-interview.md) § Review & approve. Use this title shape:

```markdown
Your professional weekly plan for **<M/D> – <M/D>** is ready for review:

**[<M/D/YY> - <M/D/YY> Technical Goals and Updates](<full Notion URL>)**
```

Approval is **only** valid after the owner opens that Notion page. Do not accept "approved" against a chat draft.

After approval, ask **one question at a time**:

1. **"Mark plan as Released (shared with team)?"** → set `Released` checkbox if yes.
2. **"Want to set tomorrow's daily focus now? (top two + stretch)"** → if yes, run § Daily Focus Journal (mid-week fill). If no, stop. If they already dictate tomorrow's focus in the same message, write it — do not re-ask.

Re-send link after any edits until approved.

---

## Daily Focus Journal

Required on **every** new professional weekly page. Execution home for the night-before top-two (+ stretch) habit.

### Skeleton (always write)

Place after `Goals for This Week` / Xavier numbered goals, **before** `Important Upcoming Milestones`. Dates are that week's Mon–Sun (America/Los_Angeles):

```markdown
# Daily Focus Journal
Night-before top two (+ stretch). Leave a day blank until you plan it.
### Monday M/D
-
### Tuesday M/D
-
### Wednesday M/D
-
### Thursday M/D
-
### Friday M/D
-
### Saturday M/D
-
### Sunday M/D
-
```

Fill a day **only** when the owner already stated it (planning interview, cross-domain carry such as Monday off, or a mid-week fill). Leave the `-` placeholder on unplanned days. Do not invent focuses.

When filling a day, use this shape:

```markdown
### Tuesday M/D
1. <primary>
2. <second>
3. **Stretch:** <stretch>
```

A single-focus day (e.g. day off) may be one bullet: `- **Primary:** …`

### Mid-week fill (next day)

Triggers: after step 8 if the owner says yes; or any "daily journal" / "tomorrow's focus" / "set tomorrow" request.

1. Open **this week's** professional page (do not create a new week).
2. Next day = tomorrow in America/Los_Angeles. Sunday evening → Monday. If tomorrow is past this week's Sunday, say the journal week is over.
3. Ask **one** question unless they already listed the focuses:

   > "What's tomorrow's top two and stretch?"

4. Update that day's H3 on the live page. Do not overwrite other days.
5. Send the Notion URL. No second approval loop unless they ask for edits.

Parse generously: if they name only a primary, write that and leave 2 / stretch blank. Carry Linear / weekly-goal numbers when they mention them.

---

## Write safety

Same as personal skill. Additionally:
- Never remove `[unsupported: button]` template blocks
- Inline grades go on numbered_list_item rich_text, not separate bullets
- Legacy multi-person pages: read-only for Katie/Jon on new creates
