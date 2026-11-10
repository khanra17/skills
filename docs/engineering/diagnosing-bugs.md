# diagnosing-bugs

## What it does

`diagnosing-bugs` runs a disciplined loop for bugs whose cause isn't obvious, and for performance regressions:

1. Build a tight feedback loop: one command that goes red on this bug.
2. Reproduce the failure and shrink it to the smallest case that still fails.
3. Rank three to five falsifiable hypotheses.
4. Test one prediction at a time with targeted instrumentation.
5. Write a regression test, then fix the cause.
6. Remove the instrumentation, confirm the original symptom is gone, and report the cause.

It builds the loop before it forms theories. When the cause is already evident, such as a stack trace that names the line, it skips to step 5.

## When to reach for it

Type `/diagnosing-bugs`, or let the agent reach for it, when a failure is intermittent, appeared between two known-good states, or survived a first fix.

Use [triage](./triage.md) first when an incoming report still needs classifying. Use [tdd](./tdd.md) for planned behavior.

## Common questions

**What makes a feedback loop tight?**

It checks your exact symptom, gives the same verdict every run, finishes in seconds, and runs without a human.

**What if the bug is intermittent?**

The skill raises the reproduction rate by looping the trigger, adding stress, and pinning time or randomness. A bug that fails half the time can be diagnosed; one that fails 1% of the time can't yet.

**What if no automated loop is possible?**

As a last resort it writes a script that walks you through the manual steps and captures what you see. If even that fails, it stops, lists what it tried, and asks for access to the failing environment, a captured artifact, or permission to add temporary instrumentation.

**What if there is no good place for a regression test?**

It fixes the bug, verifies with the loop, and reports the missing seam, suggesting [improve-codebase-architecture](./improve-codebase-architecture.md) for that area. It does not add a shallow test that would pass whether or not the bug returned.

**How are secrets handled?**

Commands, output, and captured artifacts are redacted before they are shown. Credentials stay in environment variables.

## It's working if

- You are shown a command and its failing output before any explanation of the cause.
- The hypotheses each state what would change if they were true.
- No `[DEBUG-...]` lines remain in the code afterwards.
- The original reproduction passes after the fix.
