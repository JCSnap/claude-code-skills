# Claude Code Skills

A collection of custom skills for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) by JCSnap. Each folder in `skills/` contains one skill.

## Skills

| Skill | Description |
|-------|-------------|
| [se-insights](./skills/se-insights/) | Bite-sized software engineering insights delivered at session start and after substantial implementations. Builds a personal SE knowledge base over time. Prevents brain rot from using Claude Code too much. |

## Installation

### Option 1: Plugin marketplace (recommended)

Install as a plugin directly from Claude Code:

```shell
/plugin marketplace add JCSnap/claude-code-skills
/plugin install cc-skills@jcsnap-skills
```

### Option 2: Manual install (symlink)

```bash
cd ~/Downloads && git clone https://github.com/JCSnap/claude-code-skills.git
ln -s ~/Downloads/claude-code-skills/skills/se-insights ~/.claude/skills/se-insights
```

### Option 3: Manual install (copy)

```bash
mkdir -p ~/.claude/skills/se-insights
curl -o ~/.claude/skills/se-insights/SKILL.md https://raw.githubusercontent.com/JCSnap/claude-code-skills/main/skills/se-insights/SKILL.md
```

### Verify installation

```bash
ls ~/.claude/skills/se-insights/SKILL.md
```

## Some skills may require CLAUDE.md additions

Check each skill's folder for any additional setup instructions (e.g., trigger lines to add to `~/.claude/CLAUDE.md`).

## Skill structure

```
skills/
  skill-name/
    SKILL.md    # Skill definition with YAML frontmatter (name + description)
    README.md   # Skill-specific documentation
```
