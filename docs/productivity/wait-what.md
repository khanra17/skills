# wait-what

## What it does

`wait-what` asks the agent to explain its last message again. The new explanation adds the context you were missing and uses ASD-STE100 Simplified Technical English: short sentences and common words.

When the project has a glossary, the explanation uses its terms, following `GLOSSARY-MAP.md` to the right glossary when there are several.

## When to reach for it

Type `/wait-what` right after a message that doesn't make sense, assumes too much, or is hard to follow. It works mid-task, inside any other skill, in or out of a repository.

## Common questions

**Does it restart the task?**

No. It re-explains the previous message and the conversation carries on from where it was.

**What if there is no glossary?**

You still get the plain-English explanation.

## It's working if

- The new explanation opens with the context the first one assumed.
- Sentences are short and say one thing each.
- It means the same as the original message.
