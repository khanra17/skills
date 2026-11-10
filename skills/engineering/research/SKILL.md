---
name: research
description: Investigate a question against primary sources and return cited findings. Use when the user wants a topic researched, docs or API facts gathered, the way established projects solve a problem compared, or reading legwork delegated to a background agent.
---

Answer a question from primary sources, citing each claim.

## Who does the reading

If you are the main session and can dispatch agents, hand the research to a background agent with a fresh context window, give it this skill and the question, and keep working while it reads. If you are that agent, or the harness has no agents, do the research yourself.

## Method

1. **Pin the question.** One answerable question, with the versions, APIs, or constraints that matter. When the question is about a proposed solution, research the need behind it too: the finding may be that a different approach, or no feature at all, serves it better.
2. **Read primary sources**: official docs, specifications, source code, release notes, first-party API output. A secondary write-up is a way to find the source, never the citation.
3. **Trace each claim** to the source that owns it, and link it pinned: a commit SHA for code, a version or access date for docs.
4. **Separate what you observed, what you infer, and what you could not find.** Where reading cannot settle the question, name the experiment or test that would.

## When the source is other projects' code

Use this branch to learn how established projects handle a problem.

- Pick two or three projects that face the same constraints. Popularity gets a project considered; what earns it a place is the engineering you inspect: its failure handling, its tests, how maintained the relevant code is, and how its dependency versions compare with ours.
- Read at a pinned commit. Shallow-clone into a temporary directory outside the working project (`git clone --depth 1`), or read through the host's API. If a code index of the project is already available, use it to navigate and confirm what it reports in the source.
- Read the implementation, its callers, and its tests, then look for a competing approach before settling on the first match.
- Code shows what a project does, not why. For rationale, read its docs, release notes, and design discussions.
- A practice seen in a few projects is not an industry norm. Support broader claims with standards or first-party guidance, or qualify them.
- For each approach worth reporting, state the constraints it serves, its failure cases, and its costs. Separate ideas that transfer from obsolete APIs and from complexity our problem lacks.
- Reference code is evidence. Reading it is in scope; installing its dependencies or running it needs the user's go-ahead.

## Output

One Markdown report: the answer first, then the findings with their citations, then what could not be established.

- Research that belongs to an issue: the invoking workflow posts the full report as a `## Research findings` comment on that issue and checks it was saved.
- Otherwise: write the report to the OS temporary directory and return its absolute path. Write it into the repo only when the user asks, following the repo's existing convention for such notes.
