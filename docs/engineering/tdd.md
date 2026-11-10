# tdd

## What it does

`tdd` builds behavior through red-green slices:

1. Agree the seam to test at.
2. Write one test that fails for the missing behavior.
3. Add the smallest implementation that makes it pass.
4. Repeat with the next behavior.

Tests observe public behavior through the interface callers use. Refactoring happens afterwards, in review.

## When to reach for it

Type `/tdd`, or let [implement](./implement.md) use it while building a ticket.

Use it for a concrete feature or bug fix you want built test-first. Use [codebase-design](./codebase-design.md) when the interface itself still needs designing, and [diagnosing-bugs](./diagnosing-bugs.md) when you first have to find out why something fails.

## Common questions

**What is a seam?**

The public interface where behavior is observed. Tests and callers cross the same seam, so a test never reaches into the implementation.

**Will it ask me which seams to test?**

Only when nothing has settled them. If the spec or ticket names its seams, it uses those.

**When does it mock?**

Only at boundaries the project doesn't control: third-party APIs, time, randomness. For a database or filesystem it prefers a real local stand-in. Where it does substitute, it uses a small working fake over a script of expected calls, so the test can still assert on outcomes.

**Where did the refactor step go?**

To review. Inside [implement](./implement.md) that is the review-and-fix step; when you use `tdd` alone, run [code-review](./code-review.md) on the finished change.

## It's working if

- Each test is seen failing before the code that makes it pass exists.
- Expected values are literals or worked examples, never recomputed the way the code computes them.
- Renaming or restructuring internals leaves the tests green.
