# grill-me

## What it does

`grill-me` starts a relentless interview about a plan, design, or idea. It runs [grilling](./grilling.md), which asks rounds of questions in dependency order and gives a recommended answer with each one.

It writes nothing down: no glossary, no ADRs.

## When to reach for it

Type `/grill-me` to sharpen an idea by talking it through. It works anywhere, in a repository or outside one.

Use [grill-with-docs](../engineering/grill-with-docs.md) when the terms and architectural decisions you settle should be recorded in the project.

## Common questions

**Why does it ask several questions at once?**

Each round holds every question that can be answered now. A question that depends on an answer you haven't given yet waits for a later round.

**What happens when the interview ends?**

It stops when no questions are left and you confirm you understand each other. What to do with the result (a spec, an implementation, a document) is your call.

**What if a question can't be answered by talking?**

Use [prototype](../engineering/prototype.md) to get something concrete to react to, then bring the answer back.

## It's working if

- Questions come in numbered rounds, each with a recommendation.
- Facts the agent could look up are looked up, not asked of you.
- Later rounds follow from your earlier answers.
