---
description: Run the full build loop for one phase - implement, test, review, fix.
argument-hint: <phase number, e.g. 1>
---
Step 0 (gate): open docs/PLAN.md. If it has a Status line that does not say "approved", STOP and tell the human to review the plan (or run /review-plan) and set Status to approved. If there is no Status line at all (older project), ask the human once whether the plan is approved before continuing. Also STOP if the phase has unresolved open questions that block it.

Run the build loop for phase $ARGUMENTS of docs/PLAN.md. Use subagents in this order and keep each step's output short in the main thread.

1. `implementer`: implement the phase only.
2. `test-engineer`: write and run tests for the phase's acceptance criteria.
3. `code-reviewer`: review `git diff` against the base branch.
4. If the reviewer returned blocking issues or tests failed: send the findings back to `implementer` (and `test-engineer` if needed), then re-run steps 2-3. Maximum 3 loops; if still failing, stop and report to the human.
5. When APPROVE and green: tick the phase's checklist in docs/PLAN.md, and propose a conventional commit message (do not push).
6. Final report: what was built, test results, reviewer verdict, deferred items from docs/BACKLOG.md.
