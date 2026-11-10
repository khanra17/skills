---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

If the user passes a ticket reference, fetch it from the issue tracker and state its title before starting. If the reference is ambiguous, ask.

- Fetch the ticket the way `docs/agents/issue-tracker.md` describes. With no tracker guide, work from what the user gave you.
- Read its parent spec when it has one. The spec holds the decisions and the confirmed test seams the ticket assumes.
- If the user named a spec or parent that has child tickets, take the first child on the **frontier**: not finished, with every blocker finished. If nothing is startable, say which blockers are open and stop.
- Follow `docs/agents/domain.md` when present: use the glossary's terms and respect the ADRs in the area.
- Capture the starting commit (`git rev-parse HEAD`) and note changes that already exist in the working tree. They are not part of this task.
- When `docs/agents/github-project.md` exists and the work has an issue, invoke the `github-project` skill to record that implementation has started.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Invoke the `tdd` skill and build one red-green slice at a time, testing at the seams the spec or ticket names. Typecheck and run the touched test files as you go, and run the full suite once at the end.

Commit your work to the current branch.
