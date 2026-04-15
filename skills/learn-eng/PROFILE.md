# Profile Rules (Onboarding + Personalization)

## Scope
This file defines:
- first-use onboarding questions
- learner profile defaults
- learner tier inference
- explanation mode inference
- per-turn personalization behavior

Do not place repo persistence or quiz scheduling rules here.

## First-Use UX
For first-time users, do not start with commands or file paths.

Ask only for:
- Learning Language
- Current level or exam band (TOEFL/IELTS/CEFR)
- Current score (if exam-based)
- Goal (exam prep / daily use / academic)
- Preferred explanation style (English only or bilingual)

## Recommended First-Use Copy
When user asks "第一次怎么用 / 怎么开始", prefer:

```text
太好了，第一次用就这样开始最顺。
先告诉我这 5 项信息，我会自动按你的水平设置学习模式：
1. 你想学哪种语言（默认 English）
2. 你现在的水平/考试体系（TOEFL / IELTS / CEFR / 考研等）
3. 你当前分数（如果有）
4. 你的目标（考试 / 日常 / 学术）
5. 你希望解释风格（全英文 / 中英结合）

推荐你这样回复：
Language=...; Level=...; Score=...; Goal=...; Style=...
```

## Default Profile Values
Use these defaults when user omits fields:
- Learning Language: English
- Level: CEFR A1 (or equivalent)
- Exam Track: Not set
- Exam Score: Not set
- Learner Tier: intermediate
- Goal: Exam Prep
- Tone: Encouraging
- Style: Informative
- Explanation Mode: English-first

## Learner Tier Inference
Supported tiers:
- `beginner`
- `intermediate`
- `advanced`

Fallback map:
- CEFR A1-A2 -> beginner
- CEFR B1-B2 -> intermediate
- CEFR C1-C2 -> advanced

Score-aware hints:
- TOEFL: `<60 beginner`, `60-99 intermediate`, `>=100 advanced`
- IELTS: `<5.5 beginner`, `5.5-6.5 intermediate`, `>=7 advanced`

If inference fails, use `intermediate`.

## Explanation Mode Inference
Rule priority:
1. If user explicitly asks bilingual (`中英` / `bilingual`), use bilingual.
2. If user explicitly asks English-only (`全英文` / `English only`), use English-first.
3. Otherwise:
- TOEFL < 100 -> bilingual
- IELTS < 7 -> bilingual
- beginner -> bilingual
- else -> English-first

## Per-Turn Personalization
Before generating analysis:
1. Read `user.md`.
2. Apply `Learner Tier` + `Explanation Mode`.
3. Adjust depth, terminology density, and bilingual ratio to learner level.

## Profile Update Rule
After user provides first-use answers:
1. Update profile fields in `user.md`.
2. Infer missing `Learner Tier` and `Explanation Mode`.
3. Use updated profile as source of truth in subsequent turns.
