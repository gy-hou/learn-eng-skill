# Learn Eng — Codex / OpenAI Agents

<!-- Codex entry point. Claude Code entry point → CLAUDE.md -->

## Active Skill

See `skills/codex/learn-eng/SKILL.md` for the full instruction set.
(Interface metadata: `skills/learn-eng/agents/openai.yaml`)

Paste the contents of `SKILL.md` into the system prompt, or invoke with:
```
$learn-eng <your input>
```

---

## Codex-Specific Behavior

Codex cannot write files directly. Apply these rules every session on top of the skill instructions.

### Reading state (before every analysis turn)
- The user should supply `skills/learn-eng/user.md` as context (upload or paste).
- Apply `Learner Tier` and `Explanation Mode` from that file.
- If not supplied, use skill defaults and ask user to provide it next turn.

### Writing state (output labeled code blocks)
After each turn, output updated file content in labeled blocks so the user can apply them:

| Event | Output block label |
|-------|--------------------|
| Profile setup / any turn | `→ user.md` |
| Vocabulary Mode output | `→ vocab-repo.md` (new row only) |
| Vocabulary Mode output | `→ vocabs.csv` (new/updated row only) |
| Sentence / Paragraph Mode (hard sentence) | `→ stenc-repo.md` (new row only) |
| Test mode answer checked | `→ vocabs.csv` (updated row only) |

**Label format:**
~~~
→ user.md
```
<full updated file content>
```
~~~

Output only the rows/sections that changed, not the entire file, unless it is the first write.

### Partial-write rule
When appending to a repo, output **only the new row(s)** so the user can paste them at the bottom of the existing file.

## Data File Paths

| File | Purpose |
|------|---------|
| `skills/learn-eng/user.md` | Learner profile & session state |
| `skills/learn-eng/vocab-repo.md` | Vocabulary repository (markdown table) |
| `skills/learn-eng/stenc-repo.md` | Sentence repository (markdown table) |
| `skills/learn-eng/vocabs.csv` | Spaced repetition schedule (Ebbinghaus) |
