# Project agent instructions

Create or revise the consuming project's `AGENTS.md`. Invoke the `writing-for-agents` skill for authoring discipline. This guide fixes the output structure and what belongs in each section.

## Establish the facts

Read existing root and scoped instructions, manifests, build and analysis configuration, CI, relevant architecture docs, and enough source to verify the system's shape. Use the conversation for established preferences and known failures.

Ask only for decisions the repository cannot establish: protected environments, product commitments, permitted verification access, or conflicting conventions. Mark each rule as an observed practice or an approved requirement. Setup reads and writes files; starting services, reading production data, changing compiler settings, and installing tools each need the user's explicit go-ahead.

## Output structure

For a new file, use this order and these headings. Fill each section with verified, project-specific content and omit any section that has none.

```markdown
# <Project name>

<What the project does and the architectural facts needed to work on it.>

## Constraints

<Product or architectural commitments that materially affect changes.>

## Working safely

<Protected resources, isolated development environments, and consequential operational traps.>

## Verification

<The project's verification entry points, or a conditional pointer to its verification guide.>

## Task guidance

<When changing a particular area, read the relevant source or guide.>

## Agent skills

<The applicable configuration pointers assembled by setup.>
```

For an existing file, map additions into its equivalent sections and leave the user's text and layout as they are. Propose a restructure separately when it would improve navigation. Keep the `## Agent skills` block in one place.

### What goes in each section

| Section | Content |
| --- | --- |
| Opening | Purpose, major execution paths, and ownership between applications where it is not obvious |
| Constraints | Concrete compatibility or product commitments, each with its scope |
| Working safely | The resources at risk and the safe alternative for each |
| Verification | Commands you verified, the environments they need, and their limits |
| Task guidance | Pointers with a clear trigger: "when changing X, read Y" |
| Agent skills | The configuration pointers for the setup sections that ran |

A rule earns its place when it changes a consequential decision the agent would otherwise get wrong. That test excludes what the agent can read from the repo in one lookup (file trees, script names), what an ADR or glossary entry already says, and advice that holds for any project. Record the distilled rule and leave out the incident that taught it. Where a test, analyzer, or other mechanical check could enforce a rule, propose that check in place of the prose.

## Derive rules from this project

Types, dependencies, performance, errors, and safety are questions to ask of the repository. Record a rule only where the answer is specific to it:

- **Types:** the language's actual checking setup, with its meaningful exceptions and traps.
- **Dependencies:** approved dependency constraints, and existing capabilities to reuse first.
- **Performance:** an agreed operation, workload, environment, and measurement.
- **Errors:** how this project separates broken invariants from expected user errors and recoverable failures, and its diagnostic conventions.
- **Safety:** which state is development and which is live, who owns which processes, and which fixtures are safe. Production access, copying sensitive data, destructive operations, and public evidence uploads need authorization given for this project.

## Verification context and scoped guidance

Identify the project's actual clients, entry points, adapters, and shared contracts. Record the coverage relationships that are not obvious, such as a mobile client with separate navigation or several adapters implementing one interface.

Reuse existing verification documentation. When the details need their own home and none exists, propose `docs/agents/verification.md` holding project facts: applicable surfaces, verified runner commands and environment prerequisites, safe fixtures, test accounts, and browser or device access constraints. Brief instructions stay in the root file. The verification procedure itself lives in the `implement` skill.

Create a nested `AGENTS.md` only where a directory's instructions materially differ from the root. Use the applicable parts of the same structure, keep shared rules at the root, and link scoped guidance with a clear task trigger.

## Review before writing

Present the proposed files, unresolved choices, and any changes to existing instructions for approval. Check each rule against evidence or an explicit user decision, each pointer against its target, and each command against the repository's configuration. Say which commands you ran and which you only read.

Prune duplicated, obvious, transient, and unsupported instructions. Keep necessary warnings inline and move task-specific detail behind conditional pointers.

Later lessons reach this file through the `reflect` skill's approval process.
