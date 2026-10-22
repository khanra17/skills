---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Before editing, capture the starting commit (`git rev-parse HEAD`) and note existing changes.

When `docs/agents/github-project.md` exists and this work has an issue, call the Skill tool with "github-project" to reflect that implementation has started.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Before calling the behavior complete, check the applicable clients, entry points, adapters, and shared contracts using the project's verification guidance when provided. Exercise relevant failure, recovery, and inverse actions; testing one entry point need not verify the whole feature.

For visible UI changes, inspect the running result with representative seeded or sanitized data and relevant layouts. Use screenshots for appearance and recordings when motion or timing matters; these complement behavioral tests. Follow the project's browser/device access constraints, and report unverified surfaces or blocked checks rather than claiming coverage. Do not use live sensitive data or upload evidence without authorization.

Once done, use /code-review in working-tree mode, passing the starting commit, spec/ticket or agreed requirements, and this task's changes—not unrelated existing work. Rerun affected checks after review-driven fixes.

Call the Skill tool with "git-commit" to commit your work to the current branch.

When this work has an issue and a configured Project, call the Skill tool with "github-project", passing the issue and verified outcome. Let its completion criteria determine the board stage; a commit alone need not mean Done.
