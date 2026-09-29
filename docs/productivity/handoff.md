## What it does

`handoff` writes a portable Markdown summary so another session or agent can continue the work. It saves the document in the operating system's temporary directory, not in the current repository.

The document points to existing specs, issues, ADRs, commits, and diffs instead of copying them. It also lists the skills the next agent should use.

## When to reach for it

Type `/handoff` when work must move to another harness, directory, repository, colleague, or side session.

If you only need more room in the same context and location, compacting may be a better fit. If the previous context is irrelevant, clear it instead.

## Common questions

**Where is the handoff saved?**

In the temporary directory for the user's operating system. The skill reports the path.

**What happens when I pass an argument?**

The argument describes the next session's focus. The handoff keeps information relevant to that focus and leaves unrelated history out.

**Does it copy the full conversation?**

No. It summarizes the state needed to continue and references durable artifacts for their details.

**Why include suggested skills?**

A fresh agent needs to know which procedures or reference vocabularies apply. The section names them explicitly.

**Should I commit the handoff file?**

Normally no. It is a temporary bridge between contexts, not project documentation.

## It's working if

- A fresh agent can continue without rereading the original conversation.
- Existing artifacts are linked rather than duplicated.
- Decisions, constraints, current state, and next actions are clear.
- The document contains no unrelated conversation history.
- The next session's relevant skills are named.
