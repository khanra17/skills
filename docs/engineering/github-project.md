## What it does

`github-project` maintains an explicitly configured GitHub Project's membership, delivery status, and fields. It adds a delivery view to the existing issue workflow rather than replacing triage, specs, tickets, or implementation.

The shared operating rules live in the skill. `docs/agents/github-project.md` holds the Project URL and repository-specific choices: item scope, field mapping, completion criteria, defaults, and automation ownership.

## When to reach for it

Use it for medium-to-high-complexity work where you need to see commitments, active work, and delivery across issues. Ask it to update or reconcile a board directly, or let the configured tracker and [implement](./implement.md) flows invoke it.

For hobby projects, GitHub Issues alone remain sufficient. Installing the skill does not enable board management; [setup](./setup-khanra17-skills.md) is opt-in.

## Common questions

**What board does setup recommend?**

Backlog → Next → In progress → Done. Add Awaiting acceptance only when implementation regularly waits on a real client approval or delivery check. Existing boards keep their conventions unless you agree to changes.

Use a delivery board and planning table. Add a roadmap when meaningful dates exist, not to manufacture a schedule for every ticket. There are no mandatory estimates, sprints, or one-task limits.

**How is Next different from ready-for-implementation?**

Readiness means an issue is sufficiently specified. Next means you have selected it for near-term work. Triage does not automatically make that commitment or set a priority.

**Does a commit move the issue to Done?**

Only if the configured completion criteria are satisfied. If Done means deployed or accepted by the client, passing tests and creating a commit are not sufficient evidence. Board updates do not close issues by themselves.

**Where do priority, milestones, and blockers live?**

Each has one home. Setup reuses an organization issue field for shared priority where available, otherwise a Project field. Single-repository deliverables normally use milestones. Hierarchy and blocking use native sub-issues and issue dependencies. Labels are not mirrored into fields by default.

**What happens to cancelled or reopened work?**

Not-planned closures follow the configured archive policy and stay out of delivered totals. Reopened work returns to its actual stage and active visibility. Generic closed-to-Done automation must not misrepresent cancellation or unverified delivery.

**How does this connect to the existing skills?**

The GitHub tracker guide calls it after batches of issue publication or lifecycle changes. Implementation supplies start and finish outcomes. The operator respects existing automation and verifies the affected items after the batch. Wayfinder decision tickets remain distinguishable from implementation deliverables.

**Does it change my board structure or automate everything?**

Not during routine work. Field definitions, views, access, and automation changes need approval. Setup checks existing automation and backfills old issues when needed; enabling auto-add alone does not import every existing matching issue. Unsupported steps remain pending rather than being reported as complete.

## It's working if

- Issues appear on the intended board without duplicate PR cards.
- Ready, selected, active, and delivered work remain distinct.
- Cancellation does not inflate delivery totals.
- Status reflects verified outcomes and your definition of Done.
- Native automation and agent updates do not compete.
- Projects remain absent from workflows that do not need them.
