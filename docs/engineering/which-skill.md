# which-skill

## What it does

`which-skill` is the router for this library. You describe where you are, and it names the skill or flow that fits and what comes after it.

Its main route is:

```text
grill-with-docs → optional prototype → to-spec → to-tickets → implement
```

`implement` runs `tdd`, `code-review`, and `git-commit` itself. The router also covers the three on-ramps (triage, diagnosing-bugs, wayfinder), the standalone skills, and how to choose between continuing, clearing, handing off, using a subagent, and compacting at a phase boundary.

## When to reach for it

Type `/which-skill` when you don't remember which skill comes next, or two skills look alike. It recommends; you type the skill it names.

## Common questions

**Where does a new feature start?**

With [grill-with-docs](./grill-with-docs.md) inside a project, or [grill-me](../productivity/grill-me.md) when there is no repo to keep a glossary and ADRs in.

**When do I need a prototype?**

When a design question can't be settled by talking: how a state model behaves when you push it through real cases, or which layout works. See [prototype](./prototype.md).

**When do I need wayfinder instead of grilling?**

When the decisions needed to reach the goal won't fit in one session. A feature you can hold in one conversation doesn't need a map. See [wayfinder](./wayfinder.md).

**What is the smart zone?**

The early part of a context window, where the model still reasons sharply: roughly the first 150k tokens on current frontier models. The router's advice on when to continue and when to compact is built around staying inside it.

**What is a phase boundary?**

The point where one chunk of work ends and the next begins, for example between grilling and implementation. It is the moment to decide whether to continue, clear, hand off, delegate, or compact.

## It's working if

- It names one next skill and gives the reason it fits your situation.
- It sends an effort too big for one session to wayfinder, and settled work straight to to-spec or implement.
- Every skill it names exists in this library. If one doesn't, the router is stale: fix its `SKILL.md`.
