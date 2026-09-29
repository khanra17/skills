## What it does

`triage` moves issues through two category roles and four state roles.

Categories:

- `bug`
- `enhancement`

States:

- `needs-triage`
- `needs-info`
- `ready-for-implementation`
- `suspended`

It gathers the full issue history, checks the codebase for an existing implementation and prior rejection, verifies the claim, grills unclear requests, and writes an implementation brief when the issue is ready.

## When to reach for it

Type `/triage` to inspect one issue, change an issue's state, or list work needing attention.

This workflow handles issues only. Tickets produced by [to-tickets](./to-tickets.md) are already ready and should not be triaged again.

## Common questions

**What does `ready-for-implementation` mean?**

The request is fully specified and needs no more triage. It does not assign the work or approve a merge.

**What happens when the feature already exists?**

The skill removes the triage-state label, points to the existing behavior, and closes the issue as completed. It does not mark the issue `suspended` or add it to the rejection knowledge base.

**What happens to rejected enhancements?**

A durable explanation is written or appended under `.out-of-scope/`, linked from the issue, and the issue closes as `suspended`. Rejected bugs receive an explanation but do not enter that knowledge base.

**Can I force a state change without a full interview?**

Yes. A maintainer can request a quick state override. The skill confirms the resulting label, comment, or closure, then applies it. It offers an implementation brief when moving directly to ready.

**Where do the actual label names come from?**

`docs/agents/triage-labels.md` maps the canonical roles to the repository's labels. Run [setup-khanra17-skills](./setup-khanra17-skills.md) if it is missing.

## It's working if

- Every evaluated open issue has one category and one state.
- Verification happens before a request becomes ready.
- Missing information produces specific questions without discarding what was already learned.
- Ready issues contain durable, behavioral implementation briefs.
- Already implemented work and rejected work follow different closure paths.
