# wayfinder

## What it does

`wayfinder` plans an effort too large for one session. It creates a map issue that holds the destination, standing notes, a one-line index of decisions made, the questions not yet sharp enough to ticket, and what has been ruled out of scope. Child tickets each resolve one decision, one session at a time, until the route to the destination is clear.

Wayfinder plans; it does not build. When the map clears, the result goes into [to-spec](./to-spec.md), then [to-tickets](./to-tickets.md) and [implement](./implement.md).

## When to reach for it

Type `/wayfinder` with a loose idea to chart a new map, or with a map's URL to resolve its next ticket. It suits a greenfield project or a large feature where you know where you want to end up but can't yet see how to get there.

Use [grill-with-docs](./grill-with-docs.md) when the idea can be settled in one conversation, and go straight to [to-spec](./to-spec.md) when the decisions are already made.

## Common questions

**What kinds of tickets are there?**

- `grilling`: a decision made in conversation with you. The default.
- `prototype`: something concrete to react to before you can decide.
- `research`: outside facts, gathered by a background agent.
- `task`: manual work that has to happen before a later decision can be made.

**What is the frontier?**

The child tickets that are open, unblocked, and unclaimed: what can be started now. Your tracker shows the same thing through its native blocking links.

**What goes under "Not yet specified"?**

In-scope questions you can see coming but can't yet state precisely. When an earlier answer makes one precise, it becomes a ticket and leaves that section.

**Can several tickets run at once?**

Yes, in separate sessions. A session claims its ticket by assigning it before doing any work, so two sessions never take the same one. Each session resolves one ticket; research tickets are the exception and run in parallel.

## It's working if

- The map states its destination in a line or two.
- Each closed ticket has its answer in a comment and a one-line entry in the map's index.
- No ticket describes a slice of the build.
- When no open tickets remain, you can write the spec without further questions.
