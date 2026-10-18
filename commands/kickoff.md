---
description: Start a new project. Planner drafts the docs, plan-reviewer iterates them, then stops for human approval.
argument-hint: <one-paragraph idea or paste your detailed prompt>
---
Project idea / brief:
$ARGUMENTS

1. Ensure CLAUDE.md exists in the repo root; if not, create it from ~/.claude/templates/CLAUDE.project.md and fill in what you can infer, marking unknowns as TODO.
2. Invoke the `planner` subagent with the brief above. Plan header must read: "Status: awaiting human approval".
3. Run the /review-plan loop (plan-reviewer critiques, planner revises, max 3 rounds).
4. Summarize: phases, key decisions, what the reviewer changed, open questions needing a human.
5. STOP. Do not implement anything until the human sets the plan Status to "approved".
