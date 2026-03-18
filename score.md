# Skill Scoring Rubric

Score each dimension 1–5. Total is out of 15.

## 1. Trigger Clarity (1–5)

How well does the skill define **when** it should activate?

| Score | Meaning |
|-------|---------|
| 1 | No trigger phrases or conditions specified |
| 2 | Vague trigger ("use when relevant") with no concrete examples |
| 3 | Some trigger phrases listed but gaps in coverage; ambiguous overlap with other skills |
| 4 | Clear trigger phrases and conditions; most activation scenarios covered |
| 5 | Exhaustive trigger list with positive AND negative examples; zero ambiguity about when to fire vs. not |

## 2. Instruction Completeness (1–5)

How thoroughly does the skill tell the LLM **what to do** once triggered?

| Score | Meaning |
|-------|---------|
| 1 | No actionable instructions; just a description of the topic |
| 2 | High-level direction only ("write in this style") with no structure or steps |
| 3 | Reasonable instructions but missing edge cases, fallback behavior, or key constraints |
| 4 | Detailed step-by-step process with constraints, anti-patterns, and examples |
| 5 | Complete playbook: process, constraints, anti-patterns, examples, edge cases, and validation criteria |

## 3. Output Specificity (1–5)

How precisely does the skill define the **shape and quality** of the output?

| Score | Meaning |
|-------|---------|
| 1 | No description of expected output format or quality |
| 2 | Mentions output type ("a LinkedIn post") but no structure, length, or quality bar |
| 3 | Some structure guidance (sections, length ranges) but no concrete good/bad examples |
| 4 | Clear format, length, structure, and good/bad examples for at least one output type |
| 5 | Every output type has format spec, length range, good/bad examples, and a self-check test |
