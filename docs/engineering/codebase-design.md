# codebase-design

## What it does

`codebase-design` supplies the vocabulary and principles for designing deep modules: **module**, **interface**, **depth**, **seam**, **adapter**, **leverage**, and **locality**.

A deep module gives callers a lot of behavior through a small interface. The skill helps decide where a seam belongs, shrink an interface, classify dependencies, and test through the same interface callers use. It also covers explicit state models for code whose correctness depends on event ordering, and a design-it-twice pattern that has parallel subagents propose contrasting interfaces.

## When to reach for it

Type `/codebase-design`, or let another skill call it, when the shape of a module is the question: where a seam goes, whether an abstraction earns its keep, how to make code testable without exposing internals.

Use [improve-codebase-architecture](./improve-codebase-architecture.md) when you don't yet know which part of the codebase to redesign. Use [glossary](./glossary.md) for domain language.

## Common questions

**What is the deletion test?**

Imagine deleting the module. If its complexity disappears, it was a pass-through. If the complexity reappears in every caller, the module was earning its keep.

**When is an adapter justified?**

When behavior really varies at the seam. A production adapter plus a test adapter is the usual real pair. A seam with one adapter and no expected variation is indirection.

**What does it do for stateful code?**

It has the legal states, transitions, and invariants written down in the smallest form that expresses them (a type, a table, a reducer, a state machine), keeps those decisions testable apart from I/O, and has event sequences tested through the agreed interface.

**What does design it twice produce?**

Three or more contrasting interfaces for the same module, each from its own subagent, followed by a comparison and a recommendation.

## It's working if

- Design discussion uses the seven terms and not "service", "component", or "boundary".
- Callers and tests go through the same interface.
- A proposed seam has two real adapters behind it.
