---
name: ren-pushback-vault
description: When the user substantively pushes back on your approach or design and that pushback resolves into a changed direction, write a concise markdown entry to /Users/jcjustin/Projects/tippytop/pushback-vault and commit it. Trigger automatically (the user does not need to ask) on questioning, reframing, root-cause diagnoses, Socratic challenges, or approach corrections that materially change what you do. Skip trivial corrections (typos, syntax preferences) and unresolved disagreements.
---

# Pushback Vault

When the user pushes back on something you said or did — and that pushback resolves into a real change — capture it in `/Users/jcjustin/Projects/tippytop/pushback-vault/` and commit it. **This is automatic. The user does not have to ask.**

## Why this exists

When the user pushes back during a conversation, you often defend the existing direction across several turns before conceding. By the time the conversation ends, that resistance has been quietly replaced with the better answer — but the *learning* lives in the diff between your initial position and the final one. The vault captures that diff so the user can read back later and you can read back to recognize patterns in your own reasoning.

The vault is not a complaint log. It's a record of decisions that moved because of the user's input, written so a future reader can reconstruct the why.

## When to trigger

A pushback episode has three parts: **(1)** user pushes back, **(2)** you initially defend or partially concede, **(3)** the conversation resolves into a changed approach. **Write the entry at step 3**, not at step 1. Writing too early risks capturing a "resolution" that gets reversed two turns later.

### Substantive pushback (write it up)

- **Design challenges** — "why are we doing X this way?", "couldn't we do Y instead?", "isn't this overcomplicated?"
- **Root-cause diagnoses** — user identifies a root cause you'd been describing as a symptom: "is it because Z?"
- **Socratic challenges** — user asks a leading question to expose an inconsistency or precedent you missed
- **Reframings** — user restates the issue more sharply than you had: "as in like, X isn't compulsory..."
- **Approach corrections** — "no, use the existing helper instead of writing a new one"
- **Constraint reminders that change a decision** — e.g., "remember, this needs to work offline" — only if it actually changed what you did

### Not substantive (skip)

- Typos, formatting nits, syntax preferences ("use python3 not python")
- Pure clarification questions where the user wasn't challenging you
- Disagreements that ended without resolution — wait until they resolve, or skip if they never do
- Re-reads where the user just wanted you to look at something again

### Detecting resolution

A pushback has resolved when **at least one** of the following holds, and the conversation has moved forward for at least one turn:

- You've changed your stated position ("you're right", "let me reconsider", "good catch")
- You've implemented the user's suggestion (code is in place, file is edited)
- The user has confirmed a new direction and is talking about something else

If you write an entry and the resolution gets reversed later in the same session, edit or delete the file rather than leaving a stale snapshot.

### Self-reference guard

This skill captures pushback that arises *organically during work*. If the user is explicitly invoking this skill — e.g., "vault this", "write up that pushback", "create a pushback entry" — that's a direct request, not an automatic trigger. Follow it as a request without invoking the skill recursively to log the act of being asked.

## Writeup format

Use this exact template. Keep entries under ~50 lines so they stay scannable.

```markdown
# Pushback — <topic in 3-7 words>

**Date:** YYYY-MM-DD
**Scope:** <repo / area / project — e.g., "ren, ren-backend (feat/hybrid-grading)" or "general workflow">

## Context

<One paragraph. What were we doing? What was the design / approach / claim I was defending? Why was the user engaging with it?>

## The pushback(s)

### 1. <Short label for this push>

> "<verbatim quote of the user's message>"

<1-3 sentences. What was I doing before? Where did I give ground in response?>

### 2. <Short label> — only if there were distinct moves

> "<verbatim quote>"

<as above>

## What changed

<3-6 bullets. Concrete deliverables: schema changes, code refactors, design pivots, things removed. Make the resolved outcome legible.>

## Pattern to notice next time

<1-3 sentences. What was the reasoning failure mode? What would have shortcut the conversation if I'd done it in turn 1?>
```

### Choosing what to include

Two or three pushbacks is usually enough. If the user pushed back five times on the same point before you conceded, that's one episode with one or two load-bearing moves, not five entries. Use judgment about which exchanges actually shifted the design vs. which were friction on the way to the same shift.

The **Pattern to notice next time** section is the most valuable part for future-you. Be honest about the failure mode (defending the existing design reflexively, missing a precedent already in the codebase, generating plausible-sounding justifications without naming the core mechanism) rather than describing the disagreement neutrally. The point is calibration, not a chronological transcript.

### Tone

Honest about reasoning failures, not self-flagellating. *"I defended the existing design across three turns before conceding"* is good. *"I was completely wrong and should have known better"* is not — it's both inaccurate and useless for future calibration. The user wants to learn from these, not read apologies.

## File path and naming

- **Directory:** `/Users/jcjustin/Projects/tippytop/pushback-vault/`
- **Filename:** `YYYY-MM-DD-<kebab-case-slug>.md`
- **Slug:** 3-6 words describing the topic — `assignment-mode-source-of-truth`, `migration-backfill-orphans`, `worktree-test-discovery`

If a file with the same date+slug already exists, append a suffix (`-2`, `-3`). Use today's date (`date +%F`), not the date of the original disagreement if you're catching up retroactively.

## Committing

After writing the file, commit it without prompting:

```bash
cd /Users/jcjustin/Projects/tippytop && \
git add pushback-vault/<filename>.md && \
git commit -m "vault: <kebab-slug>"
```

Use a short conventional commit message. Do **not** add `Co-Authored-By` trailers (the user's global instruction forbids them). Do **not** push — the vault is local-history, not a published artifact.

If `/Users/jcjustin/Projects/tippytop` is not a git repo (or the vault folder lives outside one), check first with `git -C /Users/jcjustin/Projects/tippytop rev-parse --is-inside-work-tree` and skip the commit step if it's not tracked. Tell the user so they know.

## What to tell the user

After writing + committing, send a one-liner so they know it happened:

> Vaulted: `pushback-vault/2026-05-18-assignment-mode-source-of-truth.md` — committed.

No further explanation needed unless the user asks. Avoid making the vault entry itself part of the conversation — write it quietly and move on.
