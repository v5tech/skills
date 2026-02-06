# Skills

[![English](https://img.shields.io/badge/docs-English-blue)](README.md)

适用于 Claude Code、Gemini CLI 等 AI 编程助手的技能集合。

## 可用技能

| 技能 | 描述 |
|------|------|
| [skill-advisor](skill-advisor/) | 通过 `npx skills` CLI 搜索、比较和安装技能 |
| [skill-exporter](skill-exporter/) | 生成安装命令以备份/复制技能配置 |

## 安装

使用 [Skills CLI](https://github.com/vercel-labs/skills) 安装技能：

```bash
# 将所有技能安装到默认代理
npx skills add v5tech/skills -g -s skill-advisor -s skill-exporter -a antigravity -a claude-code -a gemini-cli -a opencode -y

# 安装单个技能
npx skills add v5tech/skills -g -s skill-advisor -a claude-code -y
```

## 默认目标代理

| 代理 | `--agent` 值 |
|------|--------------|
| Antigravity | `antigravity` |
| Claude Code | `claude-code` |
| Gemini CLI | `gemini-cli` |
| OpenCode | `opencode` |

## 验证安装

```bash
npx skills ls -g
```

## 许可证

MIT
