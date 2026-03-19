---
name: workflow-orchestration
description: >
  Framework for orchestrating AI agents that plan, verify, and improve themselves over time. Use when the user says: 'orchestrate this workflow', 'set up agent orchestration', 'plan-verify-improve loop', 'self-improving agents', 'multi-agent workflow', 'autonomous task pipeline', or asks how to make Claude plan before acting, use subagents effectively, track lessons learned, or build self-correcting AI workflows.
  Do NOT trigger for: simple one-off tasks (just do them), writing code without orchestration needs (use web-coding-assistant), designing visual workflows (use visual-workflow-builder), converting workflows to manual docs (use workflow-to-manual-skill), or general architecture questions (use architecture).
---

# Workflow Orchestration

A framework for AI agents that plan before acting, verify before marking done, and improve from every mistake.

---

## Phase 1: Plan Before Building

Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions).

### Process

1. **Assess complexity**: If the task has 3+ steps, touches multiple files, or involves architectural decisions → enter plan mode. Simple, obvious fixes → skip planning.
2. **Write a spec**: Define what success looks like before writing code. Include inputs, outputs, constraints, and edge cases.
3. **Break into checkable tasks**: Write plan to `tasks/todo.md` with checkable items (`- [ ] task`).
4. **Check in**: Share the plan with the user before starting implementation.
5. **Re-plan on failure**: If something goes sideways, STOP and re-plan immediately — don't keep pushing a broken approach.

---

## Phase 2: Use Subagents Strategically

Keep the main context window clean by offloading work to subagents.

### When to Use Subagents

| Scenario | Action |
|----------|--------|
| Research or exploration | Spawn a subagent to investigate and report back |
| Parallel analysis (e.g., check 3 files) | Spawn multiple subagents concurrently |
| Complex problem needing more compute | Throw more subagents at it |
| Simple, single-file edit | Do it yourself — subagent overhead isn't worth it |

### Rules

- One task per subagent for focused execution
- Give subagents clear, self-contained prompts (they don't share your context)
- Use subagent results to inform your next move — don't duplicate their work

---

## Phase 3: Self-Improvement Loop

After ANY correction from the user, capture the lesson so it never happens again.

### Process

1. **Detect correction**: User says "no", "don't do that", "that's wrong", or redirects your approach.
2. **Extract the pattern**: What category of mistake was this? (e.g., "assumed X without checking", "over-engineered Y")
3. **Write a rule**: Add to `tasks/lessons.md` in this format:

```markdown
## [Category]
- **Mistake**: [What went wrong]
- **Rule**: [Concrete rule to prevent recurrence]
- **Example**: [Specific instance]
```

4. **Review at session start**: Read `tasks/lessons.md` at the beginning of each session for the relevant project.
5. **Iterate**: If the same category appears 3+ times, the rule isn't specific enough — rewrite it.

---

## Phase 4: Verify Before Done

Never mark a task complete without proving it works.

### Verification Checklist

- [ ] Run tests — all pass
- [ ] Check logs — no errors or warnings
- [ ] Diff behavior — compare main vs. your changes when relevant
- [ ] Self-review — "Would a staff engineer approve this?"
- [ ] Demonstrate correctness — show the user evidence, not just assertions

### For Bug Fixes

- Point at logs, errors, failing tests → then resolve them
- Zero context switching required from the user
- Fix failing CI tests autonomously — don't ask how

---

## Phase 5: Demand Elegance (Balanced)

- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution."
- Skip this for simple, obvious fixes — don't over-engineer.
- Challenge your own work before presenting it.

---

## Output Format

### tasks/todo.md Structure

```markdown
# [Project/Task Name]

## Plan
- [ ] Step 1: [description]
- [ ] Step 2: [description]
- [x] Step 3: [completed step]

## Review
- **What worked**: [summary]
- **What didn't**: [summary]
- **Changes from plan**: [deviations and why]
```

### tasks/lessons.md Structure

```markdown
# Lessons Learned

## Over-Engineering
- **Mistake**: Added abstraction layer for a one-time operation
- **Rule**: Don't create helpers/utilities for single-use code. Three similar lines > premature abstraction.
- **Example**: Created a `formatResponse()` helper called exactly once

## Assumptions
- **Mistake**: Assumed API returned paginated results without checking
- **Rule**: Always read the API response shape before writing parsing code
- **Example**: Wrote pagination loop for an endpoint that returns all results at once
```

### Progress Updates

At each milestone, give the user a brief update:

```
✅ Step 2/5 complete: Database schema migrated
   Next: Updating API endpoints to match new schema
```

---

## Core Principles

- **Simplicity first**: Make every change as simple as possible. Impact minimal code.
- **No laziness**: Find root causes. No temporary fixes. Senior developer standards.
- **Minimal impact**: Changes should only touch what's necessary. Avoid introducing bugs.
- **Plan → Build → Verify → Learn**: This is the loop. Every task follows it.
