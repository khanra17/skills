---
name: tdd
description: Test-driven development. Use when the user wants to build features or fix bugs test-first, mentions "red-green-refactor", or wants integration tests.
---

# Test-Driven Development

TDD is the red → green loop. This skill makes that loop produce tests worth keeping: what a good test is, where tests go, the anti-patterns, and the rules of the loop.

When exploring the codebase, read `GLOSSARY.md` (if it exists) so test names and interface vocabulary match the project's domain language, and respect ADRs in the area you're touching.

## What a good test is

Tests verify behavior through public interfaces. A good test reads like a specification: "user can checkout with valid cart" names a capability, and it survives a rewrite of the internals because it never looks at them.

Before the first test of a session, read [tests.md](tests.md) for paired good and bad examples. When a test has to cross a system boundary (a third-party API, time, randomness, a database, the filesystem), read [mocking.md](mocking.md) for what to substitute and how.

## Seams: where tests go

A **seam** is the public boundary you test at: the interface where you observe behavior without reaching inside. Tests live at seams.

**Test at agreed seams.** When the spec or ticket names its test seams, use those. Otherwise write down the seams you intend to test and confirm them with the user before the first test: "What's the public interface, and which seams should we test?" You can't test everything, and agreeing the seams is how testing effort lands on the critical paths and complex logic.

When the shape of the interface is itself in question (how deep the module is, where the seam belongs, what the interface should expose), invoke the `codebase-design` skill for the vocabulary. It is a reference to consult, not a session to run.

## Anti-patterns

- **Implementation-coupled**: mocks internal collaborators, tests private methods, or verifies through a side channel (querying the database instead of using the interface). The tell: the test breaks when you refactor but behavior hasn't changed.
- **Tautological**: the assertion recomputes the expected value the way the code does (`expect(add(a, b)).toBe(a + b)`, a snapshot derived by hand the same way, a constant asserted equal to itself), so it passes by construction and can never disagree with the code. Expected values come from an independent source of truth: a known-good literal, a worked example, the spec.
- **Horizontal slicing**: writing all tests first, then all implementation. Bulk tests verify imagined behavior: they test the shape of things, go insensitive to real changes, and commit to a test structure before the implementation is understood. Work in **vertical slices**: one test → one implementation → repeat, each test a **tracer bullet** that responds to what the last cycle taught you.

## Rules of the loop

- **Red before green.** Write the failing test first and watch it fail for the intended reason, then write only enough code to pass it.
- **One slice at a time.** One seam, one test, one minimal implementation per cycle.
- **Refactor after the loop.** Once the behavior is green, review does the refactoring: `implement` runs it as its review step, and when you are using this skill alone, invoke the `code-review` skill on the finished change.
