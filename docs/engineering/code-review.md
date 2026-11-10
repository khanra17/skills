# code-review

## What it does

`code-review` reviews committed or work-in-progress changes since a fixed point, along three axes:

- **Standards:** does the change follow the repository's documented standards, its ADRs, and its glossary, plus a baseline of twelve common code smells?
- **Spec:** does the change implement the ticket, spec, or agreed requirements, with nothing missing and nothing extra?
- **Correctness:** does the code work, and would its tests catch it if it didn't?

Each axis runs in its own subagent on the same diff, and the three reports are shown separately. Every finding is marked **hard** or **judgement call**.

## When to reach for it

Type `/code-review` to review a branch, a pull request, or the working tree since a commit, branch, tag, or merge base. [implement](./implement.md) runs it before committing.

Use [diagnosing-bugs](./diagnosing-bugs.md) when the question is why something is broken, and [improve-codebase-architecture](./improve-codebase-architecture.md) for a survey of the whole codebase.

## Common questions

**What do I pass as the fixed point?**

The commit or branch where the work started. `/implement` records its starting commit and passes it for you.

**Can it review uncommitted work?**

Yes. Working-tree mode covers committed, staged, and unstaged changes since the fixed point, and reads new untracked files as additions.

**Where does the Spec review get its requirements?**

From the spec or ticket you supply, then requirements agreed in the conversation, then issue references in commit messages, then a matching spec file. With none of those, it skips the Spec axis and says so.

**Why are the reports kept separate?**

A change can be clean and still build the wrong thing, or build the right thing with a bug in it. One merged ranking would let a pass on one axis hide a failure on another.

**Is this the same as Claude Code's built-in `/code-review`?**

No. They share a name and take different arguments. If you run these skills in Claude Code, check which one `/code-review` reaches there.

## It's working if

- The report has three headings, each with its own findings or a plain "nothing found".
- A standards finding cites the rule or names the smell; a spec finding quotes the requirement; a bug names the input that triggers it.
- The summary line gives hard and judgement-call counts per axis.
