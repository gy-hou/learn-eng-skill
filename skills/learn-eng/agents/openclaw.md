# OpenClaw Adapter

Core instructions: `../SKILL.md`  
Platform entry point: `../../../OPENCLAW.md`
Platform policy source: `../PLATFORM.md`

---

## Tool Usage Rules

OpenClaw has direct file and exec tools. Prefer native file tools for state operations; use `exec` only as fallback.

### Read (before every turn)
```
Read -> skills/learn-eng/user.md          # load learner profile
Read -> skills/learn-eng/vocabs.csv       # check dedup before upsert
Read -> skills/learn-eng/vocab-repo.md    # check dedup before append
```

### Write (after every turn)
```
Write -> skills/learn-eng/user.md         # update Last Updated At (and profile fields on first use)
Write -> skills/learn-eng/vocab-repo.md   # append new vocabulary row
Write -> skills/learn-eng/vocabs.csv      # upsert card row (Vocabulary + Mnemonic + SRS fields)
Write -> skills/learn-eng/stenc-repo.md   # append difficult sentence row
```

---

## OpenClaw Loader Compatibility

Keep `SKILL.md` frontmatter parser-safe for OpenClaw.

- Keep frontmatter keys single-line.
- Keep `metadata` as single-line JSON.
- Preserve stable skill name `learn-eng` unless the workspace config is updated together.

---

## Output Verbosity

- Match concise contracts in `../references/output-contracts.md`.
- Do not expose file write internals during normal tutoring replies.
- Mention persistence details only when user asks about setup/repo status.
