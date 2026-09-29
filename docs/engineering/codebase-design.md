## What it does

`codebase-design` supplies the vocabulary and principles for designing deep modules: **module**, **interface**, **depth**, **seam**, **adapter**, **leverage**, and **locality**.

A deep module gives callers a lot of behavior through a small interface. The skill helps place seams, reduce interface size, classify dependencies, and design tests through the same interface callers use. It also covers explicit state models when event ordering affects correctness, and a design-it-twice pattern for comparing several radically different interfaces.

## When to reach for it

Type `/codebase-design`, or let another skill call it when the shape of a module is the question.

Use it when deciding where a seam belongs, whether an abstraction earns its keep, how dependencies should be injected, or how to make code testable without exposing internals. Use [improve-codebase-architecture](./improve-codebase-architecture.md) when you do not yet know which part of the codebase to redesign. Use [glossary](./glossary.md) for domain language.

## Common questions

**What is the deletion test?**

Imagine deleting the module. If its complexity disappears, it was probably a pass-through. If the complexity spreads back across several callers, the module was providing locality and leverage.

**Does a seam require an interface type or a separate package?**

No. A seam is a place where behavior can vary without editing the caller. Its file-system shape depends on the project.

**When is an adapter justified?**

When behavior really varies at the seam. A production adapter plus a test adapter is a common real pair. One adapter with no expected variation is usually unnecessary indirection.

**Does stateful behavior require a state-machine library?**

No. When correctness depends on legal transitions or event ordering, use the smallest explicit representation that fits: a type, table, reducer, or state machine. Keep decisions testable separately from I/O, and test relevant sequences through the agreed interface. Ordinary CRUD does not need a new modeling phase or library by default.

**What does design it twice do?**

It asks parallel subagents for three or more contrasting interfaces, then compares depth, locality, seam placement, dependency strategy, and trade-offs. The user sees the options and a recommendation.

## It's working if

- The interface hides more complexity than it exposes.
- Callers and tests use the same seam.
- Internal test seams stay private to the implementation.
- A proposed adapter corresponds to real variation.
- Design discussions use the shared vocabulary consistently.
- Stateful behavior has explicit rules, with meaningful sequences tested rather than trusting the model alone.
