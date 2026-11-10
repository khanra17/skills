# implement

## What it does

`implement` builds the work described by a spec, a ticket, or requirements agreed in the conversation. It runs five steps:

1. **Load the work.** It reads the ticket and its parent spec, records the starting commit, and notes any changes already in the working tree so they stay out of the task.
2. **Build.** It uses [tdd](./tdd.md) at the test seams the spec or ticket names, one red-green slice at a time.
3. **Verify.** It runs the feature on every surface the change touches, including failure and recovery paths, and looks at visible UI changes in the running app.
4. **Review and fix.** It calls [code-review](./code-review.md) on the working tree, fixes the hard findings, and lists the judgement calls it left for you.
5. **Commit and finish.** It commits through [git-commit](./git-commit.md) to the current branch and finishes the ticket.

## When to reach for it

Type `/implement` when the decisions are settled and the work is ready to build. Name the ticket, or name the spec and it takes the first ticket whose blockers are finished.

For a multi-ticket effort, start a fresh session for each ticket.

## Common questions

**How does a ticket get closed?**

On GitHub, the commit carries a `Closes #N` footer, so the issue closes when that commit reaches the default branch. Until you push or merge, the ticket stays open and anything it blocks stays blocked. On a local tracker, the ticket file is marked `done` in the same commit. When the last ticket of a spec finishes, the spec closes with it.

**Does it create or switch branches?**

It commits to the branch you are on. Choose the branch before you start.

**What does it do with review findings?**

It fixes documented-standard violations, spec gaps, and bugs. For judgement calls such as code smells, it applies the cheap and clearly better ones and reports the rest.

**What if it can't check something?**

It says so. The final report lists what was verified and how, and names every surface it could not check.

**What if I have a GitHub Project?**

When one is configured, implement tells [github-project](./github-project.md) when work starts and what the verified outcome was. The board's own completion criteria decide the stage.

## It's working if

- The commit contains only this task's changes, and on GitHub its message ends with `Closes #N`.
- Tests were written before the code they cover, at the seams the ticket names.
- The final report separates what was verified from what was not.
- After the commit lands, the tickets this one blocked show as startable.
