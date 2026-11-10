---
name: improve-codebase-architecture
description: Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick.
disable-model-invocation: true
---

# Improve Codebase Architecture

Surface architectural friction and propose **deepening opportunities**: refactors that turn shallow modules into deep ones. The aim is testability and AI-navigability.

Two vocabularies run through everything this skill writes:

- Invoke the `codebase-design` skill for the architecture vocabulary (**module**, **interface**, **depth**, **seam**, **adapter**, **leverage**, **locality**) and its principles (the deletion test, "the interface is the test surface", the two-adapter rule). Use those terms exactly in every suggestion.
- The domain language in `GLOSSARY.md` gives names to good seams, and ADRs in `docs/adr/` record decisions this skill takes as settled.

## Process

### 1. Explore

**Scope before you scan.** Deepening a module pays off by making future changes to it easier, so weight the parts of the codebase that change most:

- If the user named a direction (a module, a subsystem, a pain point), take it.
- Otherwise, walk back a good stretch of the commit history (`git log --oneline`) to find the hot spots, the files and areas that keep coming up, and start there. If the changes are scattered with no clear hot spot, widen the net.

Read `GLOSSARY.md` and the ADRs in the area first.

Then dispatch a sub-agent with a fresh context window to walk the scoped area and report candidates, each with the files involved and the evidence. Brief it to explore organically and note where it meets friction:

- Where does understanding one concept require bouncing between many small modules?
- Where are modules **shallow**, with an interface nearly as complex as the implementation?
- Where have pure functions been extracted just for testability, while the real bugs hide in how they're called (no **locality**)?
- Where do tightly coupled modules leak across their seams?
- Which parts are untested, or hard to test through their current interface?

Have it apply the **deletion test** to anything it suspects is shallow: would deleting it concentrate complexity, or just move it? "Concentrates" is the signal. Check the candidates it returns against the source before reporting them.

### 2. Present candidates as an HTML report

Write a self-contained HTML file to the OS temp directory so nothing lands in the repo: `<tmpdir>/architecture-review-<timestamp>.html`, resolving the temp dir from `$TMPDIR`, then `/tmp`, or `%TEMP%` on Windows. Open it for the user (`xdg-open` on Linux, `open` on macOS, `start` on Windows) and tell them the absolute path.

For each candidate the report establishes:

- the files and modules involved
- the problem: why the current shape causes friction
- the solution: what would change, in plain English
- the wins, in terms of locality, leverage, and how tests improve
- a before/after diagram of the shallowness and the deepening
- a recommendation strength: `Strong`, `Worth exploring`, or `Speculative`

It ends with a top recommendation: which candidate to tackle first and why. [HTML-REPORT.md](HTML-REPORT.md) owns the layout: the scaffold, the card, the diagram patterns, and the tone.

Name domain concepts with `GLOSSARY.md` terms and architecture with `codebase-design` terms. If `GLOSSARY.md` defines "Order", write "the Order intake module", in place of a class name like `FooBarHandler` or "the Order service".

**ADR conflicts**: surface a candidate that contradicts an existing ADR only when the friction is real enough to warrant revisiting the ADR, and mark it in the card (_"contradicts ADR-0007, but worth reopening because…"_).

The report stops at candidates; interfaces come in step 3. After the file is written, ask the user: "Which of these would you like to explore?"

### 3. Grilling loop

Once the user picks a candidate, invoke the `grilling` skill to walk the decision tree with them: constraints, dependencies, the shape of the deepened module, what sits behind the seam, what tests survive.

Record side effects as decisions settle, invoking `glossary` for domain-language changes and `adr` for decision records:

- **A deepened module named after a concept that isn't in `GLOSSARY.md`**: add the term.
- **A fuzzy term sharpened during the conversation**: update `GLOSSARY.md` right there.
- **The user rejects the candidate for a reason a future review would need**: offer an ADR, framed as _"Want me to record this as an ADR so future architecture reviews don't re-suggest it?"_ Skip the offer for passing reasons ("not worth it right now") and self-evident ones.
- **The user wants to explore alternative interfaces**: invoke `codebase-design` and use its design-it-twice pattern.
