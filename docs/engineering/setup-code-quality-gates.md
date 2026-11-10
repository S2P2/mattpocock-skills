## What it does

`setup-code-quality-gates` is an optional, user-invoked, per-repository setup of [Crapper](https://github.com/unclebob/crapper), [Dryer](https://github.com/unclebob/dryer), and [Mutator](https://github.com/unclebob/mutator). It inspects existing tests/coverage/CI, proposes pinned versions and thresholds, and only then configures project-owned commands and CI.

It creates `docs/agents/quality-gates.md`, an explicit opt-in that lets the review workflow spawn a dedicated Quality Gates subagent.

## When to reach for it

Run it once for a project that wants complexity, duplication, and mutation evidence. Run again when updating tool versions, test coverage commands, or budgets. It must not silently provision tools during normal code review.

## Safety and provenance

Mutation testing follows an S2P2-specific risk/budget policy; no full mutation checks in pre-commit hooks by default. The original quality goals derive from [UB Mode at `3da62bf3fcfd2034de41f30d920d2739e566171f`](https://github.com/unclebob/ub-mode/blob/3da62bf3fcfd2034de41f30d920d2739e566171f/SKILL.md), MIT licensed.
