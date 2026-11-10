# adr

## What it does

`adr` records an architectural decision, or revises an existing record. System-wide ADRs live in `docs/adr/`; context-specific ones live in that context's `docs/adr/` directory.

The default ADR is a short title and one paragraph: the context, the decision, and the reason. Status, considered options, and consequences are added only when they preserve something a future reader would otherwise lose.

## When to reach for it

Type `/adr`, or let another skill call it, when a significant architectural decision has just been made: a database choice, a communication pattern, an ownership boundary, a deliberate departure from the obvious design.

For domain words, use [glossary](./glossary.md). For an interview that produces both, use [grill-with-docs](./grill-with-docs.md).

## Common questions

**Does every design decision get an ADR?**

Only one that passes all three tests: hard to reverse, surprising without context, and the result of a real trade-off.

**How are ADRs numbered?**

Sequentially within their directory. A context's sequence is independent of the root sequence.

**How do I change a decision that has an ADR?**

If only the wording or detail is wrong, edit it in place. If the decision itself changed, the skill writes a new ADR and marks the old one as superseded, keeping it for the history.

## It's working if

- Each ADR says why the decision was made, in a paragraph you can read in under a minute.
- A reversed decision has a new ADR, and the old one points to it.
- Small or easily reversed choices produce no ADR.
