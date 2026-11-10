# Issue tracker: GitHub

Issues and specs for this repo live as GitHub issues. Use the `gh` CLI for all operations.

## Conventions

- **Create an issue**: `gh issue create --title "..." --body "..."`. Use a heredoc for multi-line bodies.
- **Read an issue**: `gh issue view <number> --json number,title,body,labels,comments`.
- **List issues**: `gh issue list --state open --json number,title,body,labels,comments --jq '[.[] | {number, title, body, labels: [.labels[].name], comments: [.comments[].body]}]'` with appropriate `--label` and `--state` filters.
- **Count open blockers**: `gh api repos/<owner>/<repo>/issues/<n> --jq .issue_dependencies_summary.blocked_by` (open blockers only; 0 means startable). `gh issue view <n> --json blockedBy` also lists closed blockers, so filter it: `--jq '[.blockedBy.nodes[] | select(.state == "OPEN")] | length'`.
- **Comment on an issue**: `gh issue comment <number> --body "..."`
- **Apply / remove labels**: `gh issue edit <number> --add-label "..."` / `--remove-label "..."`
- **Finish a ticket**: put `Closes #<number>` in the footer of the commit that completes it. GitHub closes the issue when that commit reaches the default branch. If the ticket is the last open sub-issue of its parent (`gh api repos/<owner>/<repo>/issues/<parent> --jq .sub_issues_summary` shows `total` one more than `completed`), add a second footer line `Closes #<parent>`.
- **Close completed work by hand** (work that landed without a closing footer, or was already implemented): `gh issue comment <number> --body "..."`, then `gh issue close <number> --reason completed`.
- **Close rejected or cancelled work**: `gh issue comment <number> --body "..."`, then `gh issue close <number> --reason "not planned"`.
- Always comment before closing: on an already-closed issue, `gh issue close --comment` drops the comment and still exits 0.

Infer the repo from `git remote -v`; `gh` does this automatically when run inside a clone.

File issues only into the user's own repo. In a fork, `gh` can default to the upstream parent, so before the first `gh issue create` of a session, check the target with `gh repo view --json nameWithOwner` and confirm it with the user if it is not their repo.

## When a skill says "publish to the issue tracker"

Create a GitHub issue.

## When a skill says "fetch the relevant ticket"

Read it as in **Read an issue** above. An issue with open sub-issues is a container: the work is in its sub-issues. A ticket is startable when it is open and has no open blockers (see **Count open blockers**).

## When a skill says "finish the ticket"

Follow **Finish a ticket** above.

## GitHub Project (when configured)

If `docs/agents/github-project.md` exists, invoke the `github-project` skill after a batch of issue publications or lifecycle changes. Pass the affected issues and actual outcome, including close reasons or reopening. It handles membership and delivery fields without changing the issue content, triage labels, or relationships. With no Project configuration, skip board work.

## Wayfinding operations

Used by `/wayfinder`. The **map** is a single issue with **child** issues as tickets.

- **Map**: a single issue labelled `wayfinder:map`, holding the map body. `gh issue create --label wayfinder:map`. Before the first map, create any missing `wayfinder:map`, `wayfinder:research`, `wayfinder:prototype`, `wayfinder:grilling`, and `wayfinder:task` labels with `gh label create`.
- **Child ticket**: an issue linked to the map as a GitHub sub-issue (`gh issue edit <PARENT> --repo <owner>/<repo> --add-sub-issue <CHILD>`), one call per child in ticket order, because a comma-separated list loses the order the frontier reads. Where sub-issues aren't enabled, add the child to a task list in the map body and put `Part of #<map>` at the top of the child body. Labels: `wayfinder:<type>` (`research`/`prototype`/`grilling`/`task`). Once claimed, the ticket is assigned to the driving dev.
- **Blocking**: GitHub's **native issue dependencies**, the canonical, UI-visible representation. Add an edge with `gh issue edit <CHILD> --repo <owner>/<repo> --add-blocked-by <BLOCKER>`. GitHub reports `issue_dependencies_summary.blocked_by` (open blockers only, the live gate). Where dependencies aren't available, fall back to a `Blocked by: #<n>, #<n>` line at the top of the child body. A ticket is unblocked when every blocker is closed.
- **Frontier query**: list the map's open children (`gh api "repos/<owner>/<repo>/issues/<MAP>/sub_issues?per_page=100"`, or the map's task list where sub-issues aren't enabled), drop any with an open blocker (see **Count open blockers**, or an open issue in the `Blocked by` line) or an assignee; first in map order wins.
- **Claim**: `gh issue edit <n> --add-assignee @me`, the session's first write.
- **Resolve**: `gh issue comment <n> --body "<answer>"`, then `gh issue close <n>`, then append a context pointer (gist + link) to the map's Decisions so far.
