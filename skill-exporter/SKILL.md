---
name: skill-exporter
description: "Generate npx skills add commands to reproduce installed skills. Use when user wants to export, backup, share, or replicate their skills setup on another machine."
---

# Skill Exporter

Generate `npx skills add` commands from current installation.

## Workflow

1. Run `npx skills ls -g` and read `~/.agents/.skill-lock.json`
2. Parse skill names and agent lists from ls output
3. Extract source repos from lock file
4. Map agent display names to CLI values (see references/agents.md)
5. Group skills by (source, agent-set)
6. Output one command per group

## Parsing `npx skills ls -g`

Format:
```
<skill-name> <path>
  Agents: <Agent1>, <Agent2>, ...
```

Extract skill name (first word of non-indented line) and agents (comma-separated after "Agents:").

## Lock File

Path: `~/.agents/.skill-lock.json`

```json
{ "<skill-name>": { "source": "<owner/repo>", ... } }
```

## Command Format

```bash
npx skills add <source> -g -y -s <skill1> -s <skill2> -a <agent1> -a <agent2>
```

## Grouping

Group skills sharing same source repo AND same agent set into one command.

## Example

Input:
```
docx ~/.agents/skills/docx
  Agents: Antigravity, Claude Code
pdf ~/.agents/skills/pdf
  Agents: Antigravity, Claude Code
```

Lock: `docx` and `pdf` both have `"source": "anthropics/skills"`

Output:
```bash
npx skills add anthropics/skills -g -y -s docx -s pdf -a antigravity -a claude-code
```
