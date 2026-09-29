## What it does

`writing-for-agents` is the reference for documents an agent consumes: skills, `AGENTS.md`, and documents reached through pointers.

It explains context pointers, context and cognitive load, progressive disclosure, completion criteria, leading words, pruning, skill invocation, and router skills. The goal is predictable behavior from a concise document, not repeated explanation or defensive prompting.

## When to reach for it

Type `/writing-for-agents`, or let the agent reach for it when creating or editing a skill, `AGENTS.md`, or an agent-facing reference.

For ordinary human prose, use a writing or editing workflow instead. This skill is about instructions and references that control agent behavior.

## Common questions

**What is a context pointer?**

A short reference that tells the agent what another document contains and when to load it. Its wording determines whether the target is reached reliably.

**What should stay in the main file?**

Steps and rules every path needs. Branch-specific reference belongs behind a clear pointer so the main process remains visible.

**When should a skill be model-invoked?**

When the agent must discover it automatically or another skill must invoke it. A skill used only by explicit human choice should be user-invoked to avoid permanent context load.

**Why are completion criteria important?**

They tell the agent when a step is genuinely done. A vague criterion invites the agent to move on early, especially when later steps are already visible.

**What is a router skill?**

A user-invoked map of other user-reachable skills. It reduces the number of individual commands a human must remember without adding always-loaded model context.

## It's working if

- Each instruction changes behavior rather than restating a default.
- Required references have precise trigger conditions.
- Steps remain easy to see and end with checkable completion criteria.
- One meaning has one source of truth.
- Skill invocation matches who must discover it.
