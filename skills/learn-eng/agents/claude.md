# Claude Code Adapter

Core instructions: `../SKILL.md`  
Platform entry point: `../../../CLAUDE.md`

---

## Tool Usage Rules

Claude Code has file tools. Use them for all state operations — never ask the user to copy content manually.

### Read (before every turn)
```
Read → skills/learn-eng/user.md          # load learner profile
Read → skills/learn-eng/vocabs.csv       # check for deduplication before upsert
Read → skills/learn-eng/vocab-repo.md    # check for deduplication before append
```

### Edit (after every turn)
```
Edit → skills/learn-eng/user.md          # update Last Updated At (and profile fields on first use)
Edit → skills/learn-eng/vocab-repo.md    # append new vocabulary row
Edit → skills/learn-eng/vocabs.csv       # upsert card row (Vocabulary + Mnemonic + SRS fields)
Edit → skills/learn-eng/stenc-repo.md    # append difficult sentence row
```

### Write
Use only for initial file creation (e.g., user.md does not yet exist).

---

## Output Verbosity

- Match concise output contracts in `../references/output-contracts.md`.
- Do **not** add system messages about file writes during normal tutoring replies.
- Do **not** output file content as code blocks — write directly to disk.
- Mention file operations only when the user explicitly asks about repo or setup status.

---

## Differences vs Codex

| Behavior | Claude Code | Codex |
|----------|-------------|-------|
| File reads | `Read` tool | User uploads / pastes file |
| File writes | `Edit`/`Write` tool (silent) | Output `→ filename` code blocks |
| State persistence | Automatic, every turn | Manual, user pastes output |
| Skill invocation | Loaded via `CLAUDE.md` `@import` | `$learn-eng` or system prompt paste |
