# Project agent instructions

Create or revise the consuming project's `AGENTS.md`, not a copy of this library's instructions. Call the Skill tool with "writing-for-agents" for authoring discipline. This guide fixes the output structure and content boundaries; it does not supply universal coding rules.

## Establish the facts

Read existing root and scoped instructions, manifests, build and analysis configuration, CI, relevant architecture docs, and enough source to verify the system's shape. Use the conversation for established preferences and known failures.

Ask only for decisions the repository cannot establish: protected environments, product commitments, permitted verification access, or conflicting conventions. Distinguish an observed practice from an approved requirement. Setup does not authorize starting services, reading private production data, changing compiler settings, or installing tools.

## Consistent output structure

For a new file, use the following order and headings. Replace the placeholders with verified project-specific content. Omit sections with no useful content; never leave placeholders or add generic rules to fill a heading.

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

For an existing file, map additions into its equivalent sections. Propose structural changes when they improve navigation; do not overwrite user text or reformat the whole document just to impose these headings. Keep the approved `## Agent skills` block in one place.

Include a `### Writing` pointer under that block: "Use `unslop` when writing for humans." Keep the writing rules in the skill.

### Content boundaries

| Section | Include | Leave out |
| --- | --- | --- |
| Opening | Purpose, major execution paths, non-obvious ownership between applications | Marketing, a README rewrite, file trees and exhaustive architecture inventories |
| Constraints | Concrete compatibility or product commitments, with their scope | Slogans such as "performance without compromise", speculative policies, duplicated ADRs or glossary entries |
| Working safely | The actual resources at risk and the safe alternative | Copied paths, secrets, blanket permission to access live data, a chronological failure diary |
| Verification | Verified commands or pointers, relevant environments and limits | A getting-started tutorial, invented commands, claims that unexecuted checks passed |
| Task guidance | Stable, high-value pointers with a clear trigger | Catalogs of every file or skill, vague "read the docs" pointers, instructions to load every reference for every task |
| Agent skills | Configuration pointers for the selected setup sections | Copied skill bodies, disabled workflow configuration, a second source for shared rules |

An instruction earns its place when it changes a consequential decision the agent would otherwise get wrong. Record the distilled rule, not the incident that taught it. Known high-impact hazards may be documented before a failure occurs. Prefer an existing test, analyzer, or other mechanical check over another copy of a rule; propose new enforcement separately.

## Adapt to the project, not the example

- **Types:** inspect the real language and checking setup. TypeScript strictness, Kotlin null-safety, and PHP static analysis require different instructions. Record meaningful exceptions and traps; do not transplant `any` bans into another language or silently enable stricter checking across legacy code.
- **Dependencies:** reuse existing capabilities first. Record approved dependency constraints, not a universal "always install a popular package" or "never write it yourself" rule. Infrastructure risk, compatibility, maintenance, and licensing matter more than popularity alone.
- **Performance:** record an agreed operation, workload, environment, and measurement. Do not invent a universal latency limit or demand database-side processing for every computation.
- **Errors:** distinguish invalid configuration and broken invariants from expected user errors and recoverable failures. Record project-specific handling and diagnostic conventions, not "crash on every error" or "log everywhere".
- **Safety:** identify development versus live state and safe process ownership. Prefer seeded or sanitized fixtures. Production access, copying sensitive data, destructive operations, and public evidence uploads require appropriate authorization; a reference project's permission does not transfer here.

These are selection questions for the author, not five mandatory sections to paste into the generated file.

## Verification context and scoped guidance

Identify the project's actual clients, entry points, adapters, and shared contracts. Record only non-obvious coverage relationships, such as a mobile client with separate navigation or several adapters implementing the same interface. Do not invent a multi-platform checklist for a single-surface project.

Reuse existing verification documentation. When details need a separate home and none exists, propose `docs/agents/verification.md` with project facts only: applicable surfaces, verified runner commands and environment prerequisites, safe fixtures, test accounts, and relevant browser/device access constraints. Keep brief instructions in the root file when that is enough. The reusable verification procedure belongs in `implement`.

Create nested `AGENTS.md` files only where directory-local instructions materially differ. Use the applicable parts of the same structure, keep shared rules at the root, and link scoped guidance with a clear task trigger. Do not create a file for every package or assume a directory-local file covers work in another application.

## Review before writing

Present the proposed files, unresolved choices, and any changes to existing instructions for approval. Check each rule against evidence or an explicit user decision, each pointer against its target, and each command against the repository's configuration. Distinguish source inspection from commands actually run.

Prune duplicated, obvious, transient, and unsupported instructions. Keep necessary warnings inline; move task-specific detail behind conditional pointers. There is no magic line-count threshold and no requirement to generate every possible reference file.

Future lessons go through the existing Reflect approval process. Do not make this file self-modifying, copy a transcript into it, or repeat a rule merely because a previous agent ignored it.
