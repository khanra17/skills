# to-tickets

## What it does

`to-tickets` breaks a plan, spec, or conversation into tracer-bullet tickets. Each ticket delivers one narrow, complete path through the system, names the test seams it uses, and declares which other tickets block it.

It shows you the breakdown before publishing. A local tracker gets one Markdown file per ticket. GitHub gets one issue per ticket, attached to the spec as sub-issues, with native blocking links.

## When to reach for it

Type `/to-tickets` when the work is too large for one [implement](./implement.md) session, after [to-spec](./to-spec.md) or from an already settled plan.

Wayfinder's decision tickets are a different thing: those answer planning questions, these build decided behavior.

## Common questions

**What makes a ticket a vertical slice?**

It delivers behavior you can see working, through every layer it needs. A ticket that is only schema work or only UI work is a horizontal slice.

**How large is a ticket?**

Small enough to build in one fresh context window, complete enough to demo. You review the granularity before anything is published.

**How does it handle a rename that touches the whole codebase?**

As expand, migrate, contract: add the new form beside the old, move callers in batches, then delete the old form. Each step is a ticket, and the blocking links keep them in order.

## It's working if

- Every ticket can be demoed or verified by itself.
- A ticket with no blockers can start today, and each blocker is a real prerequisite.
- On GitHub, the spec issue lists the tickets as sub-issues.
