## What it does

`wayfinder` plans an effort too large for one session. It creates one map issue with a destination, standing notes, linked decisions, unresolved fog, and out-of-scope work. Child decision tickets move the effort forward until the route to the destination is clear.

Wayfinder plans by default. Its tickets resolve questions rather than deliver slices of the final build. When the map clears, the result normally flows into [to-spec](./to-spec.md), [to-tickets](./to-tickets.md), and [implement](./implement.md).

## When to reach for it

Type `/wayfinder` for a greenfield project or large feature whose destination is visible but whose route cannot fit in one session.

Use [grill-with-docs](./grill-with-docs.md) when the idea can be settled in one conversation. Skip directly to [to-spec](./to-spec.md) when the decisions are already made.

## Common questions

**What is the frontier?**

The open, unblocked, and unclaimed child tickets. It is the work that can safely start now.

**What kinds of tickets exist?**

- `grilling`: a live decision with the user.
- `prototype`: a concrete artifact needed before the user can decide.
- `research`: outside facts gathered by a background agent.
- `task`: manual work required before a later decision can be made.

**When does research start?**

After tickets and blocking edges exist, wayfinder starts only newly created research tickets that are on the frontier. It claims each ticket before dispatch, so blocked or already claimed research waits.

**What belongs under Not yet specified?**

In-scope questions that are visible but cannot yet be stated precisely. Once an earlier answer makes one precise, it graduates into a ticket and leaves the fog section.

**Can several tickets run at once?**

Yes, when they are independently on the frontier. Claims prevent two sessions from taking the same ticket. A normal session resolves no more than one ticket, except for parallel research dispatch.

**Where do maps and dependencies live?**

The configured tracker guide defines the concrete commands or local files. Run [setup-khanra17-skills](./setup-khanra17-skills.md) first.

## It's working if

- The destination is clear before tickets are created.
- Tickets hold decisions or prerequisites, not implementation slices.
- Blocked research waits for the decision it depends on.
- The map links to detailed answers instead of duplicating them.
- The final map hands a coherent set of decisions to the normal build flow.
