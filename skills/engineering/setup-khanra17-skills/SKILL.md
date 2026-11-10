---
name: setup-khanra17-skills
description: "Set up project-specific agent instructions and engineering workflow configuration, including an optional GitHub Project."
disable-model-invocation: true
---

# Setup khanra17's Skills

Scaffold the per-repo configuration that the engineering skills assume:

- **Issue tracker**: where issues live (GitHub by default; local markdown is also supported out of the box)
- **Triage labels**: the label strings for the triage categories and states
- **Domain docs**: where `GLOSSARY.md` and ADRs live, and the consumer rules for reading them
- **Commit conventions**: repository choices for `git-commit`
- **GitHub Project** (opt-in): delivery-board configuration for `github-project`
- **Project guidance**: concise, stack-aware `AGENTS.md` and relevant verification context

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

For targeted setup, run only the requested sections and their approval and write steps. Leave other configuration untouched.

## Process

### 1. Explore

Look at the current repo to understand its starting state. Read whatever exists:

- `git remote -v` and `.git/config`: is this a GitHub repo? Which one?
- Root and scoped `AGENTS.md` files: what guidance exists, and is there already an `## Agent skills` section?
- `GLOSSARY.md` and `GLOSSARY-MAP.md` at the repo root
- `docs/adr/` and any `src/*/docs/adr/` directories
- `docs/agents/`: does this skill's prior output already exist?
- `.scratch/`: a sign that a local-markdown issue tracker convention is already in use
- Which of `triage`, `git-commit`, and `github-project` are installed (a skill folder alongside this one, or the name in your available skills). This gates Sections B, D, and E.
- Existing commit conventions, templates, validators, and recent commit subjects.
- For GitHub: issue forms, additional required labels, any label-source or sync files, and an existing Project configuration.
- Monorepo signals: a `pnpm-workspace.yaml`, a `workspaces` field in `package.json`, or a populated `packages/*` with its own `src/`. Without one of these the repo is single-context, which is almost every repo.

### 2. Present findings and ask

Summarise what's present and what's missing. When the repo has no code or docs to read, ask what the project is first: repository naming and Section F depend on it. Then take the sections in order. One section, one answer, then the next.

Lead each section with the recommended answer so the user can accept it in a word. Give a one-line explainer only when the choice branches, and skip a section entirely when exploration already settled it (Section B when `triage` isn't installed, Section C when there's no monorepo).

**Section A: Issue tracker.**

> Explainer: The "issue tracker" is where issues live for this repo. Skills like `to-tickets`, `triage`, and `to-spec` read from and write to it. They need to know whether to call `gh issue create`, write a markdown file under `.scratch/`, or follow some other workflow you describe. Pick the place you actually track work for this repo.

These skills were designed for GitHub. If a `git remote` points at GitHub, propose that. Otherwise (or if the user prefers), offer:

- **GitHub**: issues live in the repo's GitHub Issues (uses the `gh` CLI). With no repository yet, suggest an owner and name from what the project is. On approval, run `git init -b main` and `gh repo create <owner>/<name> --private --source=. --remote=origin`, pushing nothing.
- **Local markdown**: issues live as files under `.scratch/<feature>/` in this repo (good for solo projects or repos without a remote)
- **Other** (Jira, Linear, etc.): ask the user to describe the workflow in one paragraph, and record it as freeform prose

Record the choice in `docs/agents/issue-tracker.md`. For GitHub, also retain applicable issue-form requirements, extra label conventions, and existing label-source or sync paths. These supplement the spec and ticket formats and leave the label taxonomy as it is.

**Section B: Triage labels.** Runs only when the `triage` skill is installed. Ask exactly one question:

> Do you want to keep the default triage labels? (recommended: **yes**)

The defaults are the canonical role names: the categories `bug` and `enhancement`, and the states `needs-triage`, `needs-info`, `ready-for-implementation`, and `suspended` (not pursuing; closed as not planned). On **yes**, write them as-is and, on GitHub, create any that are missing with `gh label create`. On no, usually because the tracker already uses other names (e.g. `bug:triage` for `needs-triage`), collect the overrides so `triage` applies the existing labels.

**Section C: Domain docs.** Default to **single-context** (one `GLOSSARY.md` + `docs/adr/` at the repo root) and write it without asking.

Offer **multi-context** (a root `GLOSSARY-MAP.md` pointing to per-context `GLOSSARY.md` files) only when exploration found monorepo signals. Then confirm which layout they want.

**Section D: Commit conventions.** Runs when `git-commit` is installed. Ask:

> Use the standard Gitmoji + Conventional Commits convention? (recommended: **yes**, unless this repository has a different required convention)

The standard format and fixed type-to-emoji mapping live in [git-commit](../git-commit/SKILL.md). On yes, record that choice in `docs/agents/git-commit.md` without copying the mapping. Collect only repository differences: scope restrictions, convention overrides, and paths to existing templates or validators. Propose these from what exploration found. Reconcile any validator conflict before adopting a convention. Installing hooks or dependencies is the user's call. The chosen format also applies to final squash messages if the repo uses squash merges.

**Section E: GitHub Project (opt-in).** Offer when the tracker is GitHub and `github-project` is installed, or the user explicitly requests Project setup. Recommend leaving it off for small or hobby projects; use it when delivery tracking warrants a board. Managing a board needs this opt-in even when one is already linked to the repo.

If chosen, read [github-project.md](./github-project.md) to propose the board setup and draft `docs/agents/github-project.md`. Include its remote changes in step 3; apply them only after approval.

**Section F: Project agent instructions.** Include in full setup, or run on its own when requested. Read [agent-instructions.md](./agent-instructions.md) for the output structure, stack-specific discovery, and what belongs in each section. Draft project guidance from verified facts and agreed constraints, preserving existing instructions. Other targeted setup runs update only their configuration pointers.

### 3. Confirm and edit

Show drafts for the sections being configured:

- The relevant `## Agent skills` block in `AGENTS.md` (see step 4)
- The tracker and domain guides, and triage labels when Section B ran
- Commit choices when Section D ran
- Project configuration and proposed remote changes when Section E ran
- Root instructions and any scoped or verification guides when Section F ran

Let the user edit and approve the drafts before file writes or remote changes.

### 4. Write

If `AGENTS.md` exists, apply the approved edits in place and preserve the surrounding user instructions. If it does not, create the `AGENTS.md` approved in step 3, using Section F's structure for project guidance.

Update an existing `## Agent skills` block; add one only when none exists. The block, with each subsection included only when its section ran:

```markdown
## Agent skills

### Issue tracker

[one-line summary of where issues are tracked]. See `docs/agents/issue-tracker.md`.

### Triage labels

[one-line summary of the label vocabulary]. See `docs/agents/triage-labels.md`.

### Domain docs

[one-line summary of layout: "single-context" or "multi-context"]. See `docs/agents/domain.md`.

### Git commits

Use the `git-commit` skill for commits and squash messages. Repository choices are in `docs/agents/git-commit.md`.

### GitHub Project

Use the `github-project` skill for board operations. Project choices are in `docs/agents/github-project.md`.
```

Then write the docs files, starting from the seed templates in this skill folder:

- [issue-tracker-github.md](./issue-tracker-github.md): GitHub issue tracker
- [issue-tracker-local.md](./issue-tracker-local.md): local-markdown issue tracker
- [triage-labels.md](./triage-labels.md): label mapping (Section B)
- [domain.md](./domain.md): domain doc consumer rules and layout

For an "other" tracker, write `docs/agents/issue-tracker.md` from the user's description. Cover every operation the seed templates cover: publish, fetch, label, block, finish a ticket, and the wayfinding operations.

When Section D ran, write the approved `docs/agents/git-commit.md`.

When Section E ran, apply the approved Project plan and write `docs/agents/github-project.md`. Make sure the tracker guide carries the "GitHub Project (when configured)" section from [issue-tracker-github.md](./issue-tracker-github.md), preserving its existing conventions.

### 5. Done

Summarize what is configured and any pending remote work. Mention that `docs/agents/*.md` can be edited directly, or setup rerun for the sections they want to change.
