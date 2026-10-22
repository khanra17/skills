## What it does

`to-spec` turns the current conversation and codebase understanding into a spec, then publishes it to the configured issue tracker with the `ready-for-implementation` state.

It does not interview the user again. It synthesizes what has already been discussed, checks the repository, confirms the testing seams, and writes a detailed spec covering the problem, solution, user stories, implementation decisions, testing decisions, out-of-scope work, and further notes.

## When to reach for it

Type `/to-spec` after [grill-with-docs](./grill-with-docs.md), a cleared [wayfinder](./wayfinder.md) map, or any conversation that has settled the requirements.

Use [to-tickets](./to-tickets.md) next when the build needs several sessions. For a small change that fits the current session, go directly to [implement](./implement.md).

## Common questions

**Will it ask me more design questions?**

No. It only confirms that the proposed testing seams match your expectations. If important product decisions remain open, return to grilling first.

**Why is the user-story list long?**

The spec is meant to cover all aspects of the feature, including edge cases and less common actors. The extensive list is intentional.

**Does it include file paths or code snippets?**

Normally no, because both become stale. A decision-rich snippet from a prototype may be included when it expresses a state machine, schema, reducer, or type shape more precisely than prose.

**Where is the spec published?**

The repository's `docs/agents/issue-tracker.md` decides. Run [setup-khanra17-skills](./setup-khanra17-skills.md) first if that configuration is missing.

## It's working if

- The spec uses the project's glossary vocabulary and respects relevant ADRs.
- Testing seams are explicit and confirmed.
- User stories cover the full feature rather than only the happy path.
- Implementation decisions describe stable contracts without brittle file paths.
- The published spec needs no additional triage before planning or implementation.
