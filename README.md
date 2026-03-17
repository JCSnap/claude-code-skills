# Claude Code Skills

A collection of custom skills for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) by JCSnap. Each folder contains one skill.

## Skills

| Skill | Description |
|-------|-------------|
| [se-insights](./se-insights/) | Bite-sized software engineering insights delivered at session start and after substantial implementations. Builds a personal SE knowledge base over time. Prevents brain rot for using claude code too much. |

## Installation

### 1. Clone the repo

```bash
cd ~/Downloads && git clone https://github.com/JCSnap/claude-code-skills.git
```

### 2a. Quick install (symlink)

Symlink a skill folder into your Claude Code skills directory:

```bash
ln -s ~/Downloads/claude-code-skills/se-insights ~/.claude/skills/se-insights
```

### 2b. Manual install (copy)

```bash
mkdir -p ~/.claude/skills/se-insights
cp ~/Downloads/claude-code-skills/se-insights/SKILL.md ~/.claude/skills/se-insights/SKILL.md
```

### Verify installation

```bash
ls ~/.claude/skills/se-insights/SKILL.md
```

If the file exists, the skill is installed and will be auto-discovered by Claude Code.

## Skill structure

Each skill follows the Claude Code skill format:

```
skill-name/
  SKILL.md    # Skill definition with YAML frontmatter (name + description)
```

The `SKILL.md` file contains:
- **Frontmatter** (`---` block) — `name` and `description` fields for auto-discovery
- **Body** — instructions Claude follows when the skill is invoked

## Some skills may require CLAUDE.md additions

Check each skill's folder for any additional setup instructions (e.g., trigger lines to add to `~/.claude/CLAUDE.md`).
