# UB Mode quality gates

Source: [unclebob/ub-mode, commit `3da62bf3fcfd2034de41f30d920d2739e566171f`](https://github.com/unclebob/ub-mode/blob/3da62bf3fcfd2034de41f30d920d2739e566171f/SKILL.md); MIT license. Original heading titles and bullet wording are retained below.

## Crapper

* Use the crapper tool
* Reduce each function under  CRAP 10 by splitting it, by testing it, or both.
* Consider whether case statements are worth reducing.

## Dryer

* Use the dryer tool to eliminate duplication that rank 0.8 or above.

## Mutator

* Use the mutator tool
* Cover the uncovered.
* Kill the survivors.
* Delete dead code.

## S2P2 execution policy (not from UB Mode)

This reference is loaded **only by the optional Quality Gates worker** when the target repo enables gates through `docs/agents/quality-gates.md`. The original instructions above express quality goals. This policy governs execution and cost.

1. Read the target repo's configured commands, pinned tool versions, scopes, thresholds, and test/coverage prerequisites. Never install tools during review, invent commands, or treat missing configuration as consent.
2. Run changed-code Crapper and Dryer when configured and supported. Crapper's strict **CRAP < 10** target is not enforced by its `--threshold 10` flag alone (that flags >10); inspect measured values. Explicitly set Dryer to **0.8** (upstream defaults to 0.82). Duplicates are candidates for judgement, not automatic unrelated refactors.
3. Mutator is targeted and risk-based, **not mandatory on every diff**. HIGH risk: authorization/authentication, payments, destructive persistence, data/schema migrations, concurrent shared state, retry/idempotency code, changed function with CRAP >=10, or a regression missed by tests. MEDIUM: complex branching or changed public behavior with many dependents. LOW: docs, formatting, mechanical renames, simple well-tested code. HIGH proposes a targeted run; MEDIUM runs only within budget; LOW skips.
4. Confirm baseline tests pass. Use Mutator's `--scan` on selected changed files, estimate expense from baseline duration, mutation sites, worker cap, and cache. Compare with target repo budget (suggested default: five minutes local; CI may be longer). If over budget or indeterminate, record `not run: estimated cost`, and recommend manual/CI execution. Honor configured `--max-workers`.
5. Scope checks to changed code and approved behavior seams. Do not silently expand the ticket or write tests at unapproved seams. Isolate tools/tests that alter checkouts and do not expose secrets to untrusted code.
6. Report each gate as `pass`, `fail`, or `not run`, including command, scope, measured outcome, runtime, evidence artifact, and skip reason. Survivors or uncovered sites are evidence, not authorization to modify code. CI and repo policy own merge-blocking enforcement.

Configured commands and artifacts belong to the target repo, not universal tool paths in this skill.
