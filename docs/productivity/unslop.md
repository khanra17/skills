## What it does

`unslop` guides human-facing writing automatically: responses, explanations, documentation, and issue or PR descriptions. It removes filler, vague claims, unnecessary jargon, repeated framing, and formatting that gets in the way.

It also edits existing drafts while preserving meaning, voice, specific facts, and genuine uncertainty. Good sentences stay as they are.

## When to reach for it

The agent applies it when writing for you. You can still type `/unslop` with a draft, point it at a file, or request a rewrite of a previous response.

For example, "This tool serves as a centralized location for storing your notes" can become "This tool stores your notes." The edit makes the same claim more directly. It must not add benefits the original never described.

Use [wait-what](./wait-what.md) when you need the previous answer explained again with missing context. Use [i-have-adhd](./i-have-adhd.md) when you want focused task guidance for the rest of the session.

## Common questions

**Do I have to ask every time?**

No. It is model-invoked, and [technical-writing](../engineering/technical-writing.md) also calls it. Project setup adds a short writing pointer to generated agent instructions. An explicit `/unslop` request remains useful when you want an existing piece rewritten.

**Will it remove my personality?**

It should keep your humor, opinions, personal asides, and natural rhythm. The goal is the smallest useful edit, not making everything sound like the same professional writer.

**Does it ban particular words?**

No. It replaces a word when a clearer one fits the meaning. A defined technical term stays even if that word is often used as filler elsewhere.

**Will it make uncertain claims sound more confident?**

No. "This may cause the failure" must not become "This causes the failure" without evidence. It also preserves numbers and quotations rather than inventing stronger support.

**What does it return?**

The response, draft, or revised text itself. If you asked it to edit a file, it edits the file and identifies it briefly. It explains major restructuring or unresolved factual questions when needed, without a mandatory change report.

## It's working if

- The result is easier to read but still sounds like the writer.
- Concrete facts and meaningful qualifications survive the edit.
- No unsupported claim or statistic appears.
- Defined terms are used consistently instead of replaced with loose synonyms.
- Responses need less effort to read without requiring repeated requests for a cleanup.
