# loloop

`loloop` is a reusable skill package for long-horizon project iteration.

It wraps the official `/loop` workflow with a stronger discipline:

- lock onto one active plan
- execute one bounded slice
- review what changed and what failed
- write evolution notes
- produce the next `/loop` handoff

## Design background

This skill was extracted from the `learn-likecc` repo's existing `loop in loop` method.

The design goal is not to replace `/loop`.
The goal is to make `/loop` more durable for engineering or paper iteration by forcing:

- plan anchoring
- in-loop correction
- post-iteration review
- recursive handoff into the next loop

## Package contents

- `SKILL.md`
- `references/loop-in-loop-method.md`
- `templates/evolution-entry.md`
- `TEST-RESULT.md`

## Recommended workspace layout

```text
.claude/
  skills/
    loloop/
  plans/
    loloop/
      active-*.md
      draft-*.md
      archive-*.md
      evolution-*.md
  logs/
    loloop/
      *.log
```

## Example usage

```text
请使用 loloop，基于 .claude/plans/loloop/active-loloop-validation-plan-v1.md 启动一次迭代。
先读取最近的 evolution 记录；
完成一轮最小可验证推进；
最后写 evolution note，并给出下一轮 /loop handoff。
```

## Current status

This package has already passed one self-hosted forward-test inside `learn-likecc`.
See `TEST-RESULT.md` for the result summary.

## Experiment log

The first validation pass used `loloop` to validate and tighten its own working structure.

Active plan:

- `.claude/plans/loloop/active-loloop-validation-plan-v1.md`

Observed actions in the run log:

```text
[2026-04-10 19:39:53] Start loloop self-validation run
[2026-04-10 19:39:53] Goal: validate loloop on a real project-local iteration
[2026-04-10 19:39:53] Active plan: .claude/plans/loloop/active-loloop-validation-plan-v1.md
[2026-04-10 19:39:53] Actions:
[2026-04-10 19:39:53] - create final loloop plan/log layout
[2026-04-10 19:39:53] - update skill path conventions
[2026-04-10 19:39:53] - create naming guide
[2026-04-10 19:39:53] - prepare validation docs
```

This run confirmed that `loloop` can:

- anchor itself on one active plan
- produce a review/evolution note
- split reusable skill definitions from project-instance plans and raw logs
- generate the next `/loop` handoff cleanly
