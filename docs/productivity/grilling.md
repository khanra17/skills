## What it does

`grilling` is the reusable interview method behind `grill-me`, `grill-with-docs`, triage, wayfinder, and architecture discussions.

It models the subject as a decision tree. In each round, it asks every question on the current frontier: decisions whose prerequisites are already settled. Each numbered question includes the agent's recommended answer. Your answers reshape the tree before the next round.

## When to reach for it

Type `/grilling`, or let another skill invoke it when a plan, decision, or idea needs stress-testing.

Use [grill-me](./grill-me.md) for the same interview without project documentation. Use [grill-with-docs](../engineering/grill-with-docs.md) when resolved domain language and architectural decisions should be written down.

## Common questions

**What is the frontier?**

Every question that can be answered now without guessing the answer to another open question. Dependent questions wait for later rounds.

**Why does every question include a recommendation?**

The agent should contribute judgment, not only ask for instructions. You can accept, reject, or modify the recommendation.

**Who finds technical facts?**

The agent does. If a decision depends on repository state, documentation, or another discoverable fact, it uses a subagent to investigate rather than asking you to do the lookup.

**Can the agent answer decisions for me?**

No. Facts are the agent's job; decisions are yours. A human-in-the-loop branch must wait for your answer.

**When is the interview finished?**

When the frontier is empty and you confirm that the shared understanding is complete. The skill does not act on the result before that confirmation.

## It's working if

- Questions are numbered and grouped into dependency-aware rounds.
- No question depends on another unanswered question in the same round.
- Recommendations are clear enough to accept or challenge.
- Investigations do not block unrelated frontier questions.
- The agent waits for confirmation before acting on the result.
