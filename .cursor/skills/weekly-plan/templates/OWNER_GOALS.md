# OWNER_GOALS

Agent working copy of goal tracking at three horizons. Updated each weekly planning session.
Do **not** hand-edit outside the weekly review unless flagged in chat.

Location: `.cursor/skills/weekly-plan/state/OWNER_GOALS.md` (create `state/` on first run).

---

## 6-Month Goals (mirror of Goal Tracker)

> **Source of truth: Notion Goal Tracker** on the Goals page.
> Rewritten each session by querying active rows (`Period` covers today, `Hit?` = false).
> Format: `[<Focus>] <Goal title> — ends <YYYY-MM-DD>  <!-- gt:<page_id> -->`

<!-- BEGIN goal-tracker-mirror (auto-managed) -->
<!-- END goal-tracker-mirror -->

---

## Current Week (auto-managed)

> Format: ISO week. Each line links a weekly goal to its parent 6-month goal.

### YYYY-Www (Mon – Sun)
- [ ] **Personal #N**: <goal> — ladders to `[Focus] <6-month goal>`  <!-- gt:<page_id> -->
- [ ] **Professional #N**: <goal> — ladders to `[Focus] <6-month goal>`  <!-- gt:<page_id> -->

---

## Completion Log

> Append-only. One line per goal per week.
> `[ISO_WEEK] [PERSONAL|PROFESSIONAL] "<goal>" -> [HIT|PARTIAL|MISS|DEFERRED] (<note>)  <!-- gt:<page_id> -->`

```
```

---

## 6-Month Goal Progress (auto-managed)

> Recomputed each session from Completion Log + Current Week linkages.
> Status: `On track` / `At risk` / `Behind` / `Stalled`

<!-- BEGIN goal-tracker-progress (auto-managed) -->
<!-- END goal-tracker-progress -->

---

## Rolling Metrics

| Window | Goals set | HIT | PARTIAL | MISS | Hit rate | Trend |
|--------|-----------|-----|---------|------|----------|-------|
| Last 4 weeks | | | | | | |
| Last 8 weeks | | | | | | |
| Last 13 weeks | | | | | | |

### Notes (≤ 5 lines, refresh weekly)
