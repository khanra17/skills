# research

## What it does

`research` answers a question from primary sources (official documentation, specifications, source code, release notes, first-party API output) and returns a cited Markdown report: the answer, the findings behind it, and what could not be established.

It also covers a second kind of question: how established projects solve a problem. For that it picks two or three projects facing the same constraints, reads their code, callers, and tests at a pinned commit, and reports each approach with the constraints it serves, where it fails, and what it costs.

Where the harness supports background agents, the reading runs in one while your session continues.

## When to reach for it

Type `/research`, or let the agent reach for it, when a decision depends on facts outside the conversation: what an API guarantees, what a version changed, how other projects handle the problem you are about to solve.

Use [prototype](./prototype.md) when the answer has to come from running something in your own codebase. Use [grilling](../productivity/grilling.md) when the open question is a decision for you, not a fact to find.

## Common questions

**Where does the report go?**

To a file in the OS temporary directory, and the agent gives you the path. Research that belongs to an issue is posted on that issue as a "Research findings" comment. It is written into the repository only when you ask.

**What counts as a primary source?**

The source that owns the claim. A blog post or summary can lead the agent to it, but the citation is the doc, spec, or code itself, pinned to a version or commit.

**Can it tell me my proposed feature is a bad idea?**

It can show evidence for that. When you ask how to build something, it also looks at the need behind it, and other projects may meet that need another way or not at all. The decision stays yours.

**How should I scope the question?**

Ask one answerable question and name the version, API, or constraint that matters. A broad topic gets a broad report that can miss the fact your decision is waiting on.

**How does wayfinder use it?**

[Wayfinder](./wayfinder.md) dispatches each research ticket on its frontier to a subagent that follows this skill. The full report becomes the ticket's resolution comment.

## It's working if

- The report opens with the answer to the question you asked.
- Each claim links to a primary source pinned to a version or commit.
- What was observed, what was inferred, and what was not found are told apart.
- No cloned reference code is left inside your project.
