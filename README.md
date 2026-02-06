# Skills

[![中文文档](https://img.shields.io/badge/文档-中文版-blue)](README.zh-CN.md)

A collection of agent skills for Claude Code, Gemini CLI, and other AI coding assistants.

## Available Skills

| Skill | Description |
|-------|-------------|
| [skill-advisor](skill-advisor/) | Search, compare, and install skills via `npx skills` CLI |
| [skill-exporter](skill-exporter/) | Generate install commands to backup/replicate your skills setup |

## Installation

Install skills using the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
# Install all skills to default agents
npx skills add v5tech/skills -g -s skill-advisor -s skill-exporter -a antigravity -a claude-code -a gemini-cli -a opencode -y

# Install a specific skill
npx skills add v5tech/skills -g -s skill-advisor -a claude-code -y
```

## Default Target Agents

| Agent | `--agent` value |
|-------|-----------------|
| Antigravity | `antigravity` |
| Claude Code | `claude-code` |
| Gemini CLI | `gemini-cli` |
| OpenCode | `opencode` |

## Verify Installation

```bash
npx skills ls -g
```

## License

MIT
