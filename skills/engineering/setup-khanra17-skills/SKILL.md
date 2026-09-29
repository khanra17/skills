---
name: setup-khanra17-skills
description: "Set up project-specific agent instructions and engineering workflow configuration, including optional Projects and reference collections."
disable-model-invocation: true
---

# Setup khanra17's Skills

Scaffold the per-repo configuration that the engineering skills assume:

- **Issue tracker**: where issues live (GitHub by default; local markdown is also supported out of the box)
- **Triage labels**: the strings used for the four canonical triage states
- **Domain docs**: where `GLOSSARY.md` and ADRs live, and the consumer rules for reading them
- **Commit conventions**: repository choices for `/git-commit`
- **GitHub Project** (opt-in): delivery-board configuration for `/github-project`
- **Project guidance**: concise, stack-aware `AGENTS.md` and relevant verification context

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

For targeted setup, run only the requested sections and their approval/write steps. Leave other configuration untouched.

## Process

### 1. Explore

Look at the current repo to understand its starting state. Read whatever exists; don't assume:

- `git remote -v` and `.git/config`: is this a GitHub repo? Which one?
- Root and scoped `AGENTS.md` files: what guidance exists, and is there already an `## Agent skills` section?
- `GLOSSARY.md` and `GLOSSARY-MAP.md` at the repo root
- `docs/adr/` and any `src/*/docs/adr/` directories
- `docs/agents/`: does this skill's prior output already exist?
- `.scratch/`: a sign that a local-markdown issue tracker convention is already in use
- Is the `triage` skill installed? (a `triage` skill folder alongside this one, or `triage` in your available skills.) This decides whether Section B runs at all.
- Are `git-commit` and `github-project` installed alongside setup or available in the session? This gates Sections E and F.
- Existing commit conventions, templates, validators, and recent commit subjects.
- For GitHub: issue forms, additional required labels, any label-source/sync files, and an existing Project configuration.
- Monorepo signals: a `pnpm-workspace.yaml`, a `workspaces` field in `package.json`, or a populated `packages/*` with its own `src/`. These are present only in a genuinely large multi-package repo; their absence means single-context, which is almost every repo.

### 2. Present findings and ask

Summarise what's present and what's missing. Then take the sections in order. One section, one answer, then the next.

Lead each section with the recommended answer so the user can accept it in a word. Give a one-line explainer only when the choice genuinely branches; skip the section entirely when exploration already settled it (Section B when `triage` isn't installed, Section C when there's no monorepo).

**Section A: Issue tracker.**

> Explainer: The "issue tracker" is where issues live for this repo. Skills like `to-tickets`, `triage`, and `to-spec` read from and write to it. They need to know whether to call `gh issue create`, write a markdown file under `.scratch/`, or follow some other workflow you describe. Pick the place you actually track work for this repo.

Default posture: these skills were designed for GitHub. If a `git remote` points at GitHub, propose that. Otherwise (or if the user prefers), offer:

- **GitHub**: issues live in the repo's GitHub Issues (uses the `gh` CLI)
- **Local markdown**: issues live as files under `.scratch/<feature>/` in this repo (good for solo projects or repos without a remote)
- **Other** (Jira, Linear, etc.): ask the user to describe the workflow in one paragraph; the skill will record it as freeform prose

Record the choice in `docs/agents/issue-tracker.md`. For GitHub, also retain applicable issue-form requirements, extra label conventions, and existing label-source/sync paths. These supplement the spec and ticket formats; they do not replace them or introduce a new label taxonomy.

**Section B: Triage label vocabulary.** Skip this section entirely if the `triage` skill isn't installed (exploration told you), since an uninstalled skill needs no labels.

If it is installed, ask exactly one question:

> Do you want to keep the default triage labels? (recommended: **yes**)

The four canonical states are `needs-triage`, `needs-info`, `ready-for-implementation`, and `suspended` (not pursuing). Default labels use these names. On **yes**, write them as-is. Only if the user says no, usually because their tracker already uses other names (e.g. `bug:triage` for `needs-triage`), collect the overrides so `triage` applies existing labels instead of creating duplicates.

**Section C: Domain docs.** Default to **single-context** (one `GLOSSARY.md` + `docs/adr/` at the repo root). This fits almost every repo; write it without asking.

Offer **multi-context** (a root `GLOSSARY-MAP.md` pointing to per-context `GLOSSARY.md` files) only when exploration found monorepo signals. Then confirm which layout they want.



**Section E: Commit conventions.** Run when `git-commit` is installed. Ask:

> Use the standard Gitmoji + Conventional Commits convention? (recommended: **yes**, unless this repository has a different required convention)

The standard format and fixed type-to-emoji mapping live in [git-commit](../git-commit/SKILL.md). On yes, record that choice in `docs/agents/git-commit.md` without copying the mapping. Collect only repository differences: scope restrictions, convention overrides, and paths to existing templates or validators. Use exploration to propose these rather than asking the user to enumerate discoverable settings. Reconcile any validator conflict before adopting a convention; do not install hooks or dependencies automatically. The chosen format also applies to final squash messages if the repo uses squash merges.

**Section F: GitHub Project (opt-in).** Offer when the tracker is GitHub and `github-project` is installed, or the user explicitly requests Project setup. Recommend leaving it off for small or hobby projects; use it when delivery tracking warrants a board. A linked board alone does not authorize managing it.

If chosen, read [github-project.md](./github-project.md) to propose the board setup and draft `docs/agents/github-project.md`. Include its remote changes in step 3; apply them only after approval.

**Section G: Project agent instructions.** Include in full setup, or run on its own when requested. Read [agent-instructions.md](./agent-instructions.md) for the output structure, stack-specific discovery, and content boundaries. Draft project guidance from verified facts and agreed constraints, preserving existing instructions. Include scoped or verification references only where they earn their own file. Other targeted setup runs update their configuration pointers without rewriting project guidance.

### 3. Confirm and edit

Show drafts for the sections being configured:

- The relevant `## Agent skills` block in `AGENTS.md` (see step 4)
- The tracker and domain guides, and triage labels only when Section B ran
- Commit choices only when Section E ran
- Project configuration and proposed remote changes only when Section F ran
- Root instructions and any scoped or verification guides only when Section G ran

Let the user edit and approve the drafts before file writes or remote changes.

### 4. Write

**Pick the file to edit:**

- If `AGENTS.md` exists, apply only the approved edits in place.
- If it does not exist, create the `AGENTS.md` proposed and approved in step 3.

Use Section G's structure when authoring project guidance; a targeted configuration-only run needs only its relevant pointers. If an `## Agent skills` block already exists, update it rather than appending a duplicate. Preserve surrounding user instructions and write any scoped or verification files only as approved.

The block:

```markdown
## Agent skills

### Issue tracker

[one-line summary of where issues are tracked]. See `docs/agents/issue-tracker.md`.

### Triage labels

[one-line summary of the label vocabulary]. See `docs/agents/triage-labels.md`.

### Domain docs

[one-line summary of layout: "single-context" or "multi-context"]. See `docs/agents/domain.md`.
```

Include the `### Triage labels` sub-block, and write `docs/agents/triage-labels.md`, only when `triage` is installed and Section B ran. When it isn't, both are omitted.

When Section E runs, write the approved `docs/agents/git-commit.md` and add a `### Git commits` pointer: use `git-commit` for commits and squash messages; repository choices are in that file.

When Section F runs, apply the approved Project plan and write `docs/agents/github-project.md`. Add a `### GitHub Project` pointer: use `github-project` for board operations; project choices are in that file. Ensure the tracker guide includes the conditional Project dispatch from [issue-tracker-github.md](./issue-tracker-github.md), preserving its existing conventions. Issues-only repositories need no Project configuration or pointer. For targeted setup, update only the relevant subsections.

Then write the docs files using the seed templates in this skill folder as a starting point:

- [issue-tracker-github.md](./issue-tracker-github.md): GitHub issue tracker
- [issue-tracker-local.md](./issue-tracker-local.md): local-markdown issue tracker
- [triage-labels.md](./triage-labels.md): label mapping (only if `triage` is installed)
- [domain.md](./domain.md): domain doc consumer rules + layout

For "other" issue trackers, write `docs/agents/issue-tracker.md` from scratch using the user's description.

### 5. Done

Summarize what is configured and any pending remote work. Mention that `docs/agents/*.md` can be edited directly, or setup rerun for the sections they want to change.
