## What it does

`reference-codebases` investigates how established projects address a problem to help decide what is worth doing, why, and how. It uses Codebase Memory MCP to navigate reference collections, then reads code, tests, and the documentation behind design or policy choices.

You get a source-linked explanation in the conversation unless you ask for a document.

## When to reach for it

- Find ideas and question whether a proposed feature is necessary.
- Find implementation techniques for an agreed plan.
- Check how projects use a library, alongside its current official guidance.
- Look for useful lessons after building something.

Invoke `/reference-codebases` when outside examples would help. Use [research](./research.md) for broader reading, [teach](../productivity/teach.md) for lessons, or [code-review](./code-review.md) for a Standards-and-Spec review.

## Common questions

**Can it challenge the idea I started with?**

Yes. Asking how to force users onto the latest version might lead to investigating compatibility policies, grace periods, update prompts, or security cutoffs. The useful answer could be that you only need mandatory updates in specific circumstances. It distinguishes practices found in the examples from evidence of an industry-wide norm.

**Will it replace our plan with another project's architecture?**

No. It investigates within an agreed direction and explains evidence for reconsidering it. Changes still need your approval. Another project's complexity is useful only when the constraints that justify it apply here.

**What is a collection?**

A group of repositories chosen for something you want to study. Laravel applications, Filament projects, and cross-language offline-sync implementations could be separate, overlapping collections.

Setup suggests `~/.reference-codebases/<collection>/`; you choose the names and location outside the working project. Each collection is indexed as a whole. Suitable existing collections can be shared without inspecting other consuming projects or their configuration.

**Do I need project configuration?**

No. The skill calls MCP's `list_projects` and chooses relevant reference indexes. Locations come from MCP; investigation instructions stay in the skill.

**What if suitable references are not indexed yet?**

Use the optional section of [setup-khanra17-skills](./setup-khanra17-skills.md), or let this skill load the preparation guide when needed. You approve connection changes, sources, storage, and indexing. Clones are shallow by default and treated as disposable reference copies. If whole-collection indexing cannot be verified, setup reports that rather than silently choosing a different layout.

**How are repositories chosen?**

At least 500 stars, then adoption relative to the ecosystem and inspected evidence: relevant implementation, failure handling, tests, dependency versions, maintenance, and licensing. Current-practice collections exclude abandoned projects and obsolete API examples. A requested count does not justify weaker selections.

**What stops old examples being taught as current practice?**

The agent checks source versions against your target and consults official documentation and migration guidance. A fresh index does not make old code current. Updating sources needs approval; an incompatible target gets a separate collection rather than repurposing a shared one.

## It's working if

- You discover useful options, including reasons to reconsider the original proposal.
- Claims link to inspected source revisions and distinguish evidence from inference.
- Advice fits your constraints and library versions.
- The result helps your decision without importing unnecessary architecture.
