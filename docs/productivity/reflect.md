# reflect

## What it does

`reflect` reviews how a session went and proposes lessons worth keeping in your instructions or documentation. It looks for corrections, repeated friction, and approaches that worked, then checks whether existing guidance already covers them.

The question it answers is: "Did this session reveal anything that should change how we work next time?" Sometimes the answer is no, and it says so.

## When to reach for it

Type `/reflect` after a session with useful corrections or workflow discoveries. It reviews the current conversation, or a transcript you give it.

For example, suppose an agent kept changing intentional behavior without saying what was wrong with it. Reflect might propose a rule requiring a concrete failure before recommending a workflow change. If your instructions already say that clearly, it reports that the agent ignored them and adds nothing.

Use [handoff](./handoff.md) to carry unfinished work into another session. Reflect is about how future work is done, not the status of this task.

## Common questions

**Will it edit my skills straight away?**

No. It shows the evidence, the problem, the proposed change, and where it would go, and waits for your approval of each. After the approved edits it stops so you can review the diff; it does not stage or commit.

**Where do lessons end up?**

A personal preference goes in your preference document, a project fact in project documentation, and a reusable workflow lesson in the relevant skill. Temporary workarounds are left out.

**What if a test would enforce the lesson better than a rule?**

It recommends the test, lint rule, or other check as a proposal for you to take up.

**How does it write the changes?**

For skills, `AGENTS.md`, and other agent-facing instructions, it uses [writing-for-agents](./writing-for-agents.md) for the wording.

## It's working if

- Each proposed change points to a specific incident in the session.
- An instruction that already exists is reported as ignored, not duplicated.
- No file changes before you approve it.
