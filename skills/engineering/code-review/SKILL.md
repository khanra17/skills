---
name: code-review
description: "Review the changes since a fixed point (commit, branch, tag, or merge-base) along three axes: Standards (does the code follow this repo's documented standards?), Spec (does it match what the originating issue or spec asked for?), and Correctness (does it work, and can its tests catch it failing?). Runs the reviews in parallel sub-agents and reports them side by side. Use when the user wants to review a branch, a PR, work-in-progress changes, or asks to \"review since X\"."
---

Three-axis review of committed or work-in-progress changes against a supplied fixed point:

- **Standards**: does the code conform to this repo's documented standards?
- **Spec**: does the code faithfully implement the originating issue or spec?
- **Correctness**: does the code work, and would its tests catch it if it didn't?

Each axis runs as its own sub-agent with a fresh context window, in parallel, and their findings are reported separately. A change can pass one axis and fail another (clean code that builds the wrong thing; the right thing with a bug in it), and separate reports stop one axis from masking another.

## Process

### 1. Pin the fixed point and scope

Use the fixed point supplied by the user or invoking skill (a commit SHA, branch name, tag, `main`, `HEAD~5`, etc.). If none was supplied, ask for it.

Confirm the fixed point resolves (`git rev-parse <fixed-point>`) and select the requested review mode:

- **Committed branch/PR:** `git diff <fixed-point>...HEAD`, comparing against the merge-base.
- **Working tree:** `git diff <fixed-point>`, including tracked committed, staged, and unstaged changes since that point. List untracked files with `git ls-files --others --exclude-standard` and read relevant ones as additions.

Keep the supplied task scope; exclude unrelated changes. Capture the selected diff command, scope, relevant untracked-file paths, and commit list (`git log <fixed-point>..HEAD --oneline`) for the reviewers.

Stop on an invalid ref, or when the scoped diff is empty and there are no relevant untracked files.

### 2. Identify the spec source

Look for the originating spec, in this order:

1. The spec or ticket supplied by the user or invoking skill, or the requirements already agreed in the conversation.
2. Issue references in the commit messages (`#123`, `Closes #45`, etc.), fetched the way `docs/agents/issue-tracker.md` describes when that guide exists.
3. A spec file under `docs/`, `specs/`, or `.scratch/` matching the branch name or feature.
4. If nothing is found, ask the user where the spec is. If there isn't one, skip the Spec sub-agent and report "no spec available".

### 3. Identify the standards sources

Everything in the repo that says how code here should be written:

- Root and scoped `AGENTS.md` files, `CONTRIBUTING.md`, and any coding-standards document
- ADRs in the area the diff touches (`docs/adr/` and context-scoped ADR directories): a change that contradicts one is a finding
- `GLOSSARY.md`: a domain concept named with a synonym the glossary avoids is a finding
- Linter, formatter, and type-checker configuration, to know what tooling already enforces so the review can skip it

On top of what the repo documents, the Standards axis carries the **smell baseline** below: a fixed set of Fowler code smells (_Refactoring_, ch.3) that applies even when a repo documents nothing. Two rules bind it:

- **The repo overrides.** A documented repo standard always wins; where it endorses something the baseline would flag, suppress the smell.
- **Always a judgement call.** Each smell is a labelled heuristic ("possible Feature Envy"), never a hard violation.

Each smell reads *what it is* → *how to fix*:

- **Mysterious Name**: a function, variable, or type whose name doesn't reveal what it does or holds. → rename it; if no honest name comes, the design's murky.
- **Duplicated Code**: the same logic shape appears in more than one hunk or file in the change. → extract the shared shape, call it from both.
- **Feature Envy**: a method that reaches into another object's data more than its own. → move the method onto the data it envies.
- **Data Clumps**: the same few fields or params keep travelling together (a type wanting to be born). → bundle them into one type, pass that.
- **Primitive Obsession**: a primitive or string standing in for a domain concept that deserves its own type. → give the concept its own small type.
- **Repeated Switches**: the same `switch`/`if`-cascade on the same type recurs across the change. → replace with polymorphism, or one map both sites share.
- **Shotgun Surgery**: one logical change forces scattered edits across many files in the diff. → gather what changes together into one module.
- **Divergent Change**: one file or module is edited for several unrelated reasons. → split so each module changes for one reason.
- **Speculative Generality**: abstraction, parameters, or hooks added for needs the spec doesn't have. → delete it; inline back until a real need shows.
- **Message Chains**: long `a.b().c().d()` navigation the caller shouldn't depend on. → hide the walk behind one method on the first object.
- **Middle Man**: a class or function that mostly just delegates onward. → cut it, call the real target direct.
- **Refused Bequest**: a subclass or implementer that ignores or overrides most of what it inherits. → drop the inheritance, use composition.

### 4. Spawn the sub-agents in parallel

Every prompt carries the diff command, commit list, scope, and relevant untracked-file paths from step 1, and this output rule: "Report findings only: no praise, no summary of the diff. For each finding give the file and hunk, what is wrong, why it matters, and the fix you would make. Mark each finding **hard** or **judgement call**. If you find nothing, say so."

**Standards sub-agent**, additionally:

- The standards sources from step 3, plus the smell baseline pasted in full (the sub-agent has no other access to it).
- The brief: "Report (a) every place the diff violates a documented standard, ADR, or glossary term, citing the file and the rule; and (b) any baseline smell, naming it and quoting the hunk. Documented breaches can be hard; baseline smells are always judgement calls, and a documented repo standard overrides the baseline. Skip anything tooling enforces."

**Spec sub-agent**, additionally:

- The spec path or contents, or the agreed requirements, from step 2.
- The brief: "Report (a) requirements the spec asked for that are missing or partial; (b) behaviour in the diff that wasn't asked for (scope creep); (c) requirements that are implemented but don't do what the spec describes. Quote the spec line for each finding."

**Correctness sub-agent**, additionally:

- The brief: "Read the changed code and enough of its callers to judge it. Report (a) bugs: inputs or states that produce a wrong result, a crash, or corrupted data, such as unhandled empty and boundary values, error paths that swallow or mishandle the failure, operations that break when run twice or concurrently, and resources left open; (b) unvalidated input that crosses a trust boundary; (c) tests that could not catch the change failing: a test that passes with the implementation deleted, asserts on mocks of internal collaborators, or recomputes its expected value the way the code does; and changed behaviour with no test at all. For each bug, name the concrete input or sequence that triggers it. A bug you can trigger is hard; a suspicion you could not confirm by reading is a judgement call."

### 5. Aggregate

Present the reports under `## Standards`, `## Spec`, and `## Correctness` headings, verbatim or lightly cleaned. Keep them separate: merging or reranking across axes is what the separation exists to prevent.

End with a one-line summary: findings per axis, split into hard and judgement call, and the worst issue within each axis.
