## What it does

`improve-codebase-architecture` surveys a codebase for opportunities to turn shallow modules into deep ones. It uses the vocabulary from [codebase-design](./codebase-design.md), reads the project glossary and relevant ADRs, and biases an unscoped scan toward recently changed areas.

It writes a visual HTML report to the operating system's temporary directory. Each candidate includes the files, problem, proposed deepening, locality and leverage benefits, before-and-after diagrams, and a recommendation strength. No production code changes during the survey.

## When to reach for it

Type `/improve-codebase-architecture` when you want to find architectural friction rather than fix a named defect.

Use it for routine upkeep, before a large feature, or after diagnosis reveals that no useful testing seam exists. Use [codebase-design](./codebase-design.md) directly when you already know which module you want to design.

## Common questions

**Where does the report go?**

It is written to a fresh `architecture-review-<timestamp>.html` file in the operating system's temporary directory, then opened for you. Nothing is added to the repository.

**What makes a candidate worth showing?**

The skill looks for shallow interfaces, leaked seams, scattered knowledge, weak test surfaces, and missing locality. It applies the deletion test before recommending a deepening.

**What happens after I choose a candidate?**

The skill calls [grilling](../productivity/grilling.md) to work through constraints, dependencies, the new module shape, and surviving tests. It may use [glossary](./glossary.md), [adr](./adr.md), or the design-it-twice pattern from `codebase-design` as decisions emerge.

**What if a candidate conflicts with an ADR?**

It is shown only when the friction is strong enough to justify reopening the decision, and the conflict is marked clearly.

## It's working if

- The scan follows the requested area or recent codebase hot spots.
- Every candidate explains depth, locality, leverage, and test impact.
- The report uses the project's domain words rather than invented synonyms.
- It stops after the report and asks which candidate you want to explore.
- Rejected candidates produce an ADR offer only when the reason is durable and load-bearing.
