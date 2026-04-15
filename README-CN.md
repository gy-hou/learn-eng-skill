# learn-eng-skill（中文说明）

[English/中文主文档](./README.md)

这是一个面向中文用户的英语学习 Skill 项目，重点在于：
- 单词卡片化学习
- 长难句结构拆解
- 段落逻辑分析
- 错题驱动 + 艾宾浩斯复习调度

## 通用架构
核心目录：`skills/learn-eng/`

Agent 入口（当前共享核心，后续可拆分）：
- `skills/codex/learn-eng`
- `skills/claude/learn-eng`
- `skills/openclaw/learn-eng`

## 首次使用
直接回复：
```text
Language=...; Level=...; Score=...; Goal=...; Style=...
```

## 日常使用
- 发单词/词组：词汇分析
- 发一句话：句子结构分析
- 发一段话：段落逻辑分析
- 输入 `test-mode`：开始选择题测试
- 批改后调用 `mark-correct` / `mark-missed` 更新记忆阶段

## 数据文件
- `skills/learn-eng/user.md`
- `skills/learn-eng/vocab-repo.md`
- `skills/learn-eng/stenc-repo.md`
- `skills/learn-eng/vocabs.csv`

## 许可证
MIT License（见 [LICENSE](./LICENSE)）。
