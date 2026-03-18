# autoresearch — Skill Improvement

This is an experiment to have the LLM autonomously improve Claude Code skills.

## Setup

To set up a new experiment, work with the user to:

1. **Agree on a run tag and skill**: The user specifies a skill name (matching `~/.claude/skills/<skill-name>/SKILL.md`) and a branch tag.
2. **Create the branch**: `git checkout -b skill-research/<tag>` from current master.
3. **Copy the skill**: Copy `~/.claude/skills/<skill-name>/SKILL.md` into `target/SKILL.md` in this repo. This is the file you will iterate on.
4. **Read the rubric**: Read `score.md` — it defines the 3 scoring dimensions (trigger clarity, instruction completeness, output specificity), each 1–5, total out of 15.
5. **Establish baseline**: Score the skill as-is using the rubric. Record the baseline in `results.tsv`.
6. **Initialize results.tsv**: Create `results.tsv` with header and baseline row.
7. **Begin the loop**.

## Scoring

Use the rubric in `score.md`. For each of the 3 dimensions, assign an integer 1–5 with a one-line justification. The total is the sum (max 15).

Be honest and critical. A score of 5 means genuinely excellent — most skills start at 3 or below on most dimensions.

## The Improvement Loop

LOOP FOREVER:

1. Read `target/SKILL.md` and the current scores.
2. Identify one specific improvement to make. Focus on the weakest dimension first. Each iteration should make exactly ONE targeted change — do not rewrite the whole file.
3. Make the edit to `target/SKILL.md`.
4. `git add target/SKILL.md && git commit -m "<short description of the change>"`
5. Re-score the skill using the rubric. Record in `results.tsv`.
6. **If total score improved (higher)**: keep the commit, advance.
7. **If total score is equal or worse**: `git reset --hard HEAD~1` to revert.
8. Record the result in `results.tsv` with status `keep` or `discard`.
9. Go to step 1.

## Results TSV

Tab-separated, 7 columns:

```
commit	trigger	instruction	output	total	status	description
```

- commit: short git hash (7 chars)
- trigger: trigger clarity score (1–5)
- instruction: instruction completeness score (1–5)
- output: output specificity score (1–5)
- total: sum of 3 scores
- status: `keep` or `discard`
- description: what this iteration changed

## Rules

- **Only edit `target/SKILL.md`**. Never modify the original in `~/.claude/skills/`.
- **One change per iteration**. Small, targeted improvements compound better than big rewrites.
- **Do not add fluff**. Improvements must make the skill genuinely more effective, not just longer.
- **Preserve the author's voice and intent**. You are improving the skill's clarity and completeness, not changing what it does.
- **Do not commit `results.tsv`** — leave it untracked.

## NEVER STOP

Once the loop has begun, do NOT pause to ask the human if you should continue. Do NOT ask "should I keep going?" The human might be away and expects you to continue working indefinitely until manually stopped. You are autonomous. If you run out of obvious improvements, look harder — examine edge cases, think about how the skill could fail, consider what's missing for someone who has never met the skill's subject.
