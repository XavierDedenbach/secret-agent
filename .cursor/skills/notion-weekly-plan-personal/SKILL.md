---
name: notion-weekly-plan-personal
description: >-
  Personal weekly focus dashboard in Notion — grades last week's life goals,
  sets 2-8 intentional personal goals with Purpose, interviews every sub-task,
  writes Notion page, and ends with the page link for owner review and approval.
  Use for reading, writing, Substack, relationships, habits, or personal Sunday replan.
  Requires weekly-plan bootstrap or runs bootstrap itself if OWNER_GOALS missing.
---

# Personal Weekly Plan

Executes the **personal** half of Xavier's Notion focus dashboard. For routing (personal vs professional vs full), see [weekly-plan/SKILL.md](../weekly-plan/SKILL.md). For philosophy, see [weekly-plan/philosophy.md](../weekly-plan/philosophy.md).

Shared config: [weekly-plan/notion.yaml](../weekly-plan/notion.yaml) · Templates: [weekly-plan/format-analysis.md](../weekly-plan/format-analysis.md)

State file: `weekly-plan/state/OWNER_GOALS.md`

**Approval rule (non-negotiable):** The owner approves **only** after opening the live Notion page. Chat recaps are not the plan. Never ask “reply approved and I’ll write the page.” If the interview is done, write the page immediately, send the URL, and wait. An “approved” before that URL exists is invalid.

---

## Checklist

```
Personal Weekly Plan:
- [ ] 1. Bootstrap (skip if weekly-plan router already ran)
- [ ] 2. Retro — grade last week
- [ ] 3. Plan interview — goals, purpose, 6-month ladder (if applicable)
- [ ] 4. Subtask interview — one follow-up per sub-task per goal
- [ ] 5. Write Notion page + OWNER_GOALS.md
- [ ] 6. Review & approve — send the live Notion URL; owner approves only after opening that page
```

Ask **one question at a time**. **Enforce focus**: target 2–3 goals, push extras to Deferred.

**Do not skip step 4.** Do not write the Notion page body until subtask interviews are complete. A chat recap is optional as an interview aid — **never request approval on chat**.

**Do not mark the session complete until step 6.** The only acceptable approval is the owner viewing the Notion page (the URL you send) and then saying approved or requesting edits. If they say the interview is done before the page exists, write the page immediately and send the link — do not wait for a chat "approved."

Shared interview rules: [subtask-interview.md](../weekly-plan/subtask-interview.md)

---

## Step 1: Bootstrap

Skip if `weekly-plan/state/OWNER_GOALS.md` was refreshed today.

1. Query Goal Tracker (`goal_tracker.data_source_id` from notion.yaml):
   ```text
   API-query-data-source(
     filter = { "property": "Period", "date": { "on_or_before": "<today>" } },
     page_size = 50
   )
   ```
   Client-filter: active rows (`Period` covers today, `Hit?` = false). Skip `QA DO NOT USE`.

2. Rewrite `<!-- BEGIN goal-tracker-mirror -->` in OWNER_GOALS.md.

3. Find pages — query `weekly_plan.personal.data_source_id` for last week and this week (`Start Date` range; never use `date.last_week`).

---

## Step 2: Retro

Target: **last week's Personal page**.

1. Read each `#N:` H2 from last week's "This Week's Goal Setting".
2. Per goal ask: "Did you complete **\<title\>**? (✅ / 🆗 / 🛑 / ❌)" + "Anything to capture?"
3. Write grades on H2 titles via `API-update-a-block`. Deferrals: append `🛑 (Deferred to week of M/D)`.
4. Append reflections under Sub-tasks.
5. Log to OWNER_GOALS.md Completion Log: ✅→HIT, 🆗→PARTIAL, ❌→MISS, 🛑→DEFERRED.
6. Ask: **"What are 3 ways you could have done better?"** — append under that H2.
7. Set DB `Pass` to Pass or No Pass.

If last week had no goals or retro was skipped, acknowledge it (Nov 2025 anti-pattern) and capture a brief narrative before planning.

---

## Step 3: Plan interview

Target: **this week's Personal page** (create DB row early if missing; body written in step 5).

### Create row (can happen before interview)

```text
Name: "My Weekly Plan <M/D/YY> - <M/D/YY>"
Start Date: <this_monday>
Pass: "In Progress"
Role: "Personal"
Primary Focus: <ask user — Personal Growth, Business Growth, Time Management, Family, …>
```

### Goal-level interview

Open with the philosophy anchor:

> "What are the 2–3 most important personal things this week?"

For each goal (max 8, prefer 3), **before subtasks**:
1. Title
2. **Purpose** (mandatory — never leave "xxx")
3. 6-month ladder (skip if owner opts out for this session): "Which Goal Tracker goal does this ladder to?"

Then proceed to **Step 4** for subtasks. Do not write goal blocks to Notion yet.

### Carry forward & defer

- Ask before carrying uncompleted goals from last week
- Move 🛑 items to Deferred with Reflection
- Preserve synced blocks and template buttons

### Gap check

If 6-month linking is active and zero goals ladder → callout at bottom of Goal Setting. Ask if intentional.

### One Pager (optional)

Ask: "Any focus theme for This Weeks One Pager?" Default: "What helps me focus".

---

## Step 4: Subtask interview (required)

Follow [subtask-interview.md](../weekly-plan/subtask-interview.md) — mental checklist, interpretation table, and per-sub-task loop.

---

## Step 5: Write Notion + OWNER_GOALS

1. Create page if not exists; append full skeleton from [format-analysis.md](../weekly-plan/format-analysis.md) § Personal.
2. Write all goals with Purpose, sub-tasks (with interview detail), optional Ladders to.
3. Update OWNER_GOALS.md: Current Week, Completion Log (retro), rolling metrics.
4. **Do not treat the session as approved yet** — proceed to step 6 and send the live URL.

---

## Step 6: Review & approve (mandatory final step)

Follow [subtask-interview.md](../weekly-plan/subtask-interview.md) § Review & approve. Use page title **My Weekly Plan \<dates\>**.

Approval is **only** valid after the owner opens that Notion page. Do not accept "approved" against a chat draft.

---

## Write safety

- Verify property option names via `retrieve-a-data-source` if unsure
- Append-only bodies; `API-update-a-block` for edits
- Never delete synced_block_reference or template buttons
- Never edit Goal Tracker without explicit confirmation
