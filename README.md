# secret-agent

Personal Cursor agent skills for Xavier's Notion weekly focus dashboard — personal life goals and professional work goals in one system.

## Install

```bash
git clone https://github.com/XavierDedenbach/secret-agent.git ~/Documents/git/secret-agent
~/Documents/git/secret-agent/setup
```

The setup script auto-detects Claude Code, Cursor, and Antigravity, symlinks skills into each tool's global skills directory, initializes `OWNER_GOALS.md` from template if missing, and installs slash commands into this repo's `.cursor/commands/` plus `~/.claude/commands/` when Claude Code is present.

| Tool | Skills | Slash commands / workflows |
|------|--------|----------------------------|
| Claude Code | `~/.claude/skills/` | `~/.claude/commands/` |
| Cursor | `~/.cursor/skills/` | `.cursor/commands/` (this repo) |
| Antigravity (Gemini) | `~/.gemini/skills/` + `~/.gemini/config/skills/` | `~/.gemini/config/global_workflows/` · `~/.gemini/antigravity/global_workflows/` · `.agents/workflows/` |

### Update after pull

```bash
cd ~/Documents/git/secret-agent && git pull && ./setup
```

### Verify installation

```bash
./setup --verify
```

### Install to a single tool

```bash
./setup --only cursor
```

## Slash commands

Installed by `./setup`:

| Command | Action |
|---------|--------|
| `workflow` | **Entry point** — route to the correct skill |
| `weekly-plan` | Full Sunday replan — personal → professional |
| `personal-weekly-plan` | Personal focus dashboard only |
| `professional-weekly-plan` | Work / technical goals only |

**Cursor:** `.cursor/commands/` in this repo  
**Claude Code:** `~/.claude/commands/` (when `~/.claude/` exists)  
**Antigravity:** `~/.gemini/config/global_workflows/` + `.agents/workflows/` (when `~/.gemini/` exists)

Install commands/workflows elsewhere:

```bash
./setup --commands secret-agent .cursor/commands              # Cursor
./setup --commands secret-agent ~/.claude/commands            # Claude Code
./setup --commands secret-agent ~/.gemini/config/global_workflows  # Antigravity
```

## Skills

| Skill | When to use |
|-------|-------------|
| **workflow** | **Entry point** — route any planning or agent request to the right skill |
| **weekly-plan** | Router — full Sunday flow, bootstrap, cross-domain summary |
| **notion-weekly-plan-personal** | Life goals, habits, reading, relationships |
| **notion-weekly-plan-professional** | Work goals, technical delivery, Linear reconciliation |

### Session flow (both domains)

1. **Owner vision first** (professional) — unprompted weekly picture before Linear or structured prompts
2. **Retro** — grade last week (Notion + Linear for professional)
3. **Linear reconciliation** — due-this-week items → existing goals, new goals, or reschedule
4. **Subtask interview** — one follow-up per sub-task; parse multi-goal answers generously
5. **Write Notion** → **send link** → wait for **approval**

Personal flow: retro → goal interview → subtask interview → write → approve.

## Philosophy

The weekly plan is a **focus dashboard** — not a task list. It bridges 6-month goals (Goal Tracker) to daily execution. See [philosophy.md](.cursor/skills/weekly-plan/philosophy.md).

## Shared docs

| Doc | Purpose |
|-----|---------|
| [philosophy.md](.cursor/skills/weekly-plan/philosophy.md) | Why the system exists; focus vs task list |
| [format-analysis.md](.cursor/skills/weekly-plan/format-analysis.md) | Notion template specs from 30+ historical pages |
| [subtask-interview.md](.cursor/skills/weekly-plan/subtask-interview.md) | Subtask interview + approval rules (both domains) |
| [notion.yaml](.cursor/skills/weekly-plan/notion.yaml) | Notion database IDs — single source of truth |
| [templates/OWNER_GOALS.md](.cursor/skills/weekly-plan/templates/OWNER_GOALS.md) | Goal tracking template |
| `state/OWNER_GOALS.md` | Runtime copy (gitignored; created by `./setup`) |

## Structure

```
.cursor/skills/
  workflow/                       ← top-level router (entry point)
    SKILL.md
  weekly-plan/                    ← weekly-plan router + shared assets
    SKILL.md
    philosophy.md
    format-analysis.md
    subtask-interview.md
    notion.yaml
    templates/OWNER_GOALS.md
    state/                          ← gitignored runtime
  notion-weekly-plan-personal/
    SKILL.md
  notion-weekly-plan-professional/
    SKILL.md
commands/secret-agent/            ← slash command sources
setup                             ← install script
```

## Requirements

- **Notion MCP** (`user-notion`) — Personal + Professional Weekly Plan DBs, Goal Tracker, CEO Responsibilities
- **Linear MCP** (`plugin-linear-linear`) — professional plan reconciliation and retro

Integrations must be shared on the databases listed in `notion.yaml`.

## Adding or changing skills

1. Edit skills under `.cursor/skills/`
2. Run `./setup` to refresh symlinks
3. Commit and push — pull and re-run `./setup` on other machines
