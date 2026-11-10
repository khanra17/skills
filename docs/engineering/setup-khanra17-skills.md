# setup-khanra17-skills

## What it does

`setup-khanra17-skills` configures a repository for the engineering skills. It explores the repo, shows you drafts, and after you approve them updates the root `AGENTS.md` and writes guides under `docs/agents/`:

- `issue-tracker.md`: where issues live (GitHub, local Markdown under `.scratch/`, or another tracker you describe) and how to publish, fetch, block, and finish tickets there.
- `triage-labels.md`: your label names for the two triage categories and four states, when `triage` is installed.
- `domain.md`: how skills find and use the glossary and ADRs.
- `git-commit.md`: where this repository differs from the default commit convention, when `git-commit` is installed.
- `github-project.md`: the configuration of a delivery board, if you opt in to one.

It also drafts project-specific `AGENTS.md` guidance from what it can verify about the stack.

## When to reach for it

Run `/setup-khanra17-skills` once per repository, before the first engineering workflow. Run it again to change the configuration; name one section (for example "just the commit conventions") to redo only that.

Productivity skills need no setup.

## Common questions

**Which tracker should I choose?**

GitHub is the default when the remote points to GitHub. Local Markdown keeps specs and tickets under `.scratch/` and suits solo projects or repos without a remote. For anything else, describe the workflow in a paragraph and the skill records it as the tracker guide.

**What does the generated `AGENTS.md` look like?**

A project introduction, then Constraints, Working safely, Verification, Task guidance, and Agent skills. A section with nothing verified to say is left out. An existing `AGENTS.md` is edited in place; reorganizing it is proposed separately. The [authoring reference](../../skills/engineering/setup-khanra17-skills/agent-instructions.md) defines what belongs in each section.

**What happens to my existing labels and issue forms?**

They stay. The tracker guide records your issue-form requirements and extra labels, and the triage-label mapping points the canonical roles at the labels you already use.

**Does it create `GLOSSARY.md` or an ADR directory?**

It writes only the consumer guide. [glossary](./glossary.md) and [adr](./adr.md) create their files when there is a first term or decision to record.

**Do I need a GitHub Project?**

Issues alone are enough for small projects. The board is opt-in, for work where you need to see commitments and delivery across many issues. See [github-project](./github-project.md).

## It's working if

- `AGENTS.md` has an `## Agent skills` block, and every pointer in it resolves to a file under `docs/agents/`.
- `/to-spec` publishes to your tracker without asking where issues live.
- Every label named in `triage-labels.md` exists in the tracker.
- The commands in the generated Verification section run as written.
