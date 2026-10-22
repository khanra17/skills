## What it does

`glossary` builds and sharpens the project's domain language. It challenges vague or conflicting terms, tests them against concrete scenarios and the code, then records settled definitions in `GLOSSARY.md`.

Most projects use one root `GLOSSARY.md`. A multi-context project uses a root `GLOSSARY-MAP.md` that points to the relevant context glossaries. Files are created only when the first term is ready to record.

## When to reach for it

Type `/glossary`, or let another skill call it when a domain term is ambiguous, overloaded, or inconsistent with the existing glossary.

Use it when people use one word for several concepts, several words for one concept, or when the code and the spoken model disagree. Use [adr](./adr.md) for architectural decisions and [codebase-design](./codebase-design.md) for module-design vocabulary.

## Common questions

**What belongs in the glossary?**

Project-specific domain concepts. General programming terms, implementation details, specs, and scratch notes do not belong there.

**What happens when no glossary exists?**

Nothing is scaffolded in advance. The skill creates the root `GLOSSARY.md` when the first term is settled.

**How does a multi-context glossary work?**

`GLOSSARY-MAP.md` lists each context, links its glossary, and records relationships between contexts. The skill updates the glossary relevant to the current topic.

**Can the skill disagree with the code?**

It can surface the disagreement. You decide whether the code is wrong, the spoken rule is wrong, or the glossary needs a clearer definition.

## It's working if

- One canonical term replaces competing synonyms.
- Definitions say what a concept is in one or two sentences.
- Edge-case scenarios expose unclear relationships before they reach a spec.
- Tests, tickets, and code use the same domain words.
