---
name: github-project
description: Maintain a configured GitHub Project's membership, delivery status, and fields. Use after issue publication or lifecycle changes, when implementation starts or finishes, or for explicit board updates and reconciliation.
---

# GitHub Project

Read `docs/agents/github-project.md` for the selected Project, field mapping, completion criteria, item scope, and automation ownership. Without it, skip automatic board work; for an explicit request to configure a board, direct the user to `/setup-khanra17-skills`.

This skill maintains the delivery view. The invoking workflow still owns the issue content, triage, implementation, and approvals. Do not infer new scope, priorities, dates, or issue state from a board update.

## Establish the change

Use the affected issues and outcome supplied by the active workflow. For an explicit board request, use the requested scope. Inspect current membership, issue state and close reason, relevant fields, dependencies, and configured automation before deciding what needs changing.

Resolve field and option IDs from GitHub. An issue ID and its Project item ID are different; organization issue fields and Project-local fields have different owners. Use the installed CLI or API for the actual field kind. Do not store those lookup results in project configuration or copy metadata from another board.

## Keep the meanings separate

Map these roles to the configured Status options:

| Role | Meaning |
| --- | --- |
| Backlog | Work not selected for the near term |
| Next | Work the user has selected to do soon |
| In progress | Work actually started |
| Awaiting acceptance, if configured | Implementation finished but a real approval or delivery check remains |
| Done | The configured completion criteria are met |

- **Readiness is not commitment.** `ready-for-implementation` says the issue is specified. It does not move it to Next or assign a priority. Starting an explicitly requested issue can move it directly to In progress.
- **Blocked is a relationship, not a second workflow.** Preserve native issue dependencies and the current delivery stage. Report external blockers to the invoking workflow for issue notes; do not invent a Blocked column or another copy of the dependency list.
- **Closed is not necessarily delivered.** A not-planned closure follows the configured cancellation/archive policy and stays out of delivered totals. A reopened item must leave Done or the archive when it is active again; use its actual stage, asking when that is unclear.
- **Completion needs evidence.** A local commit or passing tests does not prove deployment or client acceptance. Leave the item at the appropriate stage until the configured criterion is met. Moving a card never closes its issue by itself.
- **One work item, one card.** Prefer the issue with linked PR information rather than adding its PR as another deliverable. Respect configured exceptions. Keep wayfinder decision tickets distinguishable from implementation work and outside delivery totals unless explicitly included.

Priority, release grouping, and dates each have one configured home. Preserve those values unless the user or the approved plan supplies a change. Do not mirror labels into fields, manufacture dates, or impose a one-task WIP limit on parallel agents.

## Apply and verify

Ensure in-scope issues belong to the selected Project before editing their item fields. Preserve an existing item's values; new items use configured defaults, normally Backlog. Skip work that functioning native automation already performs. If automation owns a transition but has not produced the expected result, report the gap rather than silently adding a competing rule.

Apply the requested batch, then read back the affected items and verify membership and expected values. Report fields that failed or remain pending; do not claim the entire update succeeded after a partial result.

Field definitions, views, access, and automation changes need separate approval. Routine issue publication or implementation is not permission to redesign the board.
