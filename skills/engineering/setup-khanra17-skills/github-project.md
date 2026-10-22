# GitHub Project setup

Use for Section F. Prepare the configuration and remote-change proposal here; apply them only after the user's approval in step 3. Existing boards keep their conventions unless a change is agreed.

## Choose the board and its job

Confirm the Project URL and which repository issues belong to it. A new board is opt-in, useful for medium-to-high-complexity delivery, not a requirement for using GitHub Issues. Check access to the Project and its repositories separately; a client who can see the board may still be unable to see private issues.

Inspect existing fields, views, native workflows, and relevant Actions. Establish what automation already owns before proposing agent-managed updates. Include a one-time backfill when adopting existing issues: auto-add does not initially import every matching old issue.

## Propose the smallest useful delivery view

For a new board, recommend:

- **Status:** Backlog, Next, In progress, Done. Add Awaiting acceptance only for a real client approval or delivery handoff, not the tests inside an implementation session.
- **Priority:** one home. Reuse an organization issue field where available, otherwise a Project field. If labels already own priority, agree whether to keep them or migrate before adding a competing field. If none exists, suggest High, Normal, Low with Normal as the default. Keep existing values rather than imposing these names.
- **Deliverable:** use milestones in a single repository. For a multi-repository delivery, agree on a shared grouping only if repository milestones cannot express it.
- **Structure:** native sub-issues and dependencies, displayed rather than copied into custom fields.
- **Dates:** actual commitments on significant deliverables, not guessed start and target dates for every ticket.

Offer a delivery board and a planning table ordered by priority and grouped by deliverable. Add a roadmap when there are meaningful dates. Keep decision tickets, including wayfinder work, distinguishable from implementation and out of delivered-feature totals. Prefer issues as cards with linked PR information, not duplicate issue and PR cards.

No default estimates, sprints, velocity, Decision Needed field, mirrored labels, or fixed WIP limit. Reuse the existing triage vocabulary; it describes specification readiness, not which work is Next.

## Agree on completion and automation

Ask what Done means here: implemented and verified, deployed, or accepted by the client. Identify who or what supplies evidence for the final transition.

Propose native auto-add and archiving where they fit. Check each automation against the agreed semantics:

- A generic closed-to-Done rule also risks counting not-planned closures as delivery. Use a supported reason-specific rule if available; otherwise leave that transition agent-managed. Archive cancelled work and exclude it from delivered views.
- Reopening must restore the item's real stage and active visibility. Do not assume a built-in reopen transition exists.
- PR merge proves neither deployment nor client acceptance. Match any merge-based transition to the chosen completion criterion.

For each transition, choose native automation, an existing Action, or the agent as its owner. Avoid duplicate writers. Do not add custom Actions just to make setup look complete; propose one only for an agreed recurring gap. Record manual or pending work honestly.

## Record and apply

Draft `docs/agents/github-project.md` with this project's choices only:

- Project URL and item scope
- Status-role mapping and new-item defaults
- Meaning of Done and any acceptance stage
- Field names, their owners (issue or Project), and agreed defaults
- Deliverable/date conventions and decision-ticket treatment
- Automation ownership, cancellation/reopen policy, and any pending setup

Resolve IDs, permissions, and current values from GitHub during operations. Reusable operating instructions live in the `github-project` skill, not this configuration.

Show field, view, automation, access, and backfill changes alongside the draft. After approval, apply what the available tools support and verify the resulting configuration and affected items. If a step requires the UI or additional permissions, report it as pending rather than silently substituting a different workflow. Never change repository visibility to make a board accessible.
