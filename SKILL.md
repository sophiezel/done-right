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
No abstractions for single-use code. 200 lines → 50? Rewrite.
Would a senior engineer call this overcomplicated? If yes, simplify.

Simplicity is not an excuse for fragility. More code IS justified when:
- Shared mutable state needs explicit locking or ownership rules
- External input has no validation hook — a missing guard is a production incident
- A failure has no log — silent failures become mystery outages
If you add code for these reasons, state it in the plan: "extra lines because [risk]."

**2. Surgical Changes.** Touch only what the task requires.
Don't "improve" adjacent code. Don't refactor unbroken things.
Match existing style. Every changed line must trace to the request.
Before editing any file: read its imports and callers. Know the blast radius.
A 3-line fix that breaks 12 tests means those 3 lines were a de facto interface
for 12 consumers you didn't know about. The blast radius is never obvious.
If you notice unrelated dead code, mention it — don't delete it.
Exception for greenfield: within files you created this session, design freely. Surgical applies only to pre-existing files.

**3. Never Abandon.** Do not stop until ALL of:
- Every stated requirement is implemented
- Build/type-check passes (zero new errors)
- Tests pass (existing + new)
If stuck after 3 attempts on the same blocker, stop. Report:
- Exact error (copy-pasted, not paraphrased)
- Each approach tried and why it failed
- Which assumption to challenge: "what if [premise] is wrong?"
Do not silently switch to an easier approach.

**When a law blocks faster progress, violate it openly:** state the violation
and why in your plan, then return to the law afterward. The laws are levers,
not handcuffs.

## Execution Rhythm

Before writing any code, state a brief plan:
```
1. [Step] → verify: [concrete check]
2. [Step] → verify: [concrete check]
```

After each step, run the verification. Only proceed when it passes.

Before any implementation: run existing tests first. Orient to what's green and what's broken.
When implementing: use red/green TDD. Write the failing test, then the minimum code to pass it.

Before declaring done, run the self-check:
- [ ] Every changed line traces to the request (no "while I was here...")
- [ ] No new abstractions for single-use code
- [ ] All verifications actually passed (not assumed). Check exit codes, not output appearance.

## Anti-Rationalization

| Agent says | Reality |
|-----------|---------|
| "I'll add tests later" | Tests will not be added later |
| "This abstraction will be useful" | Over-engineering single-use code |
| "I can simplify this later" | You won't come back. Simplify now or don't add complexity. |
| "While I'm here, I'll also fix..." | Scope creep — don't |
| "Looks like it should work" | Verify; never assume |
| "Task complete" (with unverified steps) | Task is not complete |
| "I tested the happy path" | You didn't test null, empty, boundary, or concurrent. |
| "The existing tests still pass" | Tests pass because they don't cover what you changed. |

## Routing

| Situation | Action |
|-----------|--------|
| Bug with unclear cause | use `/diagnose` skill |
| Unclear requirements | use `/grill-me` skill before starting |
| Writing new code with tests | use `/tdd` skill |
| Security-sensitive changes | flag and ask before proceeding |
| Tests broken before start | Fix to green first. If >3 test files broken, flag and ask. |
| Simple typo / one-liner / pure Q&A | This skill should NOT be active. Disengage. |
