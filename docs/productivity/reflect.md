## What it does

`reflect` reviews how a session went and proposes lessons worth keeping in instructions or documentation. It looks for corrections, repeated friction, and useful approaches, then checks whether existing guidance already covers them.

It is not a general journal or a code review. The question is: "Did this session reveal anything that should change how we work next time?"

## When to reach for it

Type `/reflect` after a session with useful corrections or workflow discoveries. It can review the current conversation or a transcript you supply. You do not need to run it after every task.

For example, suppose an agent repeatedly changes intentional behavior without explaining what is wrong. Reflect could propose requiring a concrete failure example before recommending workflow changes. But if your instructions already clearly require that, it should identify a failure to follow them rather than add the same rule again.

Use [handoff](./handoff.md) to carry unfinished work into another session. Reflect is about lasting improvements to how the work is done, not preserving current task status.

## Common questions

**Will it edit my skills immediately?**

No. It first shows the evidence, the problem, the proposed change, and where it belongs. You approve the changes and destinations before it writes anything. After approved edits, it stops for your diff review rather than staging or committing automatically.

**Does every lesson go into a skill?**

No. A personal preference belongs in your agreed preference document. A project fact belongs in project documentation. A reusable workflow lesson may belong in a skill. Temporary workarounds and observations already covered by clear instructions may need no saved change.

**What if a test would solve the problem better?**

It can recommend a test, lint rule, or other mechanical check instead of another prose rule. That remains a proposal. It does not automatically implement the check or create a backlog issue.

**Does it search my other conversations?**

No. It uses the current conversation or a transcript you supply for review. If context is missing, it states the limit rather than assuming it has reviewed the whole history.

**Does it need several agents or project setup?**

No. It reviews ordinary sessions directly and can delegate bounded read-only reviews when a long or complicated session warrants them. It has no fixed model selection or engineering setup requirement.

**How does it use writing-for-agents?**

When drafting or applying changes to skills, AGENTS.md, or other agent-facing instructions, Reflect invokes [writing-for-agents](./writing-for-agents.md) for authoring guidance. Reflect still decides what lesson is supported and where it belongs, and waits for your approval before editing. Reviewing a session or finding nothing to change does not require this authoring step. Both skills are included in the productivity installation.

**What if it finds nothing worth changing?**

That is a valid result. It should say so rather than manufacture findings to fill a report.

## It's working if

- Each proposed change has a concrete incident behind it and a clear effect on future behavior.
- It distinguishes missing guidance from an agent ignoring existing guidance.
- Project details stay out of reusable skills.
- You choose which changes to apply and where they are saved.
- No files, preferences, or tracker items change before approval.
