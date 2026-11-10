# triage

## What it does

`triage` evaluates issues and moves them between states. Every evaluated issue gets one category and one state.

- Categories: `bug`, `enhancement`.
- States: `needs-triage` (evaluation unfinished), `needs-info` (waiting on the reporter), `ready-for-implementation` (fully specified), `suspended` (not pursuing; closed as not planned).

For one issue, it reads the full history, searches the codebase for an existing implementation, looks for earlier decisions in closed issues and ADRs, and verifies the claim (for a bug, by reproducing it). Then it recommends a category and state and waits for you. If the request needs fleshing out it grills you, and when the issue is ready it posts an implementation brief.

## When to reach for it

Type `/triage` to list what needs attention, look at one issue, or change an issue's state.

Tickets produced by [to-tickets](./to-tickets.md) are already ready and skip triage.

## Common questions

**What does `ready-for-implementation` mean?**

The request is fully specified. It doesn't assign the work to anyone or schedule it.

**What happens when the feature already exists?**

The issue is closed as completed with a pointer to the existing behavior. That is a different outcome from `suspended`.

**What happens to a rejected request?**

The reason is recorded on the issue, which gets the `suspended` label and closes as not planned. Later requests for the same thing can be linked back to that explanation.

**Can I change a state without the full evaluation?**

Yes. Say "move #42 to ready-for-implementation". The skill confirms what it is about to change, applies it, and offers to write an implementation brief.

**Where do the label names come from?**

`docs/agents/triage-labels.md` maps the roles above to your repository's labels. [Setup](./setup-khanra17-skills.md) writes it.

## It's working if

- Every evaluated open issue carries one category label and one state label.
- A bug marked ready has a recorded reproduction.
- A `needs-info` comment lists what is already established and asks specific questions.
- A ready issue has a brief with acceptance criteria and no file paths.
