---
name: to-spec
description: "Turn the current conversation into a spec and publish it to the project issue tracker: no interview, just synthesis of what you've already discussed."
disable-model-invocation: true
---

Turn the current conversation and your understanding of the codebase into a spec. Synthesize what is already settled; this is not another interview.

Read `docs/agents/issue-tracker.md` for how this repo's tracker works and `docs/agents/triage-labels.md` for its label strings. If the tracker guide is missing, tell the user to run `/setup-khanra17-skills`.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already. Use the project's domain glossary vocabulary throughout the spec, and respect any ADRs in the area you're touching.

2. Sketch the seams at which the feature will be tested. Prefer existing seams to new ones, and the highest seam that still observes the behaviour: one seam for the whole feature is the ideal. Check with the user that these seams match their expectations. This is the one question this skill asks.

3. Write the spec using the template below, then publish it to the issue tracker with the `ready-for-implementation` label. It needs no further triage.

<spec-template>

## Problem Statement

The problem that the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## User Stories

A numbered list of user stories, each in the format:

1. As an <actor>, I want a <feature>, so that <benefit>

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending
</user-story-example>

Write one story for each actor and need the conversation settled, including the edge cases and failure cases it covered. The list is as long as the feature is wide; a story the conversation never touched does not belong.

## Implementation Decisions

The implementation decisions that were made. This can include:

- The modules that will be built or modified
- The interfaces of those modules that will be modified
- Technical clarifications from the developer
- Architectural decisions
- Schema changes
- API contracts
- Specific interactions

Describe contracts and behaviour. File paths and code snippets go stale quickly, so leave them out, with one exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline its decision-rich part within the relevant decision and note that it came from a prototype.

## Testing Decisions

- The seams confirmed in step 2, each named precisely enough that a fresh session can find it
- Which modules are tested through each seam
- Prior art: similar tests already in the codebase

## Out of Scope

The things that are out of scope for this spec.

</spec-template>
