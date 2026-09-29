## What it does

`setup-khanra17-skills` configures a repository for the engineering skills. It records:

- Where issues live: GitHub, local Markdown, or another tracker described by the user.
- The repository's label names for the four canonical triage states, when `triage` is installed.
- How skills should find and consume glossaries and ADRs.
- Project-specific `AGENTS.md` guidance and relevant verification context, adapted to the actual stack.

After exploring the repository, it shows drafts for approval, updates the root `AGENTS.md`, and writes the relevant files under `docs/agents/`.

## When to reach for it

Run `/setup-khanra17-skills` once before the first engineering workflow in a repository. Run it again to change configuration or prepare references or a delivery board. You can request a single section, such as commit conventions or reference collections, without redoing the rest.

Productivity skills do not require this setup.

## Common questions

**Will the generated AGENTS.md have a consistent format?**

Yes. New files use a project introduction followed by Constraints, Working safely, Verification, Task guidance, and Agent skills, omitting empty sections. The [authoring reference](../../skills/engineering/setup-khanra17-skills/agent-instructions.md) defines what belongs in each section and what must stay out. A short writing pointer makes [unslop](../productivity/unslop.md) the default for human-facing prose. Existing instructions are edited in place; reorganizing them is a proposal, not an automatic rewrite.

Setup verifies the stack and tools rather than copying TypeScript rules into PHP or Kotlin projects. It keeps concrete constraints and conditional pointers, not generic advice, file inventories, duplicated glossaries, or a history of failures. It does not invent performance budgets, install analyzers, or grant production access.

**Will it create lots of instruction files?**

No. It reuses existing documentation. Scoped instructions need a genuinely different local rule, and a separate verification guide is created only when the detail warrants one. You approve the proposed files first. Full setup includes this guidance; targeted configuration runs do not rewrite it. Later lessons remain subject to [reflect](../productivity/reflect.md)'s approval process.

**Which tracker should I choose?**

GitHub is the default when the remote points to GitHub. Local Markdown stores specs and tickets under `.scratch/`. For another tracker, describe the workflow and the skill records it as repository-specific guidance.

**Will it preserve this repository's issue conventions?**

Yes. For GitHub, it records applicable issue-form requirements, extra required labels, and existing label-source/sync paths in the tracker guide. These supplement the spec and ticket formats rather than replacing them.

**How are commit conventions chosen?**


**Do I need a GitHub Project?**



**Does setup configure pull-request triage?**

No. This library's triage workflow handles issues only.

**When does it ask about triage labels?**

Only when the `triage` skill is installed beside setup or appears in the available skills. Otherwise it omits the label section and file.

**Will it install an MCP server and clone repositories on every setup run?**





**Does setup create `GLOSSARY.md` or an ADR directory?**

No. It writes the consumer guide in `docs/agents/domain.md`. [Glossary](./glossary.md) and [adr](./adr.md) create their own files lazily when there is something to record.

**How does it choose single-context or multi-context docs?**

Single-context is the default. It offers a multi-context `GLOSSARY-MAP.md` layout only when the repository shows real monorepo signals.

## It's working if

- `AGENTS.md` contains verified project guidance in a consistent structure and points to the relevant guides.
- Its rules capture consequential constraints rather than obvious advice, duplicated code facts, or speculative policies.
- The tracker guide contains commands or instructions that match the chosen tracker.
- Triage labels are included only when triage is installed.
- A collection marked ready has a working connection, verified source revisions and versions, and checked index coverage.
- Existing surrounding `AGENTS.md` content is preserved.
- Later engineering skills can use the configuration without asking where issues or domain docs live.
