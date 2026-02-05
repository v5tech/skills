# v5tech/skills

[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub](https://img.shields.io/badge/GitHub-v5tech/skills-black?logo=github)](https://github.com/v5tech/skills)

**[English](README.md) | [中文](README.zh.md)**

AI 智能体技能集合，用于开发工作流优化。本项目提供精选技能，提升多个 AI 编程助手的生产力。

---

## 项目概述

本项目包含专为 Claude Code、Gemini CLI、OpenCode 和 Antigravity 等 AI 智能体设计的专业技能。每项技能都提供特定领域的指导和工作流，帮助开发者更高效地完成任务。

## 功能特性

- **多智能体支持**: 兼容 39+ 个 AI 智能体，包括 Claude Code、Gemini CLI、OpenCode、Antigravity
- **工作流优化**: 预置常见开发场景的技能
- **易于安装**: 简单的 `npx skills` CLI 集成
- **最佳实践**: 详细的指导帮助避免常见陷阱

## 技能说明

### skill-advisor

使用 npx skills CLI 搜索、比较和安装技能的指南。

**使用场景**: 用户想要查找技能、比较技能功能，或安装技能到特定智能体时。

**核心能力**:
- 使用多个关键词搜索技能
- 安装前预览技能内容
- 从多个维度比较技能（质量、覆盖范围、技术栈匹配度等）
- 为目标智能体生成正确的安装命令
- **避免常见陷阱**，如会覆盖 `--agent` 设置的 `--all` 标志

**默认目标智能体**: Antigravity、Claude Code、Gemini CLI、OpenCode

**安装示例**:
```bash
# 将 skill-advisor 安装到所有 4 个默认智能体
npx skills add v5tech/skills -g -s skill-advisor -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

### skill-exporter

生成 `npx skills add` 命令以复现已安装技能。

**使用场景**: 用户想要导出、备份、分享或复制他们的技能配置到另一台机器时。

**核心能力**:
- 从 `npx skills ls -g` 解析当前安装
- 从锁定文件（`~/.agents/.skill-lock.json`）读取源仓库
- 按源和智能体集合分组技能
- 输出优化的安装命令

**安装示例**:
```bash
# 将 skill-exporter 安装到所有 4 个默认智能体
npx skills add v5tech/skills -g -s skill-exporter -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

## 安装

### 安装所有技能

```bash
# 将两个技能安装到默认智能体
npx skills add v5tech/skills -g -s skill-advisor -s skill-exporter -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

### 安装到自定义智能体

```bash
# 示例：安装到 Cursor 和 Windsurf
npx skills add v5tech/skills -g -s skill-advisor -s skill-exporter -a cursor -a windsurf -y
```

### 验证安装

```bash
# 列出已安装的技能及其智能体
npx skills ls -g

# 检查智能体目录中的技能文件
ls -la ~/.claude/skills/
ls -la ~/.gemini/skills/
ls -la ~/.config/opencode/skills/
```

## 项目结构

```
skills/
├── README.md                    # 英文文档
├── README.zh.md                 # 中文文档（本文件）
├── skill-advisor/
│   ├── SKILL.md                 # 技能定义和工作流
│   └── references/
│       └── agents.md            # 完整的智能体目录参考
└── skill-exporter/
    ├── SKILL.md                 # 技能定义和工作流
    └── references/
        └── agents.md            # 完整的智能体目录参考
```

## 使用示例

### 使用 skill-advisor

当用户询问"如何查找 React 相关技能？"时：

1. skill-advisor 会指导您使用多个关键词搜索：
   ```bash
   npx skills find react
   npx skills find react-components
   ```

2. 预览可用技能：
   ```bash
   npx skills add expo/skills -g --list
   ```

3. 阅读实际的 SKILL.md 内容以了解功能

4. 生成安装命令（正确避免使用 `--all`）：
   ```bash
   npx skills add expo/skills -g -s building-native-ui -a antigravity -a claude-code -a gemini-cli -a opencode -y
   ```

### 使用 skill-exporter

当用户想要备份他们的技能时：

1. 解析当前安装和锁定文件
2. 按源和智能体分组技能
3. 输出如下命令：
   ```bash
   npx skills add v5tech/skills -g -y -s skill-advisor -s skill-exporter -a antigravity -a claude-code -a gemini-cli -a opencode
   ```

## 参考文档

每项技能都在 `references/agents.md` 中包含完整的智能体目录参考：

### 目标智能体（默认）

| 智能体 | --agent | 全局路径 |
|-------|---------|---------|
| Antigravity | antigravity | ~/.gemini/antigravity/skills/ |
| Claude Code | claude-code | ~/.claude/skills/ |
| Gemini CLI | gemini-cli | ~/.gemini/skills/ |
| OpenCode | opencode | ~/.config/opencode/skills/ |

### 所有支持的智能体

39+ 个智能体，包括：amp、antigravity、augment、claude-code、openclaw、cline、codebuddy、codex、command-code、continue、crush、cursor、droid、gemini-cli、github-copilot、goose、junie、iflow-cli、kilo、kimi-cli、kiro-cli、kode、mcpjam、mistral-vibe、mux、opencode、openhands、pi、qoder、qwen-code、replit、roo、trae、trae-cn、windsurf、zencoder、neovate、pochi、adal

查看 [references/agents.md](skill-advisor/references/agents.md) 获取完整详情。

## 许可证

本项目采用 MIT 许可证 - 详情请参见 [LICENSE](LICENSE) 文件。

---

**作者**: [@v5tech](https://github.com/v5tech)  
**仓库**: [v5tech/skills](https://github.com/v5tech/skills)
