# Learn Eng - OpenClaw

<!-- OpenClaw entry point. Codex entry point -> AGENTS.md; Claude entry point -> CLAUDE.md -->

## Active Skill

Use `skills/openclaw/learn-eng/SKILL.md`.

---

## OpenClaw-Specific Behavior

OpenClaw has direct file access. Apply these rules every session on top of the skill instructions above.

### Reading state (before every analysis turn)
- Load `skills/learn-eng/user.md` and apply `Learner Tier` + `Explanation Mode`.
- Load `skills/learn-eng/vocabs.csv` and `skills/learn-eng/vocab-repo.md` before vocabulary upsert to avoid duplicates.

### Writing state (after every analysis turn)
Silently update files (no copy/paste request to user):

| Event | File to update |
|-------|----------------|
| Profile setup / any turn | `skills/learn-eng/user.md` - set `Last Updated At` |
| First-use profile collected | `skills/learn-eng/user.md` - write profile fields |
| Vocabulary Mode output | `skills/learn-eng/vocab-repo.md` - append new row |
| Vocabulary Mode output | `skills/learn-eng/vocabs.csv` - upsert card row |
| Sentence / Paragraph Mode (hard sentence) | `skills/learn-eng/stenc-repo.md` - append new row |
| Test mode answer checked | `skills/learn-eng/vocabs.csv` - update Stage / NextReviewAt / CorrectStreak |

### Silent operations rule
File writes should stay invisible in normal tutoring replies. Mention file activity only if the user explicitly asks.

---

## Suggested OpenClaw Config

Add this to `~/.openclaw/openclaw.json` to force-enable and allowlist the skill:

```json
{
  "skills": {
    "entries": {
      "learn-eng": { "enabled": true }
    }
  },
  "agents": {
    "defaults": {
      "skills": ["learn-eng"]
    }
  }
}
```
