# Learn Eng — Claude Code

<!-- Claude Code entry point. Codex entry point → AGENTS.md -->

## Active Skill

@skills/claude/learn-eng/SKILL.md

---

## Claude-Specific Behavior

Claude Code has direct file access. Apply these rules every session on top of the skill instructions above.

### Reading state (before every analysis turn)
- Use the `Read` tool to load `skills/learn-eng/user.md`.
- Apply `Learner Tier` and `Explanation Mode` from that file before generating any output.

### Writing state (after every analysis turn)
Silently update files using `Edit`/`Write` tools — do **not** ask the user to copy-paste content:

| Event | File to update |
|-------|---------------|
| Profile setup / any turn | `skills/learn-eng/user.md` — set `Last Updated At` |
| First-use profile collected | `skills/learn-eng/user.md` — write all profile fields |
| Vocabulary Mode output | `skills/learn-eng/vocab-repo.md` — append new row |
| Vocabulary Mode output | `skills/learn-eng/vocabs.csv` — upsert card row |
| Sentence / Paragraph Mode (hard sentence) | `skills/learn-eng/stenc-repo.md` — append new row |
| Test mode answer checked | `skills/learn-eng/vocabs.csv` — update Stage / NextReviewAt / CorrectStreak |

### Silent operations rule
File writes must be invisible to the learner during normal tutoring.  
Only mention file activity if the user explicitly asks about repos or setup.

## Data File Paths

| File | Purpose |
|------|---------|
| `skills/learn-eng/user.md` | Learner profile & session state |
| `skills/learn-eng/vocab-repo.md` | Vocabulary repository (markdown table) |
| `skills/learn-eng/stenc-repo.md` | Sentence repository (markdown table) |
| `skills/learn-eng/vocabs.csv` | Spaced repetition schedule (Ebbinghaus) |
