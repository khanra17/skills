## What it does

`implement` builds work described by a spec, ticket, or agreed conversation requirements. Before editing, it records the starting commit and any existing changes so the task can be reviewed without mixing in unrelated work.

It uses [tdd](./tdd.md) where possible at pre-agreed seams, runs focused checks during development, runs the full test suite at the end, then calls [code-review](./code-review.md) in working-tree mode. After review fixes and affected checks, it calls [git-commit](./git-commit.md) to commit to the current branch. For work with an issue and a configured [GitHub Project](./github-project.md), it also reports implementation start and the verified outcome to the board operator.

## When to reach for it

Type `/implement` when the decisions are settled and the work is ready to build.

For a multi-ticket effort, start a fresh session for each ticket. Use [to-spec](./to-spec.md) when the requirements still need to become one durable spec, and [to-tickets](./to-tickets.md) when the work must be split into dependency-aware slices.

## Common questions

**Does it create or switch branches?**

No. It commits to the current branch. Select the correct branch before starting.

**Can it work from the current conversation?**

Yes. Pass the agreed requirements when there is no separate spec or ticket.

**How does review see uncommitted changes?**

The skill passes its starting commit to `code-review` in working-tree mode. That includes relevant tracked and untracked task changes, even before the final commit.

**What happens when unrelated changes already exist?**

They are noted before editing and excluded from the task scope passed to review. The skill must not overwrite or include them accidentally.

**What does it verify beyond the path it changed?**

It checks applicable clients, entry points, adapters, and shared contracts using the project's verification guidance when available. Relevant failure, recovery, and inverse actions count too. The scope follows the feature, not a universal checklist of platforms.

For visible UI changes, it inspects the running result with representative seeded or sanitized data and relevant layouts. Screenshots support appearance checks; recordings help with motion or timing. These complement behavioral tests. Browser/device access follows project constraints, and unavailable checks are reported rather than claimed as passed. Sensitive live data and evidence uploads need authorization.

**Does it close the tracker ticket?**

No. It commits the implementation and, when a Project is configured, updates the delivery stage according to that board's completion criteria. Closing the issue still needs a separate instruction. A commit does not prove deployment or client acceptance.

## It's working if

- The starting commit and existing changes are recorded before edits.
- Tests are written at agreed seams in red-green slices where possible.
- Focused checks run during development and the full suite runs at the end.
- Applicable surfaces and recovery paths are checked; UI evidence uses representative safe data.
- Verification gaps are reported explicitly.
- Review receives the same requirements and task scope used for implementation.
- Review-driven fixes are checked again before the final commit.
- Commits follow the selected convention without including unrelated staging.
- Optional board updates reflect actual progress rather than assuming every commit means Done.
