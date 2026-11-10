# improve-codebase-architecture

## What it does

`improve-codebase-architecture` surveys a codebase for places where shallow modules could become deep ones. It uses the vocabulary from [codebase-design](./codebase-design.md), reads the glossary and the ADRs in the area, and weights its scan toward the parts of the code that change most.

The result is a visual HTML report in the operating system's temporary directory. Each candidate shows the files involved, the problem, the proposed change, what improves, a before-and-after diagram, and how strongly it is recommended. The survey changes no code. After you pick a candidate, it interviews you through the design.

## When to reach for it

Type `/improve-codebase-architecture` for routine upkeep, before a large feature, or after [diagnosing-bugs](./diagnosing-bugs.md) reports that an area has no seam to test at. Name a module or pain point to scope the scan.

Use [codebase-design](./codebase-design.md) directly when you already know which module you want to redesign.

## Common questions

**Where does the report go?**

To a new `architecture-review-<timestamp>.html` in the temporary directory, opened for you. Nothing is added to the repository.

**What happens after I pick a candidate?**

The skill runs [grilling](../productivity/grilling.md) on it: constraints, dependencies, the shape of the deepened module, which tests survive. Along the way it may update the glossary, offer an ADR, or run design-it-twice to compare interfaces. The idea that comes out goes into the main flow like any other.

**What if a candidate contradicts an ADR?**

It appears only when the friction is strong enough to justify reopening that decision, and the card says which ADR it contradicts.

**Will it fix an old, tangled codebase for me?**

It finds and ranks candidates. Doing the refactors is separate work, one candidate at a time.

## It's working if

- The report opens in your browser, and every candidate has a before-and-after diagram.
- Candidates sit in code that changed recently, or in the area you named.
- The report names domain concepts with your glossary's terms.
- It stops after the report and asks which candidate to explore.
