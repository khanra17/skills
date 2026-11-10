---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

## 1. Load the work

- Fetch the ticket the way `docs/agents/issue-tracker.md` describes. With no tracker guide, work from what the user gave you.
- Read its parent spec when it has one. The spec holds the decisions and the confirmed test seams the ticket assumes.
- If the user named a spec or parent that has child tickets, take the first child on the **frontier**: not finished, with every blocker finished. If nothing is startable, say which blockers are open and stop.
- Follow `docs/agents/domain.md` when present: use the glossary's terms and respect the ADRs in the area.
- Capture the starting commit (`git rev-parse HEAD`) and note changes that already exist in the working tree. They are not part of this task.
- When `docs/agents/github-project.md` exists and the work has an issue, invoke the `github-project` skill to record that implementation has started.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Invoke the `tdd` skill and build one red-green slice at a time, testing at the seams the spec or ticket names. Typecheck and run the touched test files as you go, and run the full suite once at the end.

If the ticket turns out to be wrong, or depends on a decision nobody made, stop and ask. Scope is the user's to change.

## 3. Verify

Run the feature the way its users reach it, on every surface this change touches: each client, entry point, or adapter that exposes the behaviour. The project's verification guide, when `AGENTS.md` points to one, lists the surfaces and how to run them. One entry point passing says nothing about the others. Where the feature has them, exercise the failure path, the recovery from it, and the inverse action (undo, cancel, delete).

For visible UI changes, look at the running result with representative seeded or sanitized data, at the layouts the project supports. Take screenshots for appearance and recordings where motion or timing matters. Follow the project's browser and device access constraints. Live sensitive data and uploading evidence anywhere both need the user's authorization.

List every surface you could not check. An unchecked surface is reported as unchecked.

## 4. Review and fix

Invoke the `code-review` skill in working-tree mode, passing the starting commit, the spec or ticket, and this task's scope (so pre-existing changes stay out).

Fix every hard finding: a documented-standard violation, a spec gap, a bug. For judgement calls, apply the ones that are cheap and clearly an improvement, and list the rest for the user. This is also where the refactoring that `tdd` defers happens. Rerun the affected checks after the fixes.

## 5. Commit and finish

Invoke the `git-commit` skill to commit the work to the current branch. Finish the ticket the way the tracker guide describes: on GitHub the commit carries the closing footer, on a local tracker the ticket file is marked done in the same commit.

When the work has an issue and a configured Project, invoke the `github-project` skill with the issue and the verified outcome. Its completion criteria decide the board stage.

End with a report: what was built, what was verified and how, what was not verified, review findings left for the user, and the state the ticket is now in.
