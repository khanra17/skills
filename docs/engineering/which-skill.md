## What it does

`which-skill` is the router for this library. You describe where you are, and it points to the skill or flow that fits.

Its main route is:

```text
grill-with-docs → optional prototype → to-spec → to-tickets → implement → code-review
```

It also explains the triage, diagnosis, architecture, and wayfinder on-ramps, plus how to choose between continuing, clearing, handing off, using a subagent, and compacting at a phase boundary.

## When to reach for it

Type `/which-skill` whenever you do not remember which skill comes next or two skills look similar.

It recommends a route. It does not automatically run user-invoked skills for you.

## Common questions

**Where should a new feature start?**

Usually with [grill-with-docs](./grill-with-docs.md) in a project, or [grill-me](../productivity/grill-me.md) when you want an interview without project documentation.

**When do I need a prototype?**

When a design question cannot be settled by conversation, such as how a state model feels when exercised or which visual layout works.

**When do I need wayfinder?**

When the destination is clear but the decisions needed to reach it cannot fit in one session. A well-scoped feature does not need a map.

**What helps with stateful behavior?**

Use [codebase-design](./codebase-design.md) when event ordering or state combinations affect correctness. It helps make the rules explicit without requiring a state-machine library. Use [prototype](./prototype.md) if those rules need a runnable exploration, then implement and verify them through the agreed interfaces.

**How do I prepare project-specific agent instructions?**

Use [setup-khanra17-skills](./setup-khanra17-skills.md). It inspects the stack and proposes a consistently structured `AGENTS.md`, reusing existing guides and adding scoped guidance only where useful. Use [writing-for-agents](../productivity/writing-for-agents.md) for the authoring discipline and [reflect](../productivity/reflect.md) for evidence-backed improvements later.

**What keeps commit messages consistent?**

[Git-commit](./git-commit.md) supplies the fixed Gitmoji + Conventional Commits mapping and coherent commit boundaries. Implement calls it after review; you can also ask it to prepare a commit or squash message directly. Setup records repository-specific overrides.

**What if I use GitHub Projects?**

[Github-project](./github-project.md) maintains an opted-in delivery board alongside the existing issue workflow. It runs after issue changes and implementation outcomes, or on a direct board-management request. Use setup to configure it for larger projects; hobby projects do not need it.

**What if I want to learn how established projects solve a problem?**

Use [reference-codebases](./reference-codebases.md) to find ideas, investigate practices, or improve an implementation. It can also reveal that the proposed feature is unnecessary. It discovers relevant reference indexes through MCP; project configuration is optional. Use [code-review](./code-review.md) to check your own standards and requirements.

**What if I want to learn something rather than build it?**

Use [teach](../productivity/teach.md). It can explain a concept in the conversation or provide ongoing lessons and practice in a learning workspace. Use [wait-what](../productivity/wait-what.md) when you only want the last message explained again.

**What if the wording or presentation is the problem?**

[Unslop](../productivity/unslop.md) applies automatically to human-facing writing; invoke it directly when you want selected text rewritten. Use [wait-what](../productivity/wait-what.md) to get one confusing message explained again. Use [i-have-adhd](../productivity/i-have-adhd.md) for clear steps and useful progress reminders throughout the current session, until you turn that mode off.

**What if I need to write documentation?**

Use [technical-writing](./technical-writing.md) for human-facing technical material, including docs, READMEs, RFCs, issue descriptions, and PR descriptions. The agent can invoke it automatically for that writing work, while the active workflow keeps control of its format, required detail, and approvals. It calls [unslop](../productivity/unslop.md) for wording. Use [writing-for-agents](../productivity/writing-for-agents.md) for agent instructions.

**What if the session revealed something we should do differently next time?**

Use [reflect](../productivity/reflect.md) to review the evidence and propose changes to the appropriate instructions or documentation. It checks whether the guidance already exists, uses [writing-for-agents](../productivity/writing-for-agents.md) when drafting or applying agent-instruction changes, and waits for approval before editing. Use [handoff](../productivity/handoff.md) instead when you need to carry unfinished work into another session.

**What is a phase boundary?**

The point where one chunk of work ends and another begins. That is when you decide whether to continue, clear context, write a handoff, delegate a bounded task, or compact the session.

**Does the router inspect every installed skill?**

No. It is a maintained map of the skills in this repository. Update it when this library's skills or flows change.

## It's working if

- It names a specific next skill and explains why it fits.
- It distinguishes planning tickets from implementation tickets.
- It keeps connected planning work in one context until the right boundary.
- It sends large uncertain efforts to wayfinder and small settled work to implementation.
- Its recommendations match the current `SKILL.md` files.
