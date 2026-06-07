---
name: skill-creator
description: Create, test, evaluate, and iterate on Claude Code skills. Follows a draft → test → evaluate → refine loop. Use when building new skills for Claude Code, writing SKILL.md files, or improving existing skills based on test results.
license: Complete terms in LICENSE.txt
---

# Skill Creator

Creates and improves Claude Code skills through an iterative workflow: draft → test → evaluate → refine → repeat.

## Workflow

### 1. Understand Intent

Before writing anything, clarify:
- What should this skill do? (specific behavior)
- When should it trigger? (user request patterns)
- What should the output look like?
- Are test cases needed?

### 2. Write SKILL.md

```markdown
---
name: my-skill
description: One or two sentences — what this skill does and when it's used.
---

# My Skill

[Clear, imperative instructions for what Claude should do]

## When to use

[Trigger conditions: user request patterns, context signals]

## How to do it

[Step-by-step or rule-based guidance]
```

**SKILL.md rules:**
- Keep under 500 lines
- Use clear, imperative language ("do X", "return Y", "check Z")
- Explain the *why* behind instructions, not just the *what*
- Keep it lean — avoid over-specifying edge cases that haven't happened

### 3. Test

Create 2–3 realistic test prompts that represent actual user requests:

```
Test 1: [typical use case]
Test 2: [edge case]
Test 3: [adjacent case — should this skill apply?]
```

Run each test both with and without the skill active to establish a baseline.

### 4. Evaluate

Use `eval-viewer/generate_review.py` to show skill results alongside baseline:

```bash
python eval-viewer/generate_review.py --skill my-skill --tests tests.json
```

Review:
- Does the skill improve the response?
- Does it trigger in the right cases?
- Does it avoid triggering in the wrong cases?

### 5. Iterate

Based on feedback:
- Fix instructions that are misinterpreted
- Generalize patterns that appeared in multiple test cases
- Add missing trigger cases to the description
- Remove over-specific rules that don't generalize

Repeat test → evaluate → refine until results are satisfactory.

## Principles

- **Explain why**: instructions with reasoning generalize better than bare rules
- **Stay lean**: every line costs context; don't over-specify
- **Generalize from feedback**: if a test case revealed a gap, it probably isn't unique
- **Bundle reusable patterns**: if two rules always apply together, make them one

## Platform Notes

- **Claude.ai**: Skills appear as slash commands in the sidebar
- **Claude Code CLI**: Skills live in `~/.claude/skills/` (user) or `.claude/skills/` (project)
- **claude.ai/code**: Project skills in `.claude/skills/` are loaded from the repo
