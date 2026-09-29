## What it does

`research` delegates a question to a background agent. The agent reads high-trust primary sources such as official documentation, specifications, source code, and first-party APIs, then writes one cited Markdown file.

The file goes wherever the repository already keeps research notes. If no convention exists, the agent chooses a sensible location and reports it.

## When to reach for it

Type `/research`, or let the agent reach for it when substantial reading can happen in the background while the main session continues.

Use it for external facts that a decision depends on. Use [prototype](./prototype.md) when the question must be answered by running something in the codebase. Use [grilling](../productivity/grilling.md) when the open question is a decision for the user rather than a fact to discover.

## Common questions

**What counts as a primary source?**

The source that owns the claim: official docs, the actual specification, first-party API output, or the relevant source code. Secondary summaries may help discovery but should not support the final claim.

**Where should the result live?**

The skill follows the repository's existing convention. Research can become stale, so keep, archive, or delete the file according to the project's normal documentation policy.

**Does another session read old research automatically?**

No. Point the next skill, ticket, or conversation at the file when its findings are needed.

**How should I scope the question?**

Ask one answerable question and name any version, API, or behavior that matters. A broad topic produces a broad report and can miss the fact blocking your decision.

**How does wayfinder use research?**

[Wayfinder](./wayfinder.md) dispatches newly created research tickets only when they are on the frontier, meaning open, unblocked, and unclaimed. It claims each ticket before starting the subagent.

## It's working if

- The main session remains available while the reading happens.
- One Markdown file contains the result.
- Each important claim cites the primary source that supports it.
- The report answers the scoped question rather than surveying the whole topic.
- The result can be passed into a decision or spec without repeating the research.
