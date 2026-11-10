---
name: setup-code-quality-gates
description: "One-time, user-invoked setup of Crapper, Dryer, and Mutator for a target code repository. Use when explicitly asked to install, configure, pin, verify, or update UB Mode quality checks and their CI integration."
disable-model-invocation: true
---

# Setup Code Quality Gates

Configure **one target repository**, not this skills repository. Produce reproducible, opt-in checks and `docs/agents/quality-gates.md` for `code-review`'s optional Quality Gates worker. Do not invoke during ordinary implementation or review. Re-running setup must be idempotent.

## 1. Inspect

Read the project's tests, coverage, task runner, runtime, lockfiles, hooks, CI, steering files, ignore rules, and existing `docs/agents/quality-gates.md`. Detect installed versions. Confirm source language support (Clojure, Java, Go, TypeScript/JavaScript, Rust, Python). Read authoritative documentation for [Crapper](https://github.com/unclebob/crapper), [Dryer](https://github.com/unclebob/dryer), and [Mutator](https://github.com/unclebob/mutator), checking the selected CLI version. Mutator expects Crapper as a sibling `../crapper` directory.

## 2. Propose, then confirm

Present findings, existing tools, missing prerequisites, and a minimal plan before any write or install. Recommend immutable tool revision pins, sibling checkouts (such as `.tools/quality-gates/`), isolated virtual environments, project-specific task-runner commands, and tests/coverage matching the codebase.

Agree on scope, CRAP strictly below 10, Dryer similarity 0.8 rather than default 0.82, mutation risk tiers, default proposal of five minutes local runtime, CI time/worker budgets, optional developer hooks, and merge-blocking policy. Note Crapper's `--threshold 10` flags >10, not >=10; evaluate results separately to meet strict <10.

## 3. Configure

- Pin tool revisions using the project's existing tool manager, Git submodules, or a locked fetch script. Keep Mutator and Crapper siblings. Document how to update pins. Ignore generated virtual environments, `.metrics`, coverage snapshots and mutation workers.
- Create tested project-owned runner commands for changed-code Crapper and Dryer, targeted Mutator and Mutator scan. Verify flags from pinned documentation (such as `--changed`, `--threshold 0.8`, `--scan`, `--max-workers`); use the project's real tests and coverage commands.
- Write `docs/agents/quality-gates.md` with `enabled: true`, pinned revisions, commands, outputs, thresholds, scope, exclusions, risk tiers, budgets, CI policy and owner. This file is the **sole opt-in signal** for the review worker.
- Wire CI to fast incremental checks and optional manual/scheduled mutation jobs as appropriate. Hook only fast checks if requested; no full mutation test in Husky by default.
- Isolate runs that may alter the checkout; do not pass secrets to untrusted pull request code.

## 4. Verify and hand off

Smoke-test every enabled tool and a representative CI-equivalent command. Confirm statuses, stable artifacts, and no tracked-file changes. Reinspect the setup to demonstrate that rerunning will not duplicate configuration or overwrite user edits. Mark failing/missing tools disabled or not ready rather than passing.

Report exact created files, checked commands, test outcomes, and how to run, update, or remove the setup. Do not invoke `code-review` automatically.
