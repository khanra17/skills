---
name: to-tickets
description: Break a plan, spec, or the current conversation into tracer-bullet tickets, each declaring the tickets that block it, and publish them to the configured tracker.
disable-model-invocation: true
---

# To Tickets

Break a plan, spec, or conversation into a set of **tickets**: tracer-bullet vertical slices, each declaring the tickets that **block** it.

Read `docs/agents/issue-tracker.md` for how this repo's tracker works and `docs/agents/triage-labels.md` for its label strings. If the tracker guide is missing, tell the user to run `/setup-khanra17-skills`.

## Process

### 1. Gather context

Work from whatever is already in the conversation context. If the user passes a reference (a spec path, an issue number or URL) as an argument, fetch it and read its full body and comments.

### 2. Explore the codebase

If you have not already explored the codebase, do so to understand the current state of the code. Ticket titles and descriptions use the project's domain glossary vocabulary and respect ADRs in the area you're touching.

Look for opportunities to prefactor the code to make the implementation easier. "Make the change easy, then make the easy change."

### 3. Draft vertical slices

Break the work into **tracer bullet** tickets.

<vertical-slice-rules>

- Each slice cuts a narrow but complete path through every layer (schema, API, UI, tests): vertical, not a horizontal slice of one layer
- A completed slice is demoable or verifiable on its own
- Each slice is sized to fit in a single fresh context window
- Any prefactoring comes first

</vertical-slice-rules>

Give each ticket its **blocking edges**: the other tickets that must complete before it can start. A ticket with no blockers can start immediately.

**Wide refactors are the exception to vertical slicing.** A wide refactor is one mechanical change (rename a column, retype a shared symbol) whose blast radius fans across the whole codebase, so a single edit breaks thousands of call sites at once and no vertical slice can land green. Sequence it as **expand–contract**:

1. Expand: add the new form beside the old so nothing breaks.
2. Migrate: move the call sites over in batches sized by blast radius (per package, per directory), each batch its own ticket blocked by the expand. CI stays green batch to batch because the old form still exists.
3. Contract: delete the old form once no caller remains, in a ticket blocked by every migrate batch.

When even the batches can't stay green alone, keep the sequence but let them share an integration branch, with every batch blocking a final integrate-and-verify ticket. Green is promised only there.

### 4. Quiz the user

Present the proposed breakdown as a numbered list. For each ticket, show:

- **Title**: short descriptive name
- **Blocked by**: which other tickets (if any) must complete first
- **What it delivers**: the end-to-end behaviour this ticket makes work

Ask the user:

- Does the granularity feel right? (too coarse / too fine)
- Are the blocking edges correct: does each ticket only depend on tickets that genuinely gate it?
- Should any tickets be merged or split further?

If a slice needs a test seam the spec did not confirm, name it here and get it confirmed. Iterate until the user approves the breakdown.

### 5. Publish the tickets to the configured tracker

Publish the approved tickets in dependency order (blockers first), so each ticket's blocking edges can reference real identifiers. The tickets are the same on every tracker; only the shape of the edges changes:

- **Local files** → one file per ticket under `.scratch/<feature-slug>/issues/<NN>-<slug>.md`, numbered from `01`, using the local template below.
- **A real issue tracker (GitHub, Linear, …)** → one issue per ticket, using the issue template below and the platform's native blocking relationships where available. Apply the `ready-for-implementation` label unless instructed otherwise; the tickets need no further triage.

For GitHub, attach each ticket to its source parent issue with `gh issue edit <PARENT> --repo <owner>/<repo> --add-sub-issue <CHILD>`, and add each blocking dependency separately with `gh issue edit <CHILD> --repo <owner>/<repo> --add-blocked-by <BLOCKER>`. Without a source parent, publish standalone tickets. Attaching children is the only change made to a parent: its content and open or closed state stay as they are.

<local-ticket-template>

# <NN>: <Ticket title>

**Spec:** the path to the spec this ticket came from, when there is one.

**What to build:** the end-to-end behaviour this ticket makes work, from the user's perspective.

**Test seams:** the confirmed seams this slice is tested through, named as in the spec.

**Blocked by:** the numbers of the tickets that gate this one, or "None (can start immediately)".

**Status:** ready-for-implementation

- [ ] Acceptance criterion 1
- [ ] Acceptance criterion 2

</local-ticket-template>

<issue-template>

## Parent

A reference to the parent issue on the tracker (omit this section when the source was not an existing issue).

## What to build

The end-to-end behaviour this ticket makes work, from the user's perspective.

## Test seams

The confirmed seams this slice is tested through, named as in the spec.

## Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2

## Blocked by

- A reference to each blocking ticket, or "None (can start immediately)".

</issue-template>

In either form, describe behaviour: file paths and code snippets go stale fast. The exception is a prototype snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape); inline its decision-rich part and note that it came from a prototype.
