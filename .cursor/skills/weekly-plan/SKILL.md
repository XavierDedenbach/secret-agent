---
name: weekly-plan
description: >-
  Routes weekly planning conversations to the correct Notion workflow — full
  Sunday replan (personal then professional), personal-only, or professional-only.
  Each run ends with a Notion page link for owner review and approval. Use when
  the user mentions weekly plan, weekly replan, Sunday planning, grading last
  week's goals, setting this week's priorities, or focus dashboard. Delegates to
  notion-weekly-plan-personal or notion-weekly-plan-professional. For ambiguous
  requests, prefer the workflow skill as the entry point.
---

# Weekly Plan (Router)

Orchestrates Xavier's Notion weekly focus dashboard. Read [philosophy.md](philosophy.md) first — it explains *why* this system exists.

Shared assets live in this folder:
- [philosophy.md](philosophy.md) — purpose, horizons, rituals
- [format-analysis.md](format-analysis.md) — template specs from 30+ pages
- [subtask-interview.md](subtask-interview.md) — shared subtask interview + approval rules
- [notion.yaml](notion.yaml) — Notion database IDs
- [templates/OWNER_GOALS.md](templates/OWNER_GOALS.md) — goal tracking template
- `state/OWNER_GOALS.md` — runtime copy (create on first run)

Execution skills (read and follow the matched one):
- [../notion-weekly-plan-personal/SKILL.md](../notion-weekly-plan-personal/SKILL.md)
- [../notion-weekly-plan-professional/SKILL.md](../notion-weekly-plan-professional/SKILL.md)

---

## Routing decision tree

```
User message
    │
    ├─ "weekly plan" / "replan" / "Sunday plan" / no qualifier
    │       → FULL SESSION: bootstrap → personal → professional → summary
    │
    ├─ "personal" / "my goals" / "life goals" / "Substack" / "reading" / "habits"
    │       → PERSONAL ONLY
    │
    ├─ "professional" / "work goals" / "technical goals" / "team update"
    │       / "MOR-" / "milestones" / "sharks"
    │       → PROFESSIONAL ONLY
    │
    ├─ "grade last week" / "retro" + context unclear
    │       → ASK: "Personal, professional, or both?"
    │
    └─ "what are my goals this week" / mid-week check-in
            → READ ONLY: fetch current week's pages, summarize — no interview
```

### Trigger phrases

| Route | Example phrases |
|-------|-----------------|
| **Full** | "weekly plan", "Sunday replan", "let's plan the week", "weekly planning" |
| **Personal** | "personal weekly plan", "my weekly plan", "life planning", "personal goals this week" |
| **Professional** | "work weekly plan", "technical goals", "professional replan", "team goals" |
| **Read-only** | "what's on my plan this week", "show my weekly goals", "am I on track" |

When ambiguous, ask one question:

> "Personal, professional, or full Sunday replan (both)?"

Default on Sunday evening / user says just "plan": **full session, personal first**.

---

## Full session flow

```
Weekly Plan Progress:
- [ ] 0. Bootstrap (shared — this skill)
- [ ] 1. Personal → notion-weekly-plan-personal (through step 6 approval)
- [ ] 2. Professional → notion-weekly-plan-professional (through step 6 approval)
- [ ] 3. Cross-domain summary (after both approved)
```

### Step 0: Bootstrap (run once per session)

1. Copy [templates/OWNER_GOALS.md](templates/OWNER_GOALS.md) to `state/OWNER_GOALS.md` if missing.
2. Query Goal Tracker — rewrite 6-month mirror in `state/OWNER_GOALS.md`. See personal skill for query details.
3. Present numbered 6-month goals to the user.
4. Compute this/last week dates (America/Los_Angeles).
5. Tell the user the plan: "We'll do Personal retro + plan first, then Professional. Ready?"

Then **read and execute** `notion-weekly-plan-personal` through step 6 (including subtask interview and Notion link for approval).

Then **read and execute** `notion-weekly-plan-professional` through step 6.

Each execution skill **must end with the Notion page link** and wait for owner approval before the router considers that domain complete.

When transitioning personal → professional after personal approval, **carry cross-domain items** from the personal plan (e.g. Monday off, calendar blocks) into professional planning — see [subtask-interview.md](subtask-interview.md).

### Step 3: Cross-domain summary (after both approved)

Only after owner approves both pages (or explicitly skips professional), present unified dashboard:

```markdown
## Focus Dashboard — Week of <M/D> – <M/D>

### 6-month north stars (active)
1. [Focus] Goal — ends DATE
…

### This week — Personal (<N> goals)
| # | Goal | Ladders to |
|---|------|------------|
| 1 | … | [Focus] … |

### This week — Professional (<N> goals)
| # | Goal | Ladders to |
|---|------|------------|
| 1 | … | [Focus] … |

### Gaps & alerts
- [ ] No personal goal ladders to [6-month goal X] — intentional?
- [ ] [6-month goal Y] — Stalled (no weekly bridge)

### Recurring improvement cues
(from last retro — surface if same theme 3+ weeks)

Links: [Personal plan](url) · [Professional plan](url)
```

---

## Personal-only or professional-only

Skip bootstrap if `state/OWNER_GOALS.md` was refreshed within the last 7 days AND 6-month goals unchanged. Otherwise run bootstrap step 0 (items 1–3 only).

Read and follow the matching execution skill end-to-end through **step 6 (Review & approve)**. The session is not complete until the owner approves the Notion page.

---

## Session completion rule

Every weekly plan run (personal, professional, or both) follows:

1. Retro → goal interview → **subtask interview** (parse generously; one question only for open items) → write Notion → **send link → wait for approval**

Never skip the subtask interview. Never end without the Notion URL and an explicit approval request.

---

## Read-only check-in

No interview. No writes.

1. Fetch this week's Personal + Professional pages from Notion.
2. Summarize: goal titles, purposes, 6-month linkages, Pass status, ungraded items.
3. Flag: empty plans, no 6-month bridge, stale milestones/sharks.

---

## Architecture decision (documented)

**Why split personal / professional into separate skills:**

| Factor | One skill | Two skills + router ✓ |
|--------|-----------|----------------------|
| Template difference | Large conditional blocks | Clean, focused instructions |
| Mid-week partial runs | Loads irrelevant half | Route to one skill |
| Agent discovery | Vague description | Precise trigger terms per domain |
| Shared bootstrap | Natural | Router owns bootstrap |
| Your actual usage | Always sequential on Sunday | Often one domain alone mid-week |

The router (`weekly-plan`) owns philosophy, routing, bootstrap, and cross-domain summary. Execution skills own format fidelity and domain-specific interviews.
