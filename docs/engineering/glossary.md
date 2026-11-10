# glossary

## What it does

`glossary` builds and sharpens the project's domain language. It challenges vague or conflicting terms, tests them against concrete scenarios and against the code, and writes each settled definition into `GLOSSARY.md` as it is agreed.

Most projects have one `GLOSSARY.md` at the root. A project with several contexts has a root `GLOSSARY-MAP.md` that points to one glossary per context.

## When to reach for it

Type `/glossary`, or let another skill call it, when a domain term is ambiguous, overloaded, or at odds with the existing glossary: one word doing several jobs, several words for one concept, or the code and the spoken model disagreeing.

Use [adr](./adr.md) for architectural decisions and [codebase-design](./codebase-design.md) for module-design vocabulary.

## Common questions

**What belongs in the glossary?**

Concepts specific to this project's domain, each defined in a sentence or two, with the synonyms to avoid. General programming terms and implementation details stay out.

**What if the code disagrees with what I say?**

The skill points out the contradiction. You decide whether the code is wrong, the stated rule is wrong, or the definition needs sharpening.

## It's working if

- Each concept has one canonical term, with its competing synonyms listed under "Avoid".
- New tickets, tests, and code use the glossary's words.
- No entry describes how something is implemented.
