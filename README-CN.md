# learn-eng-skill（中文说明）

[English/中文主文档](./README.md)

这是一个面向中文用户的英语学习 Skill 项目，重点在于：
- 单词卡片化学习
- 长难句结构拆解
- 段落逻辑分析
- 错题驱动 + 艾宾浩斯复习调度

## 推荐环境
- 推荐优先使用 `Claude Code` / `Codex` 这类支持本地文件读写的 Agent。
- 原因：可以自动更新 `user.md`、`vocab-repo.md`、`stenc-repo.md`、`vocabs.csv`，学习记录更连续，训练效果更稳定。

## 通用架构
核心目录：`skills/learn-eng/`

Agent 入口（当前共享核心，后续可拆分）：
- `skills/codex/learn-eng`
- `skills/claude/learn-eng`
- `skills/openclaw/learn-eng`
- `OPENCLAW.md`（OpenClaw 入口配置）

## OpenClaw 最小配置（可选）
在 `~/.openclaw/openclaw.json` 中启用并允许该技能：
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
