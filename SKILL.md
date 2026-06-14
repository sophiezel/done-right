---
name: done-right
description: >
  Execute coding tasks with engineering discipline: plan first, minimal changes, verify before claiming done, never abandon mid-task.
  Use when implementing features, fixing bugs, refactoring, or any non-trivial coding task.
  NOT for trivial edits (typos, one-liners, pure Q&A, single-line fixes).
---

# Done Right

Three iron laws. One execution rhythm. No excuses.

## Iron Laws

**1. Simplicity First.** Minimum code that solves the problem. Nothing speculative.
No features beyond what was asked. No abstractions for single-use code.
If 200 lines could be 50, rewrite it.
Test: Would a senior engineer call this overcomplicated? If yes, simplify.

**2. Surgical Changes.** Touch only what the task requires.
Don't "improve" adjacent code. Don't refactor unbroken things.
Match existing style. Every changed line must trace to the request.
Before editing any file: read its imports and callers. Know the blast radius.
If you notice unrelated dead code, mention it — don't delete it.
Exception for greenfield: within files you created this session, design freely. Surgical applies only to pre-existing files.

**3. Never Abandon.** Do not stop until ALL of:
- Every stated requirement is implemented
- Build/type-check passes (zero new errors)
- Tests pass (existing + new)
If stuck after 3 attempts on the same blocker, stop and report what's blocking and what you've tried. Do not silently switch to an easier approach.

## Execution Rhythm

Before writing any code, state a brief plan:
```
1. [Step] → verify: [concrete check]
2. [Step] → verify: [concrete check]
```

After each step, run the verification. Only proceed when it passes.

Before any implementation: run existing tests first. Orient to what's green and what's broken.
When implementing: use red/green TDD. Write the failing test, then the minimum code to pass it.

## Anti-Rationalization

| Agent says | Reality |
|-----------|---------|
| "I'll add tests later" | Tests will not be added later |
| "This abstraction will be useful" | Over-engineering single-use code |
| "I can simplify this later" | You won't come back. Simplify now or don't add complexity. |
| "While I'm here, I'll also fix..." | Scope creep — don't |
| "Looks like it should work" | Verify; never assume |
| "Task complete" (with unverified steps) | Task is not complete |

## Routing

- Bug with unclear cause → use `/diagnose` skill
- Unclear requirements → use `/grill-me` skill before starting
- Writing new code with tests → use `/tdd` skill
- Security-sensitive changes → flag and ask before proceeding
