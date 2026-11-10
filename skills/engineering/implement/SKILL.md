---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

If the user passes a ticket reference, fetch it from the issue tracker and state its title before starting. If the reference is ambiguous, ask.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, call the Skill tool with "code-review" to review the work.

Commit your work to the current branch.

## UB Mode implementation principles

Read [the original UB Mode text](../../../references/ub-mode/SKILL.original.md) before coding. Apply **First Make it Work** in full, including **Laziness Protocol**, **Foundational Thinking**, **Redesign From First Principles**, **Attack the Premise**, **Subtract Before You Add**, **Outcome-Oriented Execution**, **Build the Lever**, and every subsection of **Architecture**.

For **TDD**, the original principles remain available verbatim there, but the `tdd` skill owns seam approval and the red-green loop. Use the original **Sequence work into verifiable units** while making changes, and the original **Guard the Context Window** where context needs to be handed off.

The root UB Mode **Commit and Push** section is source text, not a delivery override. This skill still commits to the current branch, never unconditionally to main. The same precedence applies to the original **Worktree Cleanup** and **Keep a Log** sections: the calling workflow owns worktree lifecycle and reporting.
