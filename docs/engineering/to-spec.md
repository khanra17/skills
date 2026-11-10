# to-spec

## What it does

`to-spec` turns the current conversation into a spec and publishes it to the issue tracker, labelled `ready-for-implementation`.

It does not interview you again. It synthesizes what has been settled, checks the repository, asks you one thing (whether the proposed test seams are right), and writes the spec: problem, solution, user stories, implementation decisions, testing decisions, and what is out of scope.

## When to reach for it

Type `/to-spec` after [grill-with-docs](./grill-with-docs.md), a cleared [wayfinder](./wayfinder.md) map, or any conversation that has settled the requirements. Run it in the same session as that conversation, which is its source.

Use [to-tickets](./to-tickets.md) next when the build needs several sessions. For a change that fits in the current session, go to [implement](./implement.md).

## Common questions

**How many user stories will it write?**

One for each actor and need the conversation settled, including the edge and failure cases you discussed. It does not pad the list to look thorough.

**Why does it ask about test seams?**

The seams you confirm are written into the spec and copied into each ticket. `implement` and `tdd` then test at those seams in later sessions without asking again.

**Why are there no file paths in the spec?**

Paths and snippets go stale before the work is built. The exception is a snippet from a prototype that states a decision (a state machine, a schema, a type shape) more precisely than prose.

## It's working if

- The published spec names its test seams under Testing Decisions.
- Every user story traces to something you discussed.
- The issue carries the `ready-for-implementation` label.
