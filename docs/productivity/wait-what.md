## What it does

`wait-what` asks the agent to explain its last message again. The new explanation adds the missing context and uses ASD-STE100 Simplified Technical English.

When a project glossary exists, the explanation uses its domain language and follows `GLOSSARY-MAP.md` to the relevant glossary when needed.

## When to reach for it

Type `/wait-what` immediately after an explanation does not make sense, assumes too much context, or uses language that is hard to follow.

It works inside or outside a repository and does not require engineering setup.

## Common questions

**Does it restart the task?**

No. It re-explains the previous message and keeps the current conversation state.

**Does it make the answer less accurate?**

It should keep the same meaning while using shorter sentences, concrete words, and the context needed to understand the point.

**What if there is no glossary?**

It still uses Simplified Technical English. Glossary vocabulary is optional.

## It's working if

- The new explanation starts from the missing context.
- Sentences are short and direct.
- Project terms are used consistently when available.
- The explanation preserves the original meaning without repeating the same confusing wording.
