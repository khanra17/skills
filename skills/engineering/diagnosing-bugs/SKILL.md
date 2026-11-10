---
name: diagnosing-bugs
description: Diagnosis loop for bugs whose cause is not obvious, and for performance regressions. Use when the user says "diagnose" or "debug this", when a failure is intermittent or appeared between two known-good states, or when a first fix did not cure it.
---

# Diagnosing Bugs

A discipline for hard bugs. When the cause is already evident (a stack trace that names the line, a typo, an obvious off-by-one), go straight to Phase 5: regression test, then fix. Otherwise work the phases in order, and say why if you skip one.

When exploring the codebase, read `GLOSSARY.md` (if it exists) to get a clear mental model of the relevant modules, and check ADRs in the area you're touching.

## Redact

This skill has you show commands, outputs and captured artifacts. **Redact every secret first**: write `<REDACTED>` in its place. Build loops against env vars, so the credential stays in the environment. Captured artifacts carry auth headers: quote only the lines that carry the signal.

If the redacted output is not enough to diagnose the bug, say so and ask the user.

## Phase 1: Build a feedback loop

The loop is what finds the bug. A **tight** pass/fail signal that goes red on this bug is what bisection, hypothesis-testing, and instrumentation all consume; without one, you are reading code and guessing. Spend most of the effort here, and try the constructions below in order before concluding a loop is impossible.

### Ways to construct one, in roughly this order

1. **Failing test** at whatever seam reaches the bug: unit, integration, e2e.
2. **Curl / HTTP script** against a running dev server.
3. **CLI invocation** with a fixture input, diffing stdout against a known-good snapshot.
4. **Headless browser script** (Playwright / Puppeteer) that drives the UI and asserts on DOM/console/network.
5. **Replay a captured trace.** Save a real network request, payload, or event log to disk; replay it through the code path in isolation.
6. **Throwaway harness.** Spin up a minimal subset of the system (one service, mocked deps) that exercises the bug code path with a single function call.
7. **Property / fuzz loop.** If the bug is "sometimes wrong output", run 1000 random inputs and look for the failure mode.
8. **Bisection harness.** If the bug appeared between two known states (commit, dataset, version), automate "boot at state X, check, repeat" so you can `git bisect run` it.
9. **Differential loop.** Run the same input through old-version vs new-version (or two configs) and diff outputs.
10. **HITL bash script.** Last resort. If a human must click, drive them with `scripts/hitl-loop.template.sh` so the loop is still structured. Captured output feeds back to you.

### Tighten the loop

Once you have a loop, tighten it:

- Faster: cache setup, skip unrelated init, narrow the test scope.
- Sharper: assert on the specific symptom, not "didn't crash".
- More deterministic: pin time, seed RNG, isolate filesystem, freeze network.

A 30-second flaky loop is barely better than no loop; a 2-second deterministic one is tight.

### Non-deterministic bugs

The goal is a **higher reproduction rate**, not a clean repro. Loop the trigger 100×, parallelise, add stress, narrow timing windows, inject sleeps. A 50%-flake bug is debuggable; 1% is not, so keep raising the rate until it is.

### When you cannot build a loop

Stop and say so. List what you tried. Ask the user for: (a) access to whatever environment reproduces it, (b) a redacted captured artifact (HAR file, log dump, core dump, screen recording with timestamps), or (c) permission to add temporary production instrumentation. Hypothesising waits until a loop exists.

### Completion criterion: a tight loop that goes red

Phase 1 is done when you can name **one command** (a script path, a test invocation, a curl) that you have **already run at least once** (show the invocation and its output, redacted), and that is:

- [ ] **Red-capable**: it drives the actual bug code path and asserts the **user's exact symptom**, so it goes red on this bug and green once fixed. "Runs without erroring" does not qualify.
- [ ] **Deterministic**: same verdict every run (flaky bugs: a pinned, high reproduction rate, per above).
- [ ] **Fast**: seconds, not minutes.
- [ ] **Agent-runnable**: you can run it unattended; a human in the loop only via `scripts/hitl-loop.template.sh`.

If you catch yourself reading code to build a theory before this command exists, stop and go back to building the loop. Phase 2 starts only with a red-capable command.

## Phase 2: Reproduce + minimise

Run the loop and watch it go red.

Confirm:

- [ ] The loop produces the failure mode the **user** described, not a different failure that happens to be nearby. Wrong bug = wrong fix.
- [ ] The failure is reproducible across multiple runs (or, for non-deterministic bugs, at a high enough rate to debug against).
- [ ] You have captured the exact symptom (error message, wrong output, slow timing) so later phases can verify the fix addresses it.

### Minimise

Shrink the repro to the **smallest scenario that still goes red**. Cut inputs, callers, config, data, and steps **one at a time**, re-running the loop after each cut. A minimal repro leaves fewer moving parts to suspect in Phase 3 and becomes the regression test in Phase 5.

Done when **every remaining element is load-bearing**: removing any one of them makes the loop go green.

## Phase 3: Hypothesise

Generate **3–5 ranked hypotheses** before testing any of them. A single hypothesis anchors on the first plausible idea.

Each hypothesis is **falsifiable**: it states the prediction it makes.

> Format: "If <X> is the cause, then <changing Y> will make the bug disappear / <changing Z> will make it worse."

A hypothesis with no prediction gets sharpened or discarded.

**Show the ranked list to the user before testing.** They often have domain knowledge that re-ranks it instantly ("we just deployed a change to #3"), or know hypotheses already ruled out. If the user is AFK, proceed with your ranking.

## Phase 4: Instrument

Each probe maps to a specific prediction from Phase 3. **Change one variable at a time.**

Tool preference:

1. **Debugger / REPL inspection** if the env supports it. One breakpoint beats ten logs.
2. **Targeted logs** at the boundaries that distinguish hypotheses.

**Tag every debug log** with a unique prefix, e.g. `[DEBUG-a4f2]`, so cleanup is a single grep.

**Perf branch.** For performance regressions, establish a baseline measurement first (timing harness, `performance.now()`, profiler, query plan), then bisect. Measure first, fix second.

## Phase 5: Fix + regression test

Write the regression test **before the fix**, at a **correct seam**: one where the test exercises the real bug pattern as it occurs at the call site. A seam that is too shallow (a single-caller test when the bug needs multiple callers, a unit test that can't replicate the chain that triggered the bug) gives false confidence, so a test there is worse than none.

If a correct seam exists:

1. Turn the minimised repro into a failing test at that seam.
2. Watch it fail.
3. Apply the fix.
4. Watch it pass.
5. Re-run the Phase 1 feedback loop against the original (un-minimised) scenario.

If no correct seam exists, fix the bug, verify with the Phase 1 loop, and carry the missing seam into the Phase 6 report: the architecture is what stops this bug being locked down.

## Phase 6: Clean up and report

Before declaring done:

- [ ] Original repro no longer reproduces (re-run the Phase 1 loop)
- [ ] Regression test passes, or the missing seam is reported
- [ ] All `[DEBUG-...]` instrumentation removed (`grep` the prefix)
- [ ] Throwaway harnesses deleted, or moved to a clearly marked debug location

Then report the cause that turned out correct and the evidence for it, and put the same cause in the commit or PR message so the next debugger learns from it. If Phase 5 found no correct seam, say which area lacks one and suggest the user run `/improve-codebase-architecture` on it.
