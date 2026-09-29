## What it does

`adr` records or revises an architectural decision record. System-wide ADRs live in `docs/adr/`; context-specific ADRs live in that context's `docs/adr/` directory.

It offers an ADR only when the decision is hard to reverse, surprising without context, and the result of a real trade-off. The default format is a short title and one paragraph explaining the context, decision, and reason. Optional status, alternatives, and consequences appear only when useful.

## When to reach for it

Type `/adr`, or let another skill call it when a significant architectural decision becomes clear.

Use it for decisions such as a database choice, communication pattern, ownership boundary, deployment target, or deliberate departure from the obvious design. Do not use it for ordinary implementation details, temporary choices, or facts that are already clear from the code.

For domain words and definitions, use [glossary](./glossary.md). For an interview that can produce both glossary updates and ADRs, use [grill-with-docs](./grill-with-docs.md).

## Common questions

**Does every design decision need an ADR?**

No. All three tests must pass: hard to reverse, surprising without context, and a genuine trade-off.

**How long should an ADR be?**

Usually one paragraph. Add optional sections only when they preserve information a future reader would otherwise lose.

**How are ADRs numbered?**

The skill scans the selected ADR directory, finds the highest number, and increments it. A context-specific ADR sequence is independent from the root sequence.

**Can an ADR be changed later?**

Yes. Revise it, mark it deprecated, or point it at the ADR that supersedes it when that history matters.

## It's working if

- The ADR explains why the decision exists, not only what was chosen.
- A future reader can understand a surprising architectural choice without reopening the original conversation.
- Small or reversible choices do not create ADR noise.
- The record lives beside the architecture it governs.
