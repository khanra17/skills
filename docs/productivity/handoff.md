# handoff

## What it does

`handoff` writes a Markdown document that lets a fresh agent continue the current work without this conversation. It covers the goal and current state, the decisions made and why, what was tried and abandoned, and the next step with a way to check it.

The file is saved in the operating system's temporary directory, and the agent tells you its path. Existing specs, issues, ADRs, commits, and diffs are linked, not copied.

## When to reach for it

Type `/handoff` when work has to travel: to another harness, another directory or repository, a colleague, or a side session forked from the middle of a task.

If you need more room in the same session and place, compacting fits better. If the earlier context no longer matters, clear it.

## Common questions

**What does the argument do?**

`/handoff <what the next session is for>` focuses the document. It keeps what serves that purpose and leaves out the rest.

**How does the next session use it?**

Open the new session and point it at the file path.

**Should I commit the file?**

It is a bridge between two contexts, so it stays in the temporary directory. Anything in it worth keeping belongs in a spec, an ADR, or an issue.

## It's working if

- The agent reports an absolute path outside your repository.
- A fresh agent given only that file can state the next step and the reason for each earlier decision.
- The document links to existing artifacts instead of repeating their content.
