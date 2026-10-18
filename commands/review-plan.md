---
description: Independent review loop for the spec docs. Reviewer critiques, planner revises, repeat, then stop for human approval.
argument-hint: [optional: extra focus, e.g. "security and realtime"]
---
Focus (optional): $ARGUMENTS

Run this loop on docs/SPEC.md, docs/ARCHITECTURE.md and docs/PLAN.md (the plan may be a single PLAN.md that contains the architecture; that is fine).

1. Invoke the `plan-reviewer` subagent. It writes docs/PLAN_REVIEW.md.
2. If the verdict is APPROVE, go to step 5.
3. Otherwise invoke the `planner` subagent in REVISE mode: give it docs/PLAN_REVIEW.md and tell it to fix every Blocking item and every Should-fix item it agrees with, editing the existing docs in place (do not rewrite from scratch, do not touch unrelated sections). Anything it rejects must be listed with a one-line reason in a "Review responses" section at the bottom of docs/PLAN_REVIEW.md.
4. Repeat from step 1. Maximum 3 rounds. If still REQUEST CHANGES after round 3, stop and report the remaining Blocking items.
5. STOP and report to the human: rounds run, what changed per round, remaining non-blocking items, rejected suggestions with reasons, and the open questions that still need a human decision. Leave the plan Status as "awaiting human approval". Do not start implementation.
