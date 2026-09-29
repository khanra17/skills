## What it does

`diagnosing-bugs` runs a disciplined loop for hard bugs and performance regressions:

1. Build a tight feedback loop.
2. Reproduce and minimise the failure.
3. Rank falsifiable hypotheses.
4. Instrument one prediction at a time.
5. Fix the cause and add a regression test at the correct seam.
6. Remove temporary instrumentation and verify the original symptom is gone.

The skill refuses to guess before one command can detect the exact bug.

## When to reach for it

Type `/diagnosing-bugs`, or describe something broken, failing, throwing, intermittent, or slow and let the agent reach for it.

Use it for a specific symptom that needs investigation. Use [triage](./triage.md) first when an incoming report still needs classification and basic verification. Use [tdd](./tdd.md) for planned behavior rather than diagnosis.

## Common questions

**What makes a feedback loop tight?**

It is fast, deterministic, agent-runnable, and red-capable for the user's exact symptom. A nearby failure or a command that only checks for crashes is not enough.

**What if the bug is intermittent?**

Raise its reproduction rate by looping, adding stress, controlling time or randomness, and narrowing timing windows. A reliable high failure rate is enough to diagnose a flaky bug.

**What if no automated loop is possible?**

The skill can use the included human-in-the-loop Bash template as a last resort. If no useful loop can be built, it stops, lists what it tried, and asks for access, a redacted artifact, or permission to add temporary instrumentation.

**How are secrets handled?**

Commands, outputs, and captured artifacts must be redacted before they are shown. Credentials stay in environment variables, and only signal-carrying lines are quoted.

**What if there is no correct seam for a regression test?**

The skill records that architecture gap instead of adding a shallow test that gives false confidence. [Improve-codebase-architecture](./improve-codebase-architecture.md) can then help find a better seam.

## It's working if

- A command goes red on the reported symptom before hypotheses appear.
- The reproduction is reduced until every remaining part is necessary.
- You see three to five ranked hypotheses with predictions.
- Debug logs carry a unique tag and are removed before completion.
- The original reproduction goes green after the fix.
