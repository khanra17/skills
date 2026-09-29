## What it does

`grill-me` starts a relentless interview about a plan, design, or idea. It delegates to [grilling](./grilling.md), which asks dependency-aware rounds of questions and gives a recommended answer for each.

It is stateless: it does not update a project glossary or create ADRs.

## When to reach for it

Type `/grill-me` when you want to sharpen an idea through conversation without writing project documentation.

You can use it inside or outside a repository. Use [grill-with-docs](../engineering/grill-with-docs.md) when you want resolved terminology and architectural decisions recorded in the project.

## Common questions

**Can I use it inside a repository?**

Yes. The difference is documentation, not location. Choose it when you want the interview without glossary or ADR updates.

**Why does it ask several questions in one round?**

A round contains the whole current frontier: questions whose prerequisites are already settled. Questions that depend on an unanswered choice wait for a later round.

**Does it build the plan after the interview?**

No. It stops when the decision tree is complete and you confirm shared understanding. You decide whether to continue into a spec, implementation, or another artifact.

**What if a question cannot be answered by talking?**

Use [prototype](../engineering/prototype.md) for behavior or UI that needs something concrete to react to, then bring the answer back.

## It's working if

- Questions come in rounds rather than one long dump.
- Each question includes a recommendation.
- Facts are researched instead of being pushed back to you.
- Later questions reflect your earlier answers.
- The interview stops for your confirmation before any implementation begins.
