---
name: skill-advisor
description: "Guide for searching, comparing, and installing skills with npx skills CLI. Use when user wants to find skills, compare skill functionality, or install skills to specific agents. Helps avoid common pitfalls like --all flag and generates correct installation commands for target agents (default: Antigravity, Claude Code, Gemini CLI, OpenCode)."
---

# Skill Advisor

Help users search, compare, and install skills correctly to their preferred agents.

## Default Target Agents

Install skills globally to these 4 agents by default:

| Agent | --agent value |
|-------|---------------|
| Antigravity | antigravity |
| Claude Code | claude-code |
| Gemini CLI | gemini-cli |
| OpenCode | opencode |

User can customize this list by specifying different agents.

## Workflow

### Step 1: Search Skills

Search with multiple related keywords for better coverage:
```bash
npx skills find [query]
npx skills find [related-query]
```

### Step 2: Preview Skill Content

Before comparing, preview each repository's available skills:
```bash
npx skills add <owner/repo> -g --list
```

For promising skills, read the actual SKILL.md to understand real functionality. Visit:
```
https://skills.sh/<owner>/<repo>/<skill>
```

**Never rely solely on skill names to judge functionality.** Names can be misleading.

### Step 3: Compare and Recommend

Evaluate each skill on these dimensions:

| Dimension | How to Assess | Weight |
|-----------|---------------|--------|
| **Content quality** | Read SKILL.md — does it contain actionable guidance, scripts, or references? Or is it generic/empty? | High |
| **Coverage systematics** | Are multiple skills from the same author forming a coherent system? | High |
| **Tech stack match** | Does the skill match the user's current project tech stack? | High |
| **Source authority** | Official (e.g., expo/skills) > Well-known org > Individual | Medium |
| **Maintenance activity** | Repository update date, commit frequency | Medium |
| **Depth vs breadth** | Deep expertise in one area vs shallow generic guidance | Medium |
| **Function overlap** | Does it duplicate functionality of another found skill? | Medium |
| **Dependencies** | Do multiple skills need to work together? | Low |

**Comparison output format:**

```
## Recommended (Category/Author)
| Skill | Function | Quality | Note |
|-------|----------|---------|------|
| skill-a | Actual function from SKILL.md | High/Medium/Low | Why recommended |

## Optional
| Skill | Function | Quality | Note |
|-------|----------|---------|------|
| skill-b | Actual function from SKILL.md | Medium | Supplements skill-a |

## Not Recommended
| Skill | Function | Quality | Note |
|-------|----------|---------|------|
| skill-c | Actual function from SKILL.md | Low | Overlaps with skill-a, lower quality |
```

**Quality assessment criteria:**
- **High**: Contains scripts, detailed references, concrete examples, actionable workflows
- **Medium**: Has useful guidance but mostly text-based instructions
- **Low**: Generic/vague content, could be replaced by general LLM knowledge

### Step 4: Generate Install Commands

**CRITICAL: Never use `--all` flag** — it overrides `--agent` and installs to ALL agents.

Correct command pattern:
```bash
npx skills add <owner/repo> -g -s <skill1> -s <skill2> -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

**Parameter reference:**
| Parameter | Meaning |
|-----------|---------|
| `-g, --global` | Global install (user-level) |
| `-s, --skill <skills>` | Specify skill names (multiple values accepted, use `'*'` for all) |
| `-a, --agent <agents>` | Target agents (multiple values accepted, use `'*'` for all) |
| `-y, --yes` | Skip confirmation |
| `-l, --list` | List available skills without installing |
| `--all` | Install all skills to all agents without prompts |
| `--full-depth` | Search all subdirectories even when a root SKILL.md exists |

**Wrong vs Right:**
```bash
# WRONG — --all overrides -a, installs to ALL 40+ agents
npx skills add expo/skills -g -a antigravity -a claude-code -a gemini-cli -a opencode --all

# RIGHT — repeat -s for each skill, -a for each agent
npx skills add expo/skills -g -s building-native-ui -s expo-deployment -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

### Step 5: Verify Installation

```bash
# List installed skills and their agents
npx skills ls -g

# Check symlinks are valid in each agent directory
ls -la ~/.claude/skills/
ls -la ~/.gemini/skills/
ls -la ~/.gemini/antigravity/global_skills/
ls -la ~/.config/opencode/skills/

# Verify no extra agent directories created
ls ~/.cursor/ ~/.cline/ ~/.copilot/ 2>/dev/null
```

## Recovery: Cleanup After Mistakes

When installation goes wrong (e.g., used `--all` by accident):

### 1. Remove skills from all agents
```bash
# Remove specific skills from all agents
npx skills remove -g -s <skill1> -s <skill2> --agent '*' -y

# Or use --all shorthand (equals --skill '*' --agent '*' -y)
npx skills remove -g --all
```

### 2. Identify and clean empty directories
Check each non-target agent directory. Only delete if:
- Directory was newly created by skills CLI
- Contains only an empty `skills/` subdirectory
- Has no other files (file count = 0)

```bash
# Check a directory before deleting
ls -la ~/.cursor/
find ~/.cursor/ -type f | wc -l  # Must be 0 to safely delete
```

### 3. Reinstall correctly
```bash
npx skills add <owner/repo> -g -s <skill1> -s <skill2> -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

## Update Skills

```bash
npx skills check     # Check for available updates
npx skills update    # Update all installed skills
```

## Agent Directory Reference

See `references/agents.md` for the complete list of all 40 agents and their global paths.

| Agent | Global Path |
|-------|-------------|
| Antigravity | ~/.gemini/antigravity/global_skills/ |
| Claude Code | ~/.claude/skills/ |
| Gemini CLI | ~/.gemini/skills/ |
| OpenCode | ~/.config/opencode/skills/ |

## Common Pitfalls

1. **`--all` flag**: Overrides `--agent`, installs to 40+ agents, creates unwanted directories
2. **Forgetting `-g`**: Without global flag, installs to project only
3. **Missing `-s`**: Without specifying skills, may install all or prompt interactively
4. **Trusting skill names**: Always read SKILL.md content before recommending
