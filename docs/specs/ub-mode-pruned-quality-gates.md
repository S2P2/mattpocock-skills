# Specification: Selective UB Mode Integration and Opt-In Code Quality Gates

**Status:** Ready for agent ticket breakdown, subject to confirming the two proposed behavioral test seams.

**Repository:** S2P2/mattpocock-skills (fork-specific).

**Source:** [unclebob/ub-mode at commit 3da62bf3fcfd2034de41f30d920d2739e566171f](https://github.com/unclebob/ub-mode/blob/3da62bf3fcfd2034de41f30d920d2739e566171f/SKILL.md), Robert C. Martin, MIT. Retain necessary license/copyright notices for selected copied passages.

**Supersedes:** [Draft PR #1](https://github.com/S2P2/mattpocock-skills/pull/1), which currently copies and routes the whole source.

## Problem Statement

A draft integration of UB Mode into Matt Pocock's agent skills duplicates existing TDD, domain, review, and workflow instructions and makes multiple agents read an entire source skill. This wastes context and creates competing Git/testing instructions. The source provenance and retained/excluded decisions also need to be tracked for later upstream updates.

The user additionally wants optional measured code-quality checks (Crapper, Dryer, Mutator), with risk-bounded mutation execution and a reproducible one-time setup path for each target project. The current two-axis review has no such optional worker, and ordinary reviews should never install tools.

## Solution

**Phase A: Prune and attribute.** Replace the draft whole-source integration with selected original UB Mode headings and bullets, placed in their existing Matt skill owners. Preserve the wording of retained passages for now. Add Agent Skills metadata and a maintainer change log with the pinned upstream SHA, per-section keep/drop reasons, and an update procedure. Remove the copied original source and full routing index. Existing Matt orchestration remains authoritative.

**Phase B: Optional quality gates.** Add an optional, fresh-context Quality Gates worker to code-review, retaining Standards and Spec as separate independent axes. The worker uses repository-configured commands, runs suitable deterministic checks, and decides whether to run Mutator using an explicit S2P2 risk policy and time budget. Add a user-invoked, idempotent setup skill for target repositories; provision version-pinned commands/CI on approval. Local hooks are optional and lightweight; CI is the repeatable authority.

Deliver the phases as separate, reviewable changes; do not merge draft PR #1 as it stands.

## User Stories

1. As a developer, I want ordinary implementation to avoid loading the whole UB skill so that context remains relevant.
2. As a maintainer, I want one owning skill for each retained principle so that edits do not drift.
3. As a maintainer, I want selected UB headings and bullets left verbatim so that I can compare them with upstream.
4. As a maintainer, I want upstream repository, commit SHA and license recorded in optional metadata so that provenance is machine-readable.
5. As a maintainer, I want one maintenance ledger of included/excluded sections and reasons so that future revisions are cheap to audit.
6. As a maintainer, I want to compare a new upstream commit to the pinned one without loading the full upstream skill at runtime.
7. As a maintainer, I want proper copyright and MIT notices retained for borrowed text.
8. As a domain modeler, I want existing glossary and ADR ownership unchanged.
9. As a module designer, I want original UB guidance on design shape, invalid states, boundaries, typing, idempotency, and concurrent state ownership directly in codebase-design.
10. As an implementer, I want both original Build the Lever bullets, including the rule to build a tool when work is not obvious at a glance, so that I can automate repetitive work after proving a manual unit.
11. As a debugger, I want Attack the Premise to trigger only after shared-premise fixes fail, without introducing ambiguous commands.
12. As a developer, I want test seams, red-green cycles, and structural refactoring timing to remain controlled by Matt's existing skills.
13. As a developer, I want branch, commit, worktree, and integration-branch policy to remain owned by Matt's workflows, never an unconditional push to main.
14. As a reviewer, I want Standards and Spec results left separate so that they do not mask each other.
15. As a reviewer, I want optional quality-gate execution in a fresh-context worker so that it does not compete with subjective reviewers for context.
16. As a reviewer, I want exact commands, versions, scope and measurements reported so that every pass/fail is grounded.
17. As a reviewer, I want the original UB CRAP < 10 target and Dryer similarity >= 0.8 threshold applied to the appropriate changed-code scope when tools support them.
18. As a reviewer, I want mutation testing on high-risk behavior and only conditional mutation on medium-risk behavior so that review cost matches potential impact.
19. As a reviewer, I want a bounded local mutation budget and configurable CI budget so that a review cannot run indefinitely.
20. As a reviewer, I want unavailable, failed, unsupported or unrun checks marked explicitly so that no check falsely passes.
21. As a maintainer, I want the setup workflow to inspect existing tests, coverage, language, CI and hooks before proposing changes.
22. As a maintainer, I want setup to present a concrete plan for approval before provisioning tools.
23. As a maintainer, I want pinned tools and repository-owned commands usable on local machines and CI.
24. As a maintainer, I want setup to be idempotent and preserve existing configuration so that a second run is safe.
25. As a developer, I want pre-commit hooks to stay fast and optional, without mutation testing.
26. As a maintainer, I want CI to supply authoritative reproducible results and permit scheduled/manual deeper mutation runs.
27. As a user, I want the one-time setup skill exposed as a user-invoked skill in supported plugin distributions and the ask-matt router.
28. As a developer, I want disposable prototypes exempt from production quality gates.
29. As a maintainer, I want the two phases independently reviewable and reversible.

## Implementation Decisions

### Ownership, provenance and pruning (Phase A)

- Follow the fork's existing promoted-skill, invocation, plugin manifest, docs synchronization and no-em-dash conventions. This is a customization of a fork, not a change proposed to upstream Matt Pocock's catalog.
- Preserve selected original heading names and selected bullet wording. Maintain a compact decision ledger recording the pinned source SHA, source heading, ownership, retained subset, excluded portions, rationale and instructions for assessing future upstream revisions. The ledger is maintainer-facing only; no ordinary skill loads it.
- Use optional Agent Skills frontmatter metadata string fields on skills directly incorporating borrowed instructions; do not modify name, description or invocation semantics merely for provenance. Retain applicable MIT copyright/permission attribution for copied text.
- Remove the full copied UB document, complete heading-routing index and broad automatic source-loading instructions from the current draft. Do not introduce another UB-named skill.
- Inline selected original UB principles directly in the existing model-invoked codebase-design skill: Redesign From First Principles; nonduplicative Model the Domain (invalid-state invariants); Boundary Discipline; Type System Discipline; Make Operations Idempotent; Separate Before Serializing Shared State. Do not introduce a reliability pointer/file.
- Keep domain-modeling responsible for glossary and domain ADR work. Do not duplicate it.
- Retain both original Build the Lever bullets in implement. Keep its existing TDD, verification, review and Git ownership. No automatic call to codebase-design or a reliability reference.
- Add a narrow, conditional Attack the Premise escalation to diagnosing-bugs after repeated failed fixes based on a shared assumption. Preserve unambiguous original selected wording; flag the source's ambiguous 'Remove the assignment' line as excluded in the ledger.
- Existing implement-spec subagents continue to invoke TDD as before. Do not add full UB loading to implement-spec, tdd, retro, ask-matt, prototype or code-review in Phase A.
- Defer CRAP/Dryer/Mutator execution to Phase B; do not add unconfigured commands to normal implementation.

### Optional measured quality review (Phase B)

- Preserve two existing independent report axes: Standards and Spec. Add an optional third Quality Gates worker that starts with a fresh context window when the target repository has configured checks. It is a tool executor, not a subjective reviewer.
- The review aggregator appends a separate Quality Gates report containing exact tools, revisions, commands, execution scope, duration, results and actionable measurement evidence, with explicit failed/skipped/inconclusive states. Standards and Spec results remain separate and unre-ranked.
- Keep original UB Crapper, Dryer and Mutator headings and selected requirements in a conditional review-owned quality-gate reference. Execution commands come from the target project's checked-in configuration. A check may be a hard gate only if the project has explicitly adopted and configured it.
- Crapper target: CRAP < 10 on the agreed changed-function scope when supported. Dryer: structural duplication candidates at or above similarity 0.8 (configure explicitly rather than silently using another tool default), with human confirmation. Mutator: uncovered behavior, surviving mutants and possible dead code, without claiming success from absent measurements.
- New **S2P2 policy**, not from UB Mode: high-risk mutation triggers include authentication/authorization, money movement, destructive writes, migrations, concurrency/retry logic, changed CRAP >= 10, and regression on a previously escaped bug. Medium risk includes complex branching or broad downstream behavior. Low risk includes docs, formatting and mechanical changes. High-risk changes prefer targeted mutation; medium only when affordable; low skip with rationale.
- Before mutation, verify baseline tests pass, identify changed mutation sites, estimate cost from site count and baseline test duration, and compare to a proposed 5-minute local-review budget. CI budget is separately configurable. Honor worker limits and caching when supported. Defer over-budget or impossible work explicitly.
- Do not run stateful quality tasks concurrently on an unsafe shared checkout. Prefer an isolated worktree or equivalent sandbox for commands that create coverage or mutation artifacts or may alter the checkout.
- No tool installation, version changes, or configuration edits happen implicitly during code-review.

### User-invoked one-time setup (Phase B)

- Introduce a user-invoked setup-code-quality-gates skill distinct from setup-matt-pocock-skills. Honor user-only invocation policy in all supported harnesses; update promoted skill listings, plugin manifests, human docs and router.
- Inspect target language/framework, existing tests/coverage, package manager, scripts, hooks, CI, tool compatibility and permissions before acting.
- Present a proposed tool/version/threshold/scope/risk-budget/CI/local-hooks configuration for user approval. A run with no approval changes nothing.
- Install or provision compatible, pinned Crapper/Dryer/Mutator tools using isolated/reproducible tooling appropriate to the project. Account for Mutator dependencies. Do not assume universal support across languages.
- Provide repository-owned commands for supported checks, with suitable changed-code CI and optional manual/scheduled deeper mutation checks. Optional hooks run quick checks only; no Mutator at pre-commit.
- Validate tools and commands with smoke checks, document operational maintenance in the target project, preserve existing customizations, and remain idempotent on rerun. Unsupported/not-available cases yield documented partial setup, never an invented success.
- Adopt the existing setup skill's explore, propose, confirm, write, verify sequence, without changing its issue tracker/domain responsibilities.

## Testing Decisions

Use externally observable behavior through **two high-level seams**. This is the smallest practical set because review produces a report while setup changes an external target repository.

1. **Published skill invocation and review report seam.** Verify the existing implement → tdd → code-review route and the normal codebase-design invocation, with retained UB prose localized to the owning skills, no runtime full-source reads, and no unapproved test seams. Verify unchanged Standards and Spec report sections alongside an optional independent Quality Gates section. Prior art: existing two-axis code-review outputs, original implement-to-review flow, plugin validation and docs synchronization.
2. **Target repository setup-and-execution seam.** Invoke the opt-in setup against disposable representative target projects; inspect checked-in scripts/hooks/CI configuration and run actual supported commands through the same entrypoints a developer/CI uses. Verify the second setup run is idempotent. Prior art: existing setup-matt-pocock-skills explore/confirm/write process and retro's checks-before-rules convention.

Behavioral scenarios:
- Phase A: every selected passage compares equal to pinned upstream; excluded/duplicate sections are documented; provenance metadata is valid; no UB original file required at runtime; original testing/branch conventions still work.
- Plugin manifest, skill discovery, human docs, routing and formatting validations pass, including the repository's strict plugin validation where available.
- Phase B: no configured tools yields unchanged two-axis review and no implicit installation.
- Configured Crapper/Dryer yields measured changed-scope results and explicit threshold semantics.
- High risk with healthy baseline and affordable estimate triggers targeted Mutator; low risk skips it; exceeded budget defers it.
- Failed baseline, missing tools, unsupported language, crashing tool, incomplete data and permission errors are explicit non-passes.
- Reports cannot mask Standards or Spec; tool work is isolated if it writes artifacts.
- Setup works on a new project and pre-configured project; rerun makes no duplicate changes; approval is required before mutating infrastructure; local hooks stay fast and CI results reproducible.

Tests should assert public invocation behavior, generated project configuration/commands and report semantics, not private helpers or copied prompt wording. Where tools/platforms are unsupported, test status behavior with representative fixtures rather than assuming all tools are universally executable.

**Seam confirmation:** the above are the proposed highest-level seams based on existing routes. Confirm or adjust before implementation; do not silently add new test seams.

## Out of Scope

- Merging the current full-copy draft unchanged or preserving an entire UB runtime source.
- Creating a new UB implementation skill or changing Matt's existing TDD, domain glossary, branch, integration, worktree or two-axis ownership.
- Rewriting the wording of retained UB passages at this stage.
- Automatically provisioning tools during normal implement or review runs.
- Running mutation on every commit, every PR or unsupported environment.
- Treating every Dryer candidate as a certain defect, or enforcing unconfigured gates.
- Refactoring unrelated product code merely to satisfy changed-code metrics.
- Publishing the changes to upstream Matt Pocock's repository.

## Further Notes

- The original UB Mode skill does not define criteria for when Mutator should run; risk levels and budgets herein are new S2P2 decisions.
- The fork's existing issue tracker vocabulary includes the triage role 'ready-for-agent'.
- The spec should be split into at least two reviewable implementation phases: Phase A for pruning, metadata and change log; Phase B for setup and optional quality review.
- The fork's GitHub Issues feature was disabled (GitHub returned HTTP 410 when creating this spec issue). This document is therefore published as a versioned specification for review on a separate branch, not as an Issue.
