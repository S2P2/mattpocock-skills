# UB Mode source and routing

The file [SKILL.original.md](SKILL.original.md) is copied **verbatim** from
[unclebob/ub-mode](https://github.com/unclebob/ub-mode/blob/3da62bf3fcfd2034de41f30d920d2739e566171f/SKILL.md).
The adjacent [LICENSE](LICENSE) preserves its MIT attribution.
No headings, bullets, or wording were edited or omitted in that copy.

This document explains **when to read** the preserved source. It is a routing
index, not a replacement or summary of its content.

| Original heading | Workflow stage that reads it |
| --- | --- |
| First Make it Work | implement; implement-spec implementers |
| Laziness Protocol | implement; implement-spec implementers |
| Foundational Thinking | implement; implement-spec implementers |
| TDD | tdd; implement invokes tdd |
| Redesign From First Principles | implement; implement-spec implementers |
| Attack the Premise | implement; diagnosing-bugs |
| Subtract Before You Add | implement; implement-spec implementers |
| Outcome-Oriented Execution | implement; implement-spec implementers |
| Build the Lever | implement; implement-spec implementers |
| Architecture | implement; implement-spec implementers; code-review |
| Model the Domain | implement; implement-spec implementers; code-review |
| Boundary Discipline | implement; implement-spec implementers; code-review |
| Type System Discipline | implement; implement-spec implementers; code-review |
| Make Operations Idempotent | implement; implement-spec implementers; code-review |
| Separate Before Serializing Shared State | implement; implement-spec implementers; code-review |
| Then Make it Right | code-review; implement uses its verifiable-unit principle |
| Fix Root Causes | diagnosing-bugs; code-review |
| Sequence work into verifiable units | implement; implement-spec implementers; code-review |
| Test Behavior, Not Implementation | tdd; code-review |
| Crapper | code-review; retro for CI automation |
| Dryer | code-review; retro for CI automation |
| Mutator | code-review; retro for CI automation |
| Refactoring | code-review |
| Practice | retro, with implementation-phase precedence noted below |
| Keep a Log | retro; caller-owned reporting |
| Guard the Context Window | implement; implement-spec; retro |
| Worktree Cleanup | implement-spec; retro; caller-owned cleanup |
| Commit and Push | retro for commit evidence; caller-owned Git delivery |

## Precedence and safety

The original text is preserved as an *unaltered source*, not an unconditional
override of Matt Pocock's flows. In the event of a conflict:

- `tdd` chooses and confirms public test seams with the user.
- `code-review` keeps its two Standards and Spec axes and repository standards.
- `implement` commits to the current branch, and `implement-spec` owns its
  integration branch, subagent worktrees, and any PR.
- **Do not follow UB Mode's unconditional `Push to the main line at the end`
  instruction** within those workflows.
- Run quality tools only when available and in scope; never invent passing
  scores or claim unrun tests passed.
- `prototype` remains a disposable, no-test exploration workflow and does
  not implicitly adopt this production implementation integration.

Both repositories have MIT licenses; retain the source [LICENSE](LICENSE)
with the preserved text.
