## What it does

`code-review` reviews committed or work-in-progress changes against a fixed point along two separate axes:

- **Standards:** whether the change follows repository standards and a baseline of common code smells.
- **Spec:** whether the change implements the supplied ticket, spec, or agreed requirements.

The two reviews run in parallel subagents with the same diff, commit list, scope, and relevant untracked files. Their findings stay separate so one passing axis cannot hide a failure in the other.

## When to reach for it

Type `/code-review` when you want a branch, pull request, or working tree reviewed since a commit, branch, tag, or merge base. [implement](./implement.md) also runs it before committing.

Use [diagnosing-bugs](./diagnosing-bugs.md) when the main question is why something is broken. Use [improve-codebase-architecture](./improve-codebase-architecture.md) for a whole-codebase architecture survey.

## Common questions

**Can it review uncommitted work?**

Yes. Working-tree mode includes tracked committed, staged, and unstaged changes since the fixed point. Relevant untracked files are listed and read as additions. New-file-only work is not treated as an empty review.

**What should I pass as the fixed point?**

Pass the commit or branch that represents the start of the work. `/implement` captures its starting commit and supplies it automatically.

**Where does the Spec review get its requirements?**

It prefers an explicitly supplied spec or ticket, then requirements agreed in the conversation, then issue references in commit messages, then a matching local spec. If no requirements exist, it skips that axis and says so.

**What standards does it use?**

Repository documents such as `AGENTS.md`, `CONTRIBUTING.md`, or coding standards take priority. A fixed Fowler smell baseline applies as judgment, not as hard law, and documented repository choices override it.

## It's working if

- Both reviewers inspect exactly the same scoped change.
- Unrelated existing work is excluded.
- Standards findings cite the repository rule or name the smell.
- Spec findings quote the requirement they concern.
- The final report gives separate counts and worst findings for each axis.
