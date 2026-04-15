# Skills Layout

## Agent Entry Points (project root)

| Agent | Config File | Skill Entry |
|-------|-------------|-------------|
| Claude Code | `CLAUDE.md` | `claude/learn-eng/` → `learn-eng/` |
| Codex / OpenAI | `AGENTS.md` | `codex/learn-eng/` → `learn-eng/` |
| OpenClaw | `OPENCLAW.md` | `openclaw/learn-eng/` → `learn-eng/` |

## Directory Structure

- `learn-eng/` — canonical shared skill core (single source of truth)
- `claude/learn-eng` — Claude Code entry (symlink → `../learn-eng`)
- `codex/learn-eng` — Codex entry (symlink → `../learn-eng`)
- `openclaw/learn-eng` — OpenClaw entry (symlink → `../learn-eng`)

Adapter-specific behavior lives in `learn-eng/agents/<agent>.md`, not in the symlinks.  
The symlinks exist to reserve per-agent override paths for future platform divergence.
