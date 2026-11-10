# writing-for-agents

## What it does

`writing-for-agents` is the reference for documents an agent consumes: skills, `AGENTS.md`, and documents an agent reaches through a pointer.

It covers how to word pointers so the agent loads the right document at the right time, what to keep in the main file and what to move behind a pointer, how to end each step on a checkable completion criterion, how to anchor behavior with a few well-chosen words, and how to prune what the model already does by default.

## When to reach for it

Type `/writing-for-agents`, or let the agent reach for it, when creating or editing a skill, an `AGENTS.md`, or an agent-facing reference. [Setup](../engineering/setup-khanra17-skills.md) and [reflect](./reflect.md) call it when they draft instructions.

For prose a person will read, use [unslop](./unslop.md) or [technical-writing](../engineering/technical-writing.md).

## Common questions

**What is a context pointer?**

A short reference that tells the agent what another document contains and when to load it. A skill's description is one; so is a line in `AGENTS.md` naming a doc. Its wording decides how reliably the target gets read.

**What stays in the main file?**

The steps and rules every path needs. Reference that only some branches use goes behind a pointer.

**When should a skill be model-invoked?**

When the agent has to find it without being told, or another skill has to call it. A skill you only ever type yourself is better user-invoked, where it costs no context.

**Why does it tell me to remove instructions?**

An instruction the model already follows costs attention and changes nothing. A sentence denying a past mistake, or an instruction written in capitals, can make the behavior worse: the first plants the idea, the second gets over-applied.

**What is a router skill?**

A user-invoked map of the other skills, so you have one name to remember. [which-skill](../engineering/which-skill.md) is this library's.

## It's working if

- Deleting any one sentence from the document would change what the agent does.
- Each step says how the agent knows it is finished.
- Each rule is stated in one place.
