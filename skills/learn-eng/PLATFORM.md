# Platform Rules (Codex / Claude / OpenClaw)

## Scope
This file defines platform-specific execution differences only.

Do not place pedagogy logic, routing rules, or quiz scheduling here.

## Shared Behavior Baseline
- Use `SKILL.md` as the user-facing contract.
- Use `PROFILE.md` for onboarding/personalization.
- Use `STATE.md` for persistence.
- Use `TESTMODE.md` for quiz/review loop.
- Keep learner-facing replies free from file-operation noise unless user asks.

## Platform Matrix

### Codex / OpenAI Agents
- Entry: `AGENTS.md`
- Adapter metadata: `skills/learn-eng/agents/openai.yaml`
- Read model:
- User supplies `skills/learn-eng/user.md` content in context (paste/upload).
- Write model:
- Return labeled update blocks (for example `→ user.md`, `→ vocabs.csv`).
- Partial write:
- For repo append, output new rows only.

### Claude Code
- Entry: `CLAUDE.md`
- Adapter notes: `skills/learn-eng/agents/claude.md`
- Read model:
- Use `Read` tool for state files.
- Write model:
- Use `Edit` / `Write` silently.
- Never require user copy-paste for normal persistence.

### OpenClaw
- Entry: `OPENCLAW.md`
- Adapter notes: `skills/learn-eng/agents/openclaw.md`
- Read model:
- Use native file reads before analysis/upsert.
- Write model:
- Use native file writes silently.
- Keep OpenClaw frontmatter compatibility:
- single-line YAML keys
- single-line JSON `metadata`

## Conflict Resolution
- If platform entry files (`AGENTS.md`, `CLAUDE.md`, `OPENCLAW.md`) define stricter behavior, follow entry-file rules first.
- Keep adapter markdown files aligned with this document.
