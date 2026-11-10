# grill-with-docs

## What it does

`grill-with-docs` runs the [grilling](../productivity/grilling.md) interview and keeps the project's durable knowledge current while it does.

When a domain term gets settled, it uses [glossary](./glossary.md) to write it into `GLOSSARY.md`. When an architectural decision is hard to reverse, surprising, and a real trade-off, it uses [adr](./adr.md) to record it.

## When to reach for it

Type `/grill-with-docs` to sharpen a plan or design inside a project.

Use [grill-me](../productivity/grill-me.md) for the same interview with nothing written down. Use [wayfinder](./wayfinder.md) when the effort is too large for one session.

## Common questions

**Where do my answers go?**

Domain terms go to the glossary, and the few decisions that qualify become ADRs. Requirements and ordinary design answers stay in the conversation, which is why the next step is [to-spec](./to-spec.md) in the same session: the conversation is its source.

**Why did no ADR appear?**

Most decisions don't qualify. An ADR is offered only when the choice is hard to reverse, surprising without context, and the result of a real trade-off.

## It's working if

- Questions arrive in numbered rounds, each with a recommended answer.
- A term you settle appears in `GLOSSARY.md` during the interview, not at the end.
- The agent waits for you to confirm shared understanding before it builds anything.
