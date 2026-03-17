---
name: se-insights
description: Use at the start of every new conversation and after completing substantial feature implementations or bug fixes
---

# SE Insights

Bite-sized software engineering insights for passive learning while AI agents handle implementation. Two modes: startup and post-implementation.

## Startup Mode (every session)

Deliver one SE insight at the start of each conversation. **Run this non-blocking** — spawn a background agent so the user can start working immediately.

Spawn an Agent with `run_in_background: true`. The agent should:
1. Run `mkdir -p ~/.claude/insights`. Create `topics.md` (empty) and `log.md` (with `# SE Insights Log` header) if they don't exist.
2. Run `git log --oneline -20` for recent work context
3. Read `~/.claude/insights/topics.md` for covered topics
4. Pick an intermediate/advanced SE concept **adjacent** to recent work — the deeper concept it touches, not the code itself (e.g., DB migrations → write-ahead logging; WebSockets → C10K problem). No git context: infer from project file types. Topic covered: broaden or fall back to foundational SE topics (distributed systems, concurrency, type theory, networking, etc.)
5. Write 4-6 sentences: definition (1-2), why it matters (1-2), concrete example (1-2). Intermediate/advanced level — the "why behind the why." Tone: senior engineer at a whiteboard.
6. Persist to both files (see Persistence below)
7. Return the insight text

**Immediately proceed** to handle the user's request after spawning. When the agent completes, display the insight. Do NOT wait before responding.

## Post-Implementation Mode (Claude's judgment)

After completing substantial work, before moving on, pause and deliver an insight about the engineering behind what was just built.

**Trigger when:** 3+ files changed in a feature, root-cause bug fix, architecture refactor, new external integration, or schema migration.
**Skip when:** config/formatting changes, single-line edits, dependency updates, or user signals urgency ("quick fix", "just do X", production incidents).

Write 8-12 sentences covering:
- **What was done** — brief recap of the approach
- **Why this approach** — the engineering reasoning
- **Alternatives considered** — what else could have worked and why it wasn't chosen
- **Underlying SE concept** — the deeper principle at play (e.g., strategy pattern, eventual consistency, separation of concerns)

Tone: senior colleague doing a quick post-mortem, not lecturing.

## Output Format

Use this exact format (the box-drawing lines are literal characters to reproduce):

★ SE Insight ─────────────────────────────────────
[insight content here]
─────────────────────────────────────────────────────

## Persistence

After writing each insight, append to both files:

**`~/.claude/insights/topics.md`** — one line per insight for repeat avoidance:

YYYY-MM-DD | startup | Topic Name
YYYY-MM-DD | post-impl | Topic Name

**`~/.claude/insights/log.md`** — full entry for the knowledge base:

## YYYY-MM-DD — Topic Name (startup|post-implementation)
**Adjacent to:** what recent work prompted this
**Type:** startup|post-implementation
**Files:** (post-implementation only) relevant files

[Full insight text]

---
