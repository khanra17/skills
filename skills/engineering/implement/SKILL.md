---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Before editing, capture the starting commit (`git rev-parse HEAD`) and note existing changes.

If the user passes a ticket reference, fetch it from the issue tracker and state its title before starting. If the reference is ambiguous, ask.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, use /code-review in working-tree mode, passing the starting commit, spec/ticket or agreed requirements, and this task's changes—not unrelated existing work. Rerun affected checks after review-driven fixes.

Commit your work to the current branch.
