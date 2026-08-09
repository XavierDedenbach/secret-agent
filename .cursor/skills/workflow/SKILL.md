---
name: workflow
description: >-
  Route personal agent requests to the correct secret-agent skill. Use when the
  user mentions weekly plan, replan, goals, focus dashboard, or any planning
  request where the right skill is unclear. Does not execute Notion writes itself;
  delegates to weekly-plan or an execution skill.
---

# Workflow (Secret Agent Router)

Top-level router for secret-agent. Read the matched skill end-to-end — do not substitute this router for leaf skill execution.

Shared assets: [weekly-plan/](../weekly-plan/) (philosophy, notion.yaml, subtask-interview.md)

---

## Routing output

Before acting, state briefly:

```text
Route: <full | personal | professional | read-only>
Next skill: <skill name>
Reason: <one sentence>
```

Then read and follow the selected skill.

---

## Decision tree

```
User message
    │
    ├─ "weekly plan" / "replan" / "Sunday plan" / "plan the week" / no qualifier
    │       → weekly-plan (full session: personal → professional)
    │
    ├─ "personal" / "my goals" / "life goals" / habits / reading / Substack
    │       → notion-weekly-plan-personal
    │
    ├─ "professional" / "work goals" / "technical goals" / "team update"
    │       / MR-### / milestones / sharks / Linear due this week
    │       → notion-weekly-plan-professional
    │
    ├─ "what's on my plan" / "show my goals" / "am I on track" / mid-week check-in
    │       → weekly-plan § Read-only check-in (no interview, no writes)
    │
    ├─ "grade last week" / "retro" + domain unclear
    │       → ASK: "Personal, professional, or both?" then route
    │
    └─ ambiguous planning language
            → weekly-plan (router handles disambiguation)
```

### Trigger phrases

| Route | Examples |
|-------|----------|
| **Full** | "weekly plan", "Sunday replan", "let's plan the week" |
| **Personal** | "personal weekly plan", "my weekly plan", "life planning" |
| **Professional** | "work weekly plan", "technical goals", "professional replan" |
| **Read-only** | "what's on my plan this week", "show my weekly goals" |

When ambiguous, ask one question:

> "Personal, professional, or full Sunday replan (both)?"

Default when user says just "plan" on Sunday evening: **full session, personal first**.

---

## Execution skills

| Skill | Path |
|-------|------|
| Router (full + bootstrap) | [weekly-plan/SKILL.md](../weekly-plan/SKILL.md) |
| Personal | [notion-weekly-plan-personal/SKILL.md](../notion-weekly-plan-personal/SKILL.md) |
| Professional | [notion-weekly-plan-professional/SKILL.md](../notion-weekly-plan-professional/SKILL.md) |

Every planning run ends with a **Notion page link** and **owner approval** before the session is complete.

---

## Extending this router

When new secret-agent skills are added (beyond weekly planning), append rows to the decision tree and execution skills table. Keep `workflow` as the single entry point; leaf skills own format fidelity and interviews.
