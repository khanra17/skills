# grilling

## What it does

`grilling` is the interview method behind `grill-me`, `grill-with-docs`, triage, wayfinder, and architecture reviews.

It treats the subject as a tree of decisions, where each decision opens the ones that depend on it. In each round it asks every question whose prerequisites are settled (the frontier), numbered, each with the agent's recommended answer. Your answers reshape the tree, and the next round asks what they opened up.

## When to reach for it

Type `/grilling`, or let another skill invoke it, when a plan, decision, or idea needs stress-testing.

[grill-me](./grill-me.md) is the same interview under a name that's easier to remember. [grill-with-docs](../engineering/grill-with-docs.md) adds a written glossary and ADRs.

## Common questions

**Why does every question come with a recommendation?**

So you can accept it in a word when you agree, and so the agent contributes judgment as well as questions.

**Who looks up facts?**

The agent. If a decision depends on the state of the repository, a doc, or anything else it can find, it finds it. For a long search it sends a subagent and keeps asking the questions that don't depend on the result.

**Will it decide anything for me?**

No. Facts are the agent's job and decisions are yours, down to the small ones.

**When is it finished?**

When no questions are left and you confirm the understanding is shared. Nothing is built before that.

## It's working if

- No question in a round depends on another question in the same round.
- Each recommendation is specific enough to accept or reject.
- You are never asked for something the agent could have looked up.
