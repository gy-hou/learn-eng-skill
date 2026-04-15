# State Rules (Persistence Only)

## Scope
This file defines how learning state is read/written.  
Do not place teaching output style or quiz-generation logic here.

## Data Files (current paths)
- `skills/learn-eng/user.md` — learner profile + session timestamps
- `skills/learn-eng/vocab-repo.md` — difficult words/phrases table
- `skills/learn-eng/stenc-repo.md` — difficult sentences table
- `skills/learn-eng/vocabs.csv` — vocabulary cards + spaced-repetition fields

## Canonical Keys
- Vocabulary key: lowercase of collapsed whitespace text (word/phrase level).
- Sentence key: lowercase of collapsed whitespace full sentence text.
- Use canonical keys for dedupe and upsert matching.

## Write Triggers
1. Any normal turn:
- Update `user.md` `Last Updated At`.

2. Vocabulary mode:
- Append new hard vocabulary units into `vocab-repo.md` (dedupe first).
- Upsert `Vocabulary` + `Mnemonic` card into `vocabs.csv`.

3. Sentence/paragraph mode:
- Append difficult sentence lines into `stenc-repo.md` (dedupe first).

4. After review/testing updates:
- Sync `vocabs.csv.TestErrors` with vocabulary miss counts when applicable.

## Repo Dedupe Rules
- Before append, check canonical key existence.
- If key exists, do not append duplicate row.
- Keep existing `Added At` for existing rows.
- `Seen`/`Misses`/`Last Reviewed` are updated by review workflows, not by normal explanation output.

## `vocabs.csv` Schema
Columns:
- `Vocabulary`
- `Mnemonic`
- `TestErrors`
- `Stage`
- `LastReviewAt`
- `NextReviewAt`
- `CorrectStreak`
- `TotalReviews`
- `LastUpdatedAt`

Defaults for new rows:
- `TestErrors=0`, `Stage=0`, `LastReviewAt=-`, `NextReviewAt=-`, `CorrectStreak=0`, `TotalReviews=0`.

Validation:
- Clamp `Stage` to valid range (`0..5`).
- Keep integer counters non-negative.

## CSV Upsert / Merge Rules
- Match existing rows by canonical vocabulary key.
- Normalize whitespace and casing-stable key matching.
- If existing `Mnemonic` is empty and new mnemonic exists, fill it.
- Keep stronger learning state when merging duplicates:
- `Stage`, `CorrectStreak`, `TotalReviews`, `TestErrors`: keep max value.
- `NextReviewAt`: keep earliest valid due time.
- `LastReviewAt`, `LastUpdatedAt`: keep latest valid timestamp.
- On any row change, refresh `LastUpdatedAt`.

## Failure / Degrade Behavior
- Persistence failure must not block learner-facing explanation output.
- If write fails, return analysis first, then emit a concise operator-facing warning.
- Never delete user history as fallback behavior.
