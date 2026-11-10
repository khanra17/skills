# unslop

## What it does

`unslop` is guidance for plain, natural prose written for people: responses, explanations, documentation, and issue or PR descriptions. It cuts filler, vague claims, needless jargon, repeated framing, and formatting that gets in the way.

It also edits existing drafts while keeping the meaning, the voice, the specific facts, and any real uncertainty. Good sentences are left alone.

## When to reach for it

Type `/unslop` with a draft, point it at a file, or ask for a previous response to be rewritten.

For example, "This tool serves as a centralized location for storing your notes" becomes "This tool stores your notes." The edit makes the same claim more directly and adds no benefit the original didn't state.

Use [wait-what](./wait-what.md) when you need the previous answer explained again with the context you were missing.

## Common questions

**Does the agent apply it without being asked?**

Sometimes. It is model-invoked, so the agent loads it when it judges a task to be mainly writing, and [technical-writing](../engineering/technical-writing.md) calls it. It does not run before every reply. To have its rules in force all the time, copy the "Write plainly" list from the [skill](../../skills/productivity/unslop/SKILL.md) into your global agent instructions.

**Will it remove my personality?**

It keeps your humor, opinions, personal asides, and rhythm. The goal is the smallest useful edit.

**Does it ban particular words?**

It replaces a word when a clearer one carries the same meaning. A defined technical term stays, even if the same word is filler elsewhere.

**Will it make uncertain claims sound more confident?**

No. "This may cause the failure" stays "may". Numbers and quotations are kept as they are.

## It's working if

- The edited text makes the same claims as the original, in fewer words.
- It still sounds like the person who wrote it.
- No statistic, example, or benefit appears that the original didn't contain.
