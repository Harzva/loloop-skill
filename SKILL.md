---
name: loloop
description: Use when a task should advance through repeated plan-driven loop cycles for an engineering project, paper, or long-running repo change. loloop wraps the official /loop idea with the repo's loop-in-loop method: read the current plan, inspect prior evolution notes, execute the current iteration, write a new evolution record, draft the next plan when a version is complete, and prepare the next /loop handoff.
---

# loloop

`loloop` is a local skill for long-horizon work that should keep evolving instead of stopping after one implementation pass.

It does not replace the official `/loop`.
It packages your repo's `loop in loop` method around it.
At the current stage it is a **skill**, not a built-in slash command.

## When to use

Use this skill when the user wants any of these:

- continue a project by iterating against a plan file
- keep evolving a repo or paper over multiple versions
- read prior "evolution" notes before deciding the next iteration
- finish one plan, then immediately draft the next version
- prepare or trigger another `/loop` run with a better prompt

## Core idea

`loloop` follows this pattern:

1. Lock onto one current plan file.
2. Execute a bounded iteration against that plan.
3. Record what changed, what failed, and what remains.
4. If the plan is complete, write the next versioned plan.
5. End with an explicit next `/loop` handoff so the process can recurse.

## Invocation model

Current form:

- ask the agent to use `loloop`
- let `loloop` generate or refine the next `/loop` handoff

Intended future form:

- provide a dedicated `/loloop ...` command
- let that command wrap the official `/loop`

## Files and conventions

- General plans: `.claude/plans/*.md`
- loloop-specific plan docs: `.claude/plans/loloop/*.md`
- Raw run logs: `.claude/logs/loloop/*.log`
- Evolution note pattern: `.claude/plans/loloop/evolution-YYYY-MM-DD-short-slug.md`

Use `templates/evolution-entry.md` as the default structure.

## Workflow

### 1. Anchor on the active plan

Prefer:

- a plan explicitly named by the user
- the newest relevant `active-*.md` in `.claude/plans/loloop/`
- the newest relevant file in `.claude/plans/`

### 2. Read recent evolution notes

Read the most recent relevant `evolution-*.md` notes from `.claude/plans/loloop/`.

### 3. Define one bounded loop target

Reduce the current iteration to:

- one active plan
- one bounded slice
- one clear success condition

### 4. Execute

- edit files
- run checks
- update docs
- validate results

### 5. Review

Each iteration should include explicit review checkpoints:

- before the iteration
- during the iteration if drift/failure appears
- after the iteration

### 6. Recurse

- continue the same plan if unfinished
- draft the next plan if the current plan is complete
- always finish with the next `/loop` handoff
