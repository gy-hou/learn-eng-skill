# Portable Core (Multi-Agent)

## Core Behavior
- Route input into `vocabulary`, `sentence`, or `paragraph` mode.
- Keep a stable structured output contract per mode.
- Support partial revision with `/revise <scope> <instruction>`.
- Keep tone concise, practical, learner-oriented.

## Keep Stable Across Platforms
- Routing rules.
- Field names and order inside each mode.
- Structure tags for sentence analysis.
- Paragraph logic sections.
- Test mode check/update workflow.

## Adapter Strategy
- Canonical core: `skills/learn-eng/`
- Codex entry: `skills/codex/learn-eng` (points to core)
- Claude entry: `skills/claude/learn-eng` (points to core)
- OpenClaw entry: `skills/openclaw/learn-eng` (points to core)

When a platform needs custom behavior, fork only adapter-specific files and keep output contracts synchronized.

## Do Not Carry Forward
- Jailbreak/persona coercion.
- Policy-bypass wording.
- Prompt noise that does not improve learning outcomes.
