## What it does

`grill-with-docs` runs the [grilling](../productivity/grilling.md) interview while keeping durable project knowledge current.

As terms become clear, it uses [glossary](./glossary.md) to update `GLOSSARY.md` or the relevant context glossary. When a significant architectural decision passes the ADR eligibility test, it uses [adr](./adr.md) to record it.

## When to reach for it

Type `/grill-with-docs` when you want to sharpen a plan or design inside a project and preserve the domain language or architectural decisions that emerge.

Use [grill-me](../productivity/grill-me.md) when you want the same interview without project documentation. Use [wayfinder](./wayfinder.md) when the effort is too large for one session.

## Common questions

**Does every answer get written to a file?**

No. Domain terms go to the glossary. Significant architectural decisions may become ADRs. Requirements and ordinary design answers remain in the conversation and should flow into [to-spec](./to-spec.md).

**Why did no ADR appear?**

Most decisions do not qualify. An ADR is offered only when the choice is hard to reverse, surprising without context, and based on a real trade-off.

**What if no glossary exists yet?**

It is created lazily when the first term is settled. The setup skill does not create empty glossary files.

**Should I continue into a spec in the same session?**

Yes, when the idea is ready. The full conversation is the primary source for [to-spec](./to-spec.md), so continuing avoids losing the reasoning behind the decisions.

## It's working if

- Questions arrive in dependency-aware rounds with recommendations.
- Resolved domain terms are written immediately rather than collected at the end.
- The glossary stays free of implementation details.
- ADRs remain rare and explain real trade-offs.
- The conversation ends with shared understanding before implementation begins.
