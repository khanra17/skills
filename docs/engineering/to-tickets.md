## What it does

`to-tickets` breaks a plan, spec, or conversation into tracer-bullet implementation tickets. Each ticket delivers a narrow but complete path through the system and declares which other tickets block it.

It shows the proposed breakdown for approval before publishing. Local trackers receive one Markdown file per ticket. Real trackers receive one issue per ticket with native parent and blocking relationships where available.

## When to reach for it

Type `/to-tickets` when the work is too large for one [implement](./implement.md) session.

Use it after [to-spec](./to-spec.md) or directly from an already settled plan. Do not use it for wayfinder decision tickets; those answer planning questions, while these tickets build the decided behavior.

## Common questions

**What makes a ticket a vertical slice?**

It delivers observable behavior through every required layer and can be demonstrated or verified on its own. A ticket containing only schema work or only UI work is usually horizontal.

**How large should each ticket be?**

Small enough for one fresh context window, but complete enough to produce a useful result. The user reviews whether the proposed granularity is too coarse or too fine.

**How are wide mechanical refactors handled?**

With an expand-contract sequence: introduce the new form, migrate callers in safe batches, then remove the old form. Blocking edges keep the order clear.

**How does GitHub publishing work?**

Generated tickets become sub-issues of the source parent when one exists. Blocking relationships are added separately because parenthood and blocking mean different things. Without a source parent, tickets are standalone.

**Does it choose the breakdown without asking?**

No. It presents titles, blockers, and delivered behavior, then waits for approval before publishing.

## It's working if

- Every ticket delivers a complete, testable behavior.
- Each blocker is a real prerequisite rather than a preferred order.
- Independent tickets can start immediately.
- Wide refactors keep the codebase buildable between migration batches.
- Published tickets use the configured tracker and the canonical ready state.
