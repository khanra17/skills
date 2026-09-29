## What it does

`tdd` builds behavior through repeated red-green slices:

1. Agree the public seam to test.
2. Write one test that fails for the missing behavior.
3. Add the smallest implementation that makes it pass.
4. Repeat with the next behavior.

Tests observe public behavior rather than private structure. Refactoring happens during review, outside the red-green implementation loop.

## When to reach for it

Type `/tdd`, or let [implement](./implement.md) use it while building a ticket or spec.

Use it for a concrete feature or bug fix that should be built test-first. Use [codebase-design](./codebase-design.md) when the interface or seam itself still needs design. Use [diagnosing-bugs](./diagnosing-bugs.md) when you first need to discover the cause of a hard failure.

## Common questions

**What is a seam?**

The public interface where behavior is observed. Callers and tests should cross the same seam without reaching into implementation details.

**Why must the seam be agreed first?**

A test suite can become expensive noise when it targets the wrong level. Agreement focuses testing effort on the behavior and interfaces that matter.

**What makes a test implementation-coupled?**

It mocks internal collaborators, calls private methods, asserts call order, or checks state through a side channel. Such a test breaks when the implementation changes even though behavior remains correct.

**When should I mock?**

At real system boundaries such as third-party APIs, time, randomness, and sometimes databases or filesystems. Prefer realistic local substitutes where available. Do not mock your own internal modules merely to isolate them.

**Why not write all tests first?**

That is horizontal slicing against imagined behavior. One test and one implementation at a time lets each result teach the next slice.

## It's working if

- Every test starts red for the intended reason.
- Expected values come from the spec or a known example, not from repeating the implementation.
- Tests use public interfaces and survive internal refactors.
- Each cycle adds one behavior and the minimum code needed for it.
- Refactoring waits until the review stage.
