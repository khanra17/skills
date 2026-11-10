---
name: which-skill
description: Ask which skill or flow fits your situation. A router over the skills in this repo.
disable-model-invocation: true
---

# Which Skill

The user wants to know which skill or flow fits where they are. If they have not said what they are trying to do, ask. Then name the next skill to run, say why it fits, and say what follows it. User-invoked skills are theirs to type; you can only point at them.

Answer from the map below. A **flow** is a path through the skills. Most work runs along one **main flow**, and three **on-ramps** merge onto it. Everything else is standalone, or a vocabulary layer that runs underneath.

## The main flow: idea → ship

1. **`/grill-with-docs`** sharpens the idea by interview and records what it learns in `GLOSSARY.md` and ADRs. Outside a repo, `/grill-me` runs the same interview and records nothing.
2. **Does a question need a runnable answer** (state, business logic, a UI you have to see)? Build a **`/prototype`**. A small one is built in this session. One that would crowd the planning context is forked: `/handoff` out, build it in a fresh session, and bring the verdict back to this thread.
3. **Is this a multi-session build?**
   - **Yes** → **`/to-spec`** turns the thread into a spec, then **`/to-tickets`** splits it into tracer-bullet tickets, each declaring the tickets that block it. Run **`/implement`** once per ticket, in a fresh context each time: a ticket is self-contained, so the previous one's context is disposable. Any ticket whose blockers are done can start.
   - **No** → **`/implement`** right here, in the same context window.

`/implement` builds through `/tdd` (one red-green slice at a time), checks the feature on every surface it touches, runs `/code-review` (Standards, Spec, and Correctness) on the diff, fixes what the review finds, and commits through `/git-commit`. The commit finishes the ticket: on GitHub its `Closes #N` footer closes the issue when the commit reaches the default branch; on a local tracker the ticket file is marked `done`.

`/tdd` and `/code-review` also work alone: `/tdd` to build one behaviour test-first without a spec, `/code-review` to review a branch or PR against a fixed point.

### Context hygiene

Keep steps 1–3 in one context window, up to and including `/to-tickets`, so the grilling, spec, and tickets all build on the same thinking. Each `/implement` then starts fresh from its ticket.

The limit is the **smart zone**: the early part of the context window, where the model still reasons sharply (roughly the first 150k tokens on current frontier models). If a session nears its edge before `/to-tickets`, compact at the nearest phase boundary and carry on (see Phase boundaries).

## On-ramps

Starting situations that generate work, then merge onto the main flow.

- **Bugs and requests piling up** → **`/triage`**. It evaluates incoming requests, including your own half-formed ones, and marks the fully specified ones `ready-for-implementation` for `/implement`. Rejected requests close as not planned. Tickets from `/to-tickets` are already ready and skip triage.
- **Something's broken and the cause isn't obvious** → **`/diagnosing-bugs`**: the intermittent flake, the regression between two known-good states, the bug a first fix didn't cure. It builds a tight feedback loop (one command that goes red on this bug) before it theorises, then fixes with a regression test. When no test seam can hold the bug, it says so and points at `/improve-codebase-architecture`.
- **A huge, foggy effort, too big for one session** → **`/wayfinder`**. It charts a shared map of decision tickets on the issue tracker and resolves them one per session. It produces decisions, not deliverables. When the map clears, merge onto the main flow at `/to-spec`, which collapses the linked decisions into a buildable plan. It is slower and denser than `/grill-with-docs`, so keep it for the idea one session cannot hold.

## Codebase health

- **`/improve-codebase-architecture`** surveys the codebase for deepening opportunities and reports candidates. Picking one produces an idea to take into the main flow at `/grill-with-docs`. `/codebase-design` (below) is the vocabulary the chosen one is designed in.

## Vocabulary and decisions

Model-invoked; the agent reaches for them inside other skills, and you can type them.

- **`/glossary`** sharpens the project's domain language: challenges a fuzzy term, resolves an overloaded word, and maintains `GLOSSARY.md` and `GLOSSARY-MAP.md`.
- **`/adr`** records a significant architectural decision or supersedes an existing ADR.
- **`/codebase-design`** is the deep-module vocabulary (module, interface, depth, seam, adapter, leverage, locality) for designing a module's shape, plus explicit state models where event ordering affects correctness.

## Phase boundaries

A **phase** is a chunk of work inside a session: the grilling, the implementation, the QA. At the boundary between two phases there are five options:

- **Continue**: stay put. Costs nothing, loses nothing.
- **Clear** (`/clear`, or your harness's new-session command): empty the window, when nothing here matters to what's next.
- **`/handoff`**: write a portable markdown file to open a new session against. Only for a new harness, a new directory, a colleague, or forking a side task mid-phase.
- **Subagent**: send a tightly scoped task to its own window and get a report back.
- **Compact** (`/compact`): compress this context into a summary and carry on from it. The default when none of the others fits.

Read [PHASE-BOUNDARIES.md](PHASE-BOUNDARIES.md) for the ordered questions that pick between them. Decide at a boundary; mid-phase, continue or split the remaining work into subagents.

## Standalone

- **`/grill-me`**: the `/grill-with-docs` interview with no files written. For plans with no repo under them.
- **`/grilling`**: the interview primitive both of those run, also used inside `/triage`, `/wayfinder` and `/improve-codebase-architecture`. Type it only when you want the interview with no wrapper.
- **`/prototype`**: throwaway code that answers one design question, as a clickable logic demo or as switchable UI variants. It records the verdict and evidence, then removes itself.
- **`/research`**: answers a question from primary sources with citations, in a background agent where the harness has one. It also covers how established projects solve a problem in their code. Reports go to a temporary file, or to the issue as a comment when the research belongs to one.
- **`/wizard`**: generates an interactive bash script for steps only a human can take (provisioning, credentials, third-party dashboards, one-off cutovers). The agent reaches for it when it hits such a step.
- **`/wait-what`**: re-pitches the agent's last message with the context you were missing, in plain English and glossary terms.
- **`/teach`**: explains a concept in the conversation, or runs lessons over several sessions in a learning workspace with records of what you have learned.
- **`/unslop`**: plain-writing guidance for human-facing prose. The agent loads it when a task is mainly writing; type it to rewrite a specific text.
- **`/technical-writing`**: accuracy and structure for docs, READMEs, RFCs, and issue or PR descriptions. It defers wording to `/unslop` and format to whatever workflow called it.
- **`/writing-for-agents`**: the reference for documents agents consume: skills, `AGENTS.md`, pointed-at docs.
- **`/git-commit`**: coherent commit boundaries and one fixed emoji per Conventional Commit type. `/implement` calls it; type it for a commit or squash message.
- **`/github-project`**: keeps an opted-in GitHub Project's membership and delivery fields current. The tracker guide and `/implement` call it; type it to update or reconcile the board.
- **`/reflect`**: reviews a session for lasting lessons and proposes instruction or documentation changes for your approval. `/handoff` carries unfinished work forward; `/reflect` changes how future sessions work.

## Project setup

**`/setup-khanra17-skills`**: run once per repo before the first engineering flow. It configures the issue tracker, triage labels, domain-doc layout, and commit conventions, and drafts a stack-aware `AGENTS.md`. A GitHub Project is opt-in. Any one section can be rerun later.
