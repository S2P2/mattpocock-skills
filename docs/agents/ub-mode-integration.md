# UB Mode integration and upstream update log

## Attribution

- Source: [unclebob/ub-mode](https://github.com/unclebob/ub-mode), [`SKILL.md` at commit `3da62bf3fcfd2034de41f30d920d2739e566171f`](https://github.com/unclebob/ub-mode/blob/3da62bf3fcfd2034de41f30d920d2739e566171f/SKILL.md)
- Copyright: Robert C. Martin; MIT licensed. The [original license notice](../../references/ub-mode/LICENSE) is retained for the copied passages.
- Modified skills have `metadata.ub_mode_source`, `metadata.ub_mode_commit`, `metadata.ub_mode_license`, and `metadata.ub_mode_change_log` in YAML frontmatter.
- This ledger is for maintainers only, not a runtime dependency. The full upstream skill is not vendored.

## Retained, omitted, and relocated sections

| Original UB heading | Decision | Location and reason |
| --- | --- | --- |
| Laziness Protocol | Omit | Already in minimal-change rules |
| Foundational Thinking | Omit | Design and concurrency handled in targeted rules |
| TDD | Omit | Matt's `tdd` owns seams and red/green |
| Redesign From First Principles | Retain both bullets | `codebase-design/SKILL.md` |
| Attack the Premise | Retain first bullet | `diagnosing-bugs/SKILL.md`, only after two failed fixes sharing a premise; omit ambiguous assignment instruction |
| Subtract Before You Add | Omit | Existing deletion test and speculative generality |
| Outcome-Oriented Execution | Omit | Existing small, verifiable slices |
| Build the Lever | Retain both bullets | `implement/SKILL.md` |
| Model the Domain | Retain illegal-states bullet | `codebase-design/SKILL.md`; existing glossary ownership unchanged |
| Boundary Discipline | Retain validation pair | `codebase-design/SKILL.md`; pure-logic instruction overlaps testability |
| Type System Discipline | Retain parse-once and compiler bullets | `codebase-design/SKILL.md`; illegal-value rule overlaps domain modeling |
| Make Operations Idempotent | Retain original bullet | `codebase-design/SKILL.md` |
| Separate Before Serializing Shared State | Retain both bullets | `codebase-design/SKILL.md` |
| Fix Root Causes | Omit | `diagnosing-bugs` already provides reproduction |
| Sequence work into verifiable units | Omit | Existing tracer-bullet TDD |
| Test Behavior, Not Implementation | Omit | `tdd` already owns behavior seams |
| Crapper | Retain all bullets | `code-review/QUALITY-GATES.md`; tool evidence |
| Dryer | Retain original bullet | `code-review/QUALITY-GATES.md`; tool evidence |
| Mutator | Retain all bullets | `code-review/QUALITY-GATES.md`; risk-based tool evidence |
| Refactoring | Omit | Existing review design |
| Keep a Log | Omit | Existing reporting |
| Guard the Context Window | Omit | Existing context management |
| Worktree Cleanup | Omit | `implement-spec` already owns it |
| Commit and Push | Omit | Conflicts with current/integration branch policy |

Organizational parent headings are not individually imported.

## S2P2-only rules (not from UB Mode)

- Optional Quality Gates tool-execution subagent, separate from Standards and Spec axes.
- Repository opt-in using `docs/agents/quality-gates.md`, configured through a one-time user-invoked setup skill.
- Mutation testing selection by risk tier and estimated time, with a proposed five-minute local budget.
- Strict CRAP <10 is not implemented by `--threshold 10` alone (which fails only for >10); set Dryer 0.8 explicitly (its CLI defaults to 0.82).
- CI/project commands own enforcement; reviews never install missing tools.

## Update procedure

1. Compare upstream `3da62bf3fcfd2034de41f30d920d2739e566171f` against a newer commit using `git diff 3da62bf3fcfd2034de41f30d920d2739e566171f..<new-commit> -- SKILL.md` in a checkout of the upstream repository.
2. Use the ledger to locate retained headings and destination skills; update verbatim excerpts as needed. Reconsider omissions only if ownership changes.
3. Separately check the Crapper, Dryer, and Mutator repos and their pinned versions for changes in flags, dependencies and thresholds.
4. Update the modified skills' `metadata.ub_mode_commit`, upstream link, license attribution if needed, and the change history.
5. Validate YAML, all linked references, retained passages vs source, and that no runtime skill reads the whole upstream source.

## Change history

- 2026-11-10: Selective integration from `3da62bf3fcfd2034de41f30d920d2739e566171f`; replace full-source routing with inline design, implementation and diagnostic principles plus optional quality tooling and opt-in setup.
