# Recovery Operations

Procedures for removing, reinstalling, and fixing skill installations.

## Contents

- [Remove from Specific Agent](#remove-from-specific-agent)
- [Remove from All Agents](#remove-from-all-agents)
- [Reinstall to Specific Agents](#reinstall-to-specific-agents)
- [Batch Cleanup](#batch-cleanup)
- [Verification Checklist](#verification-checklist)

## Remove from Specific Agent

**Goal**: Remove skill from one agent while keeping it for others.

**Operation**: Delete only the symlink, preserve source files.

```bash
# Claude Code
rm ~/.claude/skills/SKILL_NAME

# Gemini CLI
rm ~/.gemini/skills/SKILL_NAME

# Antigravity
rm ~/.gemini/antigravity/skills/SKILL_NAME

# OpenCode
rm ~/.config/opencode/skills/SKILL_NAME
```

Source files in `~/.agents/skills/` remain intact.

## Remove from All Agents

**Goal**: Fully remove skill, delete source files, clean all symlinks.

```bash
# Step 1: CLI removes source files + lock records
npx skills remove -g -s SKILL_NAME -y

# Step 2: Clean orphaned symlinks (CLI may miss some)
for dir in ~/.claude/skills ~/.gemini/skills ~/.gemini/antigravity/skills ~/.config/opencode/skills; do
  [ -L "$dir/SKILL_NAME" ] && rm "$dir/SKILL_NAME" && echo "Cleaned: $dir/SKILL_NAME"
done
```

## Reinstall to Specific Agents

**Goal**: Clean removal then reinstall to specified agents.

```bash
# Step 1: Remove source files
npx skills remove -g -s SKILL_NAME -y

# Step 2: Clean symlinks
for dir in ~/.claude/skills ~/.gemini/skills ~/.gemini/antigravity/skills ~/.config/opencode/skills; do
  [ -L "$dir/SKILL_NAME" ] && rm "$dir/SKILL_NAME"
done

# Step 3: Reinstall
npx skills add owner/repo -g -s SKILL_NAME -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

## Batch Cleanup

When installation went wrong (e.g., used `--all` by accident):

### Step 1: Remove skill source files

```bash
# Single skill
npx skills remove -g -s SKILL_NAME -y

# Multiple skills
npx skills remove -g -s skill1 -s skill2 -y
```

### Step 2: Clean all symlinks in target directories

```bash
for dir in ~/.claude/skills ~/.gemini/skills ~/.gemini/antigravity/skills ~/.config/opencode/skills; do
  [ -d "$dir" ] && find "$dir" -maxdepth 1 -type l -delete -print
done
```

### Step 3: Check unwanted agent directories

Only delete if:
- Directory was newly created by skills CLI
- Contains only empty `skills/` subdirectory
- Has no other files

```bash
# Check before deleting
ls -la ~/.cursor/
find ~/.cursor/ -type f | wc -l  # Must be 0 to safely delete
```

### Step 4: Reinstall correctly

```bash
npx skills add owner/repo -g -s skill1 -s skill2 -a antigravity -a claude-code -a gemini-cli -a opencode -y
```

## Verification Checklist

After any recovery operation:

```
Recovery Verification:
- [ ] npx skills ls -g shows expected skills
- [ ] Symlinks exist in target agent directories
- [ ] No broken symlinks (ls -la shows valid targets)
- [ ] No unwanted agent directories created
```
