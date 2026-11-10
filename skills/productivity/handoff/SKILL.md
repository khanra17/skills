---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff document that lets a fresh agent continue this work with no access to this conversation. Save it as a Markdown file in the OS temporary directory, outside the current workspace, and tell the user its absolute path.

Cover what the next agent cannot recover from the repo:

- the goal and the current state of the work
- the decisions made and the reason behind each
- what was tried and abandoned, and why
- the next step, and how to check it worked

Content that already lives in another artifact (a spec, plan, ADR, issue, commit, or diff) is referenced by path or URL instead of copied.

If the user passed arguments, they describe what the next session will focus on: keep what serves that focus and leave the rest out.
