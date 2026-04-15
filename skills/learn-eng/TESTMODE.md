# Test Mode Rules (Quiz + SRS Only)

## Scope
This file defines:
- quiz entry triggers
- MCQ generation format
- answer evaluation
- spaced-repetition updates (`Stage`, `NextReviewAt`, etc.)

Do not place normal vocabulary/sentence/paragraph explanation style here.

## Entry Triggers
Enter test mode when user asks:
- `test-mode`
- `/test-mode`
- `test me`
- `quiz`

## Question Format (default)
1. Vocabulary MCQ:
- One vocabulary item -> one single-choice meaning question (`A/B/C`).
- Do not use synonym multi-select by default.

2. Long-sentence MCQ:
- Show original sentence first.
- Then generate exactly three questions:
- `Meaning MCQ`
- `Function MCQ` (for highlighted chunk role)
- `Detail MCQ` (scope/negation/condition/modifier target)

3. Response format:
- Accept compact answer strings such as `1A 2C 3B`.

## Item Selection Priority
Vocabulary:
1. Due first: `NextReviewAt <= now` in `vocabs.csv`.
2. Rank due words by:
- overdue duration (higher first)
- repo misses (higher first)
- `TestErrors` (higher first)
- lower `Stage` (harder words earlier)
3. If due items are insufficient, fill from `vocab-repo.md` hard items.

Sentences:
- Select from `stenc-repo.md` using difficulty-first ordering (high misses first, then low seen count).

## Review Update Rules
SRS interval table (days by stage):
- `Stage 0 -> 1 day`
- `Stage 1 -> 2 days`
- `Stage 2 -> 4 days`
- `Stage 3 -> 7 days`
- `Stage 4 -> 15 days`
- `Stage 5 -> 30 days`

Stage range:
- clamp to `0..5`

On correct recall:
- `Stage += 1` (clamped)
- `CorrectStreak += 1`
- `TotalReviews += 1`
- update `LastReviewAt`, `NextReviewAt`, `LastUpdatedAt`

On missed recall:
- `Stage -= 1` (clamped)
- `CorrectStreak = 0`
- `TotalReviews += 1`
- `TestErrors += 1`
- increment vocab-repo `Misses`
- update `LastReviewAt`, `NextReviewAt`, `LastUpdatedAt`

## Sync Rules
- After test updates, synchronize `vocabs.csv.TestErrors` with repo miss counts when needed.
- Keep timestamp format consistent (UTC ISO-8601).

## Non-Test Turns
- Do not run selection/scoring/stage updates when user is in normal analysis mode.
