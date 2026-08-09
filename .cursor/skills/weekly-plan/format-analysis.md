# Weekly Plan Format Analysis

Derived from 30+ live Notion pages reviewed 2026-08-09. Full philosophy: [philosophy.md](philosophy.md).

## Pages reviewed (by era)

### Genesis — May–Jul 2024
| Week | Notes |
|------|-------|
| 6/03/24 | Earliest page; "Goal" not "Purpose"; no grading callout; no Deferred |
| 8/12/24 | 7 goals; "Approach" instead of Sub-tasks; Deferred Items section begins |

### Structure forming — Aug–Oct 2024
| Week | Notes |
|------|-------|
| 9/17/24 | Grading callout added; "Total Plan (3 Weeks Left)" multi-week horizon |
| 10/27/24 | 6-month callout on Goal Setting; One Pager "What helps me focus" |
| 11/18/24 | Full retro grading; recurring improvement cues (TV, timeboxing) |

### Mature personal — 2025
| Week | Notes |
|------|-------|
| 4/21/25 | Synced reading tracker; deferred with Reflection |
| 8/25/25 | 10 graded retro goals; runway/founder pivot content |
| 11/17/25 | Retro skipped — anti-pattern |

### Professional — 2024–2026
| Week | Notes |
|------|-------|
| 1/06/24 | Early format; no template buttons; milestones + sharks present from start |
| 2/03/25 | Xavier-only goals; full milestone/deferred/sharks structure |
| 6/09/25 | Katie sections (legacy); Released=true pattern |

**Format stabilized Aug–Oct 2024** for personal; professional stable from early 2025.

---

## Stable format rules (Oct 2024 onward)

### Personal weekly plan

**Database row properties** (set on create):
- `Name`: `My Weekly Plan M/D/YY - M/D/YY` (Monday–Sunday of the week)
- `Start Date`: Monday ISO date
- `Pass`: `In Progress` (updated to Pass/No Pass after retro)
- `Role`: `Personal`
- `Primary Focus`: owner picks one (Business Growth, Time Management, Family, …)

**Page body section order** (strict):

1. **H1** `Last Week's Goals Retrospective`
2. **Callout** (💡, gray background) — Grading Key
3. **H2 blocks** `#N: <title> <grade>` — one per last-week goal, graded inline on the H2 title
   - `- Purpose` → indented paragraph
   - `- Sub-tasks` → indented bullets (sub-tasks may carry their own ✅/❌)
   - Optional `- Related tasks`
   - Optional `- Ladders to: <6-month goal>` (agent adds during planning; rare in older pages)
4. **H2** `What are 3 ways I could have done better?` → 1–3 bullets (often nested with detail)
5. **H1** `This Week's Goal Setting`
6. **Callout** (💡, gray) — *"This should be the 2-3 most important things… towards my 6 month goals"* (present since Oct 2024)
7. **H2 blocks** `#1:` … `#N:` (target 2–3, ceiling 8) each with Purpose / Sub-tasks / optional Ladders to
8. **H1** `Deferred`
9. **H2** `#X: <title>` items with Purpose, Subtasks, Reflection; plus a free-form bullet list of misc deferred ideas
10. **H2** `This Weeks One Pager:` → link placeholder + Core Ideas / Inspiration bullets
11. **H2** `What are my improvement cues I am focusing on` → free-form paragraph

**Grading symbols** (consistent across all 14 pages):
- ✅ Complete
- 🆗 In Progress (80%+ complete)
- 🛑 Deleted or deferred to another week — append `(Deferred to week of M/D)` to H2 title when deferring
- ❌ Not Complete

**Variations to preserve, not "fix":**
- Some pages put retro goals BEFORE the grading callout (Aug 2025 `25a115d4`) — canonical order is callout first
- `#6: 6 month replan` goals appear ad hoc during replan weeks (Aug 2025)
- Synced blocks (Weekly Reading Tracker) may appear under reading goals — never delete synced_block_reference
- Not all goals have Purpose/Sub-tasks — but the agent should always ask for them on new goals

### Professional weekly plan

**Database row properties:**
- `Name`: `M/D/YY - M/D/YY Technical Goals and Updates`
- `Start Date`, `Pass`, `Role: Work`, `Primary Focus`, `Released` (checkbox)

**Page body section order:**

1. **Callout** (🪫, gray background) — Grading Key (note: `>80%` not `80%+`)
2. **H1** `Last Week's Goals Retro:`
3. **H3** `Xavier` → numbered list; grade inline: `1. **Goal title:** ✅`
   - Nested Purpose / Subtasks under each numbered item
   - **Bold paragraph** `Added during the week` → numbered mid-week additions
4. **Divider**
5. *(Legacy pages only)* **H3** `Katie` / `Jon` — same retro structure. **New pages: Xavier only** (per 2026-04-19 rule)
6. **H1** `Goals for This Week:`
7. **H3** `Xavier` → `[template button block]` then numbered goals with Purpose/Subtasks
8. **H1** `Important Upcoming Milestones:` — bullets with Status / Scope / Blockers / Due Date sub-structure
9. **H1** `Deferred` — bullet list (often standing items like "Residency on electrolyzer teams")
10. **H1** `Highlights`
11. **H1** `Sharks and Shipwrecks`
    - **Sharks** = active risks being tracked
    - **Shipwrecks** = issues that materialized

**Professional goal nesting pattern** (observed consistently):
```
1. **Goal title:**
   - **Purpose:** …
   - **Subtasks**
     1. First subtask ✅
     2. Second subtask
```

---

## Priority & goal-tracking map

| Horizon | Where tracked | What it holds | Agent role |
|---------|---------------|---------------|------------|
| 6-month | Goal Tracker DB (`Goals` page) | `[Focus] Goal title`, Period, Hit? | Read only; mirror to OWNER_GOALS.md |
| Weekly (personal) | Personal Weekly Plan DB + page body | `#N:` goals, Purpose, sub-tasks | Interview, write, grade |
| Weekly (professional) | Professional Weekly Plan DB + page body | Xavier numbered goals, milestones | Interview, write, grade, optional Linear link |
| Weekly focus theme | `Primary Focus` select on DB row | One category for the week | Ask owner at page create |
| CEO cadence | CEO Responsibilities DB | Active + Frequency=Weekly items | Surface during planning; timebox on calendar |
| Agent bridge | `OWNER_GOALS.md` | 6-month mirror, current week linkages, completion log, rolling metrics | Read/write each session |
| Execution | Linear (professional only) | MOR-### tasks | Optional link on goal title |

**6-month linkage** — no Notion relation exists. Bridge via:
1. `Ladders to: <Goal Tracker title>` bullet under each weekly goal in Notion page body
2. `OWNER_GOALS.md` "Current Week" section with `<!-- gt:<page_id> -->` comments
3. Completion Log entries tagged to parent 6-month goal

**Gap flag:** If no weekly goal ladders to any active 6-month goal, add a note at the bottom of "This Week's Goal Setting" calling it out.

---

## Observed planning behaviors (from good weeks)

1. **Retro before plan** — grade every `#N:` from last week before setting new goals
2. **Purpose is mandatory** — even one line; distinguishes "what" from "why"
3. **Deferred is a parking lot** — items get Reflection when deferred; `#X:` numbering
4. **3 improvement cues** — always asked; often recurs ("timebox tasks at work")
5. **Primary Focus** — one select per week sets the thematic lens
6. **Professional Released** — checkbox flipped after plan shared with team
7. **Milestones carry forward** — copy unresolved milestones week to week
8. **Sharks persist** — link back to week first identified when a shark continues
