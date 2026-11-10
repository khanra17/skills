# github-project

## What it does

`github-project` keeps a GitHub Project's membership, delivery status, and fields current. It adds a delivery view on top of the issue workflow; triage, specs, tickets, and implementation work as before.

The operating rules live in the skill. `docs/agents/github-project.md` holds this project's choices: the Project URL, which issues belong on it, the field mapping, what Done means, and which transitions automation owns.

## When to reach for it

Use it on work large enough that you need to see commitments, active work, and delivery across many issues. Ask it to update or reconcile the board, or let the tracker guide and [implement](./implement.md) call it.

It acts only on a board you opted in to during [setup](./setup-khanra17-skills.md). For small projects, issues alone are enough.

## Common questions

**What board does setup recommend?**

Backlog → Next → In progress → Done, with Awaiting acceptance added when work regularly waits on a client approval or delivery check. A board you already have keeps its conventions unless you agree to change them.

**How is Next different from `ready-for-implementation`?**

Ready means the issue is specified well enough to build. Next means you have chosen it for near-term work. Triage sets the first; only you set the second.

**Does a commit move the issue to Done?**

Only when your definition of Done is met. If Done means deployed or accepted by the client, a commit and passing tests leave the card earlier on the board.

**Where do priority, milestones, and blockers live?**

Each in one place: priority in an organization issue field or a Project field, deliverables in milestones, hierarchy and blocking in native sub-issues and dependencies.

**What happens to cancelled or reopened work?**

An issue closed as not planned follows your archive policy and stays out of delivered totals. A reopened issue goes back to the stage it is really at.

## It's working if

- Each issue appears on the board once, with its PR linked rather than added as a second card.
- Cancelled issues are absent from delivered counts.
- A card reaches Done only when your completion criteria are met.
- After a batch of updates, the skill reports which fields it could not set.
