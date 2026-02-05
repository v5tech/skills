# v5tech/skills

[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub](https://img.shields.io/badge/GitHub-v5tech/skills-black?logo=github)](https://github.com/v5tech/skills)

**[English](README.md) | [中文](README.zh.md)**

AI agent skills collection for development workflow optimization. This repository provides curated skills to enhance productivity across multiple AI coding agents.

---

## Overview

This project contains specialized skills designed for AI agents like Claude Code, Gemini CLI, OpenCode, and Antigravity. Each skill provides domain-specific guidance and workflows to help developers accomplish tasks more efficiently.

## Features

- **Multi-agent support**: Compatible with 39+ AI agents including Claude Code, Gemini CLI, OpenCode, Antigravity
- **Workflow optimization**: Pre-built skills for common development scenarios
- **Easy installation**: Simple `npx skills` CLI integration
- **Best practices**: Avoid common pitfalls with detailed guidance

## Skills

### skill-advisor

Guide for searching, comparing, and installing skills with npx skills CLI.

**Use when**: User wants to find skills, compare skill functionality, or install skills to specific agents.

**Key capabilities**:
- Search skills with multiple keywords
- Preview skill content before installation
- Compare skills across multiple dimensions (quality, coverage, tech stack match, etc.)
- Generate correct installation commands for target agents
- **Avoids common pitfalls** like the `--all` flag that overrides `--agent` settings

**Default target agents**: Antigravity, Claude Code, Gemini CLI, OpenCode

**Installation example**:
```bash
# Install skill-advisor to all 4 default agents
npx skills add v5tech/skills -g -s skill-advisor -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

### skill-exporter

Generate `npx skills add` commands to reproduce installed skills.

**Use when**: User wants to export, backup, share, or replicate their skills setup on another machine.

**Key capabilities**:
- Parse current installation from `npx skills ls -g`
- Read source repositories from lock file (`~/.agents/.skill-lock.json`)
- Group skills by source and agent-set
- Output optimized installation commands

**Installation example**:
```bash
# Install skill-exporter to all 4 default agents
npx skills add v5tech/skills -g -s skill-exporter -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

## Installation

### Install All Skills

```bash
# Install both skills to default agents
npx skills add v5tech/skills -g -s skill-advisor -s skill-exporter -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

### Install to Custom Agents

```bash
# Example: Install to Cursor and Windsurf
npx skills add v5tech/skills -g -s skill-advisor -s skill-exporter -a cursor -a windsurf -y
```

### Verify Installation

```bash
# List installed skills and their agents
npx skills ls -g

# Check skill files in agent directories
ls -la ~/.claude/skills/
ls -la ~/.gemini/skills/
ls -la ~/.config/opencode/skills/
```

## Project Structure

```
skills/
├── README.md                    # English documentation (this file)
├── README.zh.md                 # Chinese documentation
├── skill-advisor/
│   ├── SKILL.md                 # Skill definition and workflow
│   └── references/
│       └── agents.md            # Complete agent directory reference
└── skill-exporter/
    ├── SKILL.md                 # Skill definition and workflow
    └── references/
        └── agents.md            # Complete agent directory reference
```

## Usage Examples

### Using skill-advisor

When a user asks "How do I find skills for React?":

1. The skill-advisor will guide you to search with multiple keywords:
   ```bash
   npx skills find react
   npx skills find react-components
   ```

2. Preview available skills:
   ```bash
   npx skills add expo/skills -g --list
   ```

3. Read actual SKILL.md content to understand functionality

4. Generate installation commands (correctly avoiding `--all`):
   ```bash
   npx skills add expo/skills -g -s building-native-ui -a antigravity -a claude-code -a gemini-cli -a opencode -y
   ```

### Using skill-exporter

When a user wants to backup their skills:

1. Parse current installation and lock file
2. Group skills by source and agents
3. Output commands like:
   ```bash
   npx skills add v5tech/skills -g -y -s skill-advisor -s skill-exporter -a antigravity -a claude-code -a gemini-cli -a opencode
   ```

## References

Each skill includes a complete agent directory reference at `references/agents.md`:

### Target Agents (Default)

| Agent | --agent | Global Path |
|-------|---------|-------------|
| Antigravity | antigravity | ~/.gemini/antigravity/skills/ |
| Claude Code | claude-code | ~/.claude/skills/ |
| Gemini CLI | gemini-cli | ~/.gemini/skills/ |
| OpenCode | opencode | ~/.config/opencode/skills/ |

### All Supported Agents

39+ agents including: amp, antigravity, augment, claude-code, openclaw, cline, codebuddy, codex, command-code, continue, crush, cursor, droid, gemini-cli, github-copilot, goose, junie, iflow-cli, kilo, kimi-cli, kiro-cli, kode, mcpjam, mistral-vibe, mux, opencode, openhands, pi, qoder, qwen-code, replit, roo, trae, trae-cn, windsurf, zencoder, neovate, pochi, adal

See [references/agents.md](skill-advisor/references/agents.md) for complete details.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Author**: [@v5tech](https://github.com/v5tech)  
**Repository**: [v5tech/skills](https://github.com/v5tech/skills)
