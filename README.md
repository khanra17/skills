# Skills For Real Engineers

[![skills.sh](https://skills.sh/b/khanra17/skills)](https://skills.sh/khanra17/skills)

The agent skills I use every day to do real engineering, not vibe coding.

Adapted from [Matt Pocock's skills](https://github.com/mattpocock/skills), customized by khanra17. See [LICENSE](./LICENSE) for the MIT terms and copyright notices.

Developing real applications is hard. Approaches like GSD, BMAD, and Spec-Kit try to help by owning the process. In doing so they take away your control, and a bug in the process becomes hard to fix.

These skills are small, easy to adapt, and composable. They are written for current frontier models and rest on long-standing engineering practice. Edit them until they fit how you work.

## Installation

Use [skills.sh](https://skills.sh/khanra17/skills) with pi, Codex, Antigravity, or another supported agent. The installer lets you choose which skills to install and for which agents.

### 1. Get the skills

**Productivity: install globally.**

```bash
npx skills@latest add khanra17/skills --global --skill grill-me grilling handoff reflect teach unslop wait-what writing-for-agents
```

For a project-specific copy, run the same command from the project without `--global`.

**Engineering: install per project.** Run these from the project directory:

```bash
npx skills@latest add khanra17/skills/skills/engineering --skill '*'
npx skills@latest add khanra17/skills --skill grilling unslop writing-for-agents
```

The first command installs the engineering set, including `setup-khanra17-skills` and `triage`. The second installs the productivity skills the engineering flows call: `grilling` for interviews, `unslop` for human-facing writing, and `writing-for-agents` for project instructions. With both, the engineering flows work without a global installation.

The installed files are yours to edit. Update when you want with `npx skills update`.

### 2. Run `/setup-khanra17-skills`

Run it once per repo for the engineering skills. Productivity skills need no setup. It will:

- Ask which issue tracker you use: GitHub, local files, or another tracker you describe
- Ask whether to keep the default triage labels (`/triage` works through labels)
- Write the guide that tells skills where the glossary and ADRs live, confirming the layout for multi-context repos
- Draft stack-aware `AGENTS.md` guidance for your approval
- Confirm the Gitmoji + Conventional Commits convention and record where your repository differs
- Offer a GitHub Project for delivery tracking, which small projects can skip

### 3. Start with `/which-skill`

Describe what you are trying to do and it names the skill or flow to use.

## Workflow

Most work travels one route, from an idea to a closed ticket. The other skills are ways onto that route, or run inside it.

```mermaid
%%{init: {"flowchart": {"nodeSpacing": 24, "rankSpacing": 34, "padding": 10}}}%%
flowchart TB
    setup["<b>/setup-khanra17-skills</b><br/>once per repo"]:::step --> idea([You have an idea]):::start
    idea --> grill["<b>/grill-with-docs</b><br/>interview that keeps<br/>a glossary and ADRs"]:::skill
    arch["<b>/improve-codebase-<br/>architecture</b><br/>upkeep survey"]:::ramp -- pick a candidate --> grill

    grill --> q1{{"Need to see<br/>it running?"}}:::ask
    q1 -- yes --> proto["<b>/prototype</b><br/>throwaway logic or UI"]:::skill
    proto --> q2
    q1 -- no --> q2{{"Fits in one<br/>session?"}}:::ask

    q2 -- no --> spec["<b>/to-spec</b><br/>conversation → spec"]:::skill
    way["<b>/wayfinder</b><br/>too big for one session:<br/>map the decisions first"]:::ramp --> spec
    spec --> tickets["<b>/to-tickets</b><br/>vertical slices<br/>with blockers"]:::skill
    tickets --> impl
    q2 -- yes --> impl
    tri["<b>/triage</b><br/>issues piling up"]:::ramp --> impl

    subgraph impl ["/implement, per ticket"]
        direction TB
        tdd["<b>/tdd</b><br/>red, green, repeat"]:::skill --> verify["verify every<br/>surface touched"]:::step
        verify --> review["<b>/code-review</b><br/>standards, spec,<br/>correctness"]:::skill
        review --> commit["<b>/git-commit</b><br/>with Closes #N"]:::skill
    end

    impl --> done([Ticket closes when<br/>the commit lands]):::finish
    done -. next unblocked ticket .-> impl
    done -. a bug turns up .-> diag["<b>/diagnosing-bugs</b><br/>repro loop, then fix"]:::ramp
    diag --> fixed([Fixed, with a<br/>regression test]):::finish

    classDef start fill:#fff8c5,stroke:#9a6700,color:#3b2300
    classDef skill fill:#ddf4ff,stroke:#0969da,color:#0a3069
    classDef ramp fill:#ffe7d1,stroke:#bc4c00,color:#5c2200
    classDef ask fill:#fbefff,stroke:#8250df,color:#3e1f79
    classDef step fill:#f6f8fa,stroke:#57606a,color:#24292f
    classDef finish fill:#dafbe1,stroke:#1a7f37,color:#0f3d1e
    style impl fill:transparent,stroke:#4493f8,stroke-dasharray:5 4
```

Blue boxes are the main route. Orange boxes are the other ways in: each joins the route where its arrow lands. Purple boxes are the two decisions that shape the route.

Two links are left out of the picture to keep it readable:

- `/diagnosing-bugs` points you to `/improve-codebase-architecture` when a bug has no seam to test at.
- A prototype that would crowd the planning session is built in a fresh one, with `/handoff` carrying the question out and the verdict back.

**Running inside the route.** The agent reaches for these when the work calls for them, and you can type them too.

| Skill | Where it shows up |
| --- | --- |
| `grilling` | The interview inside `grill-with-docs`, `triage`, `wayfinder`, and architecture reviews |
| `glossary`, `adr` | Whenever a domain term or an architectural decision gets settled |
| `codebase-design` | When a module's shape is the question, in `tdd` and architecture work |
| `research` | When a decision waits on outside facts, including `wayfinder`'s research tickets |
| `technical-writing`, `unslop` | Docs, and issue or PR descriptions |
| `github-project` | When issues change and when `implement` starts and finishes, if you opted in to a board |
| `wizard` | When a step needs you: credentials, dashboards, cutovers |

**Any time.** These sit outside the route.

| Skill | Use it to |
| --- | --- |
| `which-skill` | Ask what to run next |
| `grill-me` | Get the interview with no repo and no files written |
| `handoff` | Move work to another session, harness, or person |
| `wait-what` | Have the last message explained again |
| `reflect` | Turn a session's lessons into instruction changes |
| `teach` | Learn a topic, in one answer or over many sessions |
| `writing-for-agents` | Write skills and `AGENTS.md` |

Every skill is linked in the [Reference](#reference) below.

## Why These Skills Exist

These skills address common failure modes with Claude Code, Codex, and other coding agents.

### #1: The Agent Didn't Do What I Want

> "No-one knows exactly what they want"
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**The Problem**: The most common failure mode in software development is misalignment. You think the dev knows what you want. Then you see what they built, and you realize they didn't understand you at all.

The same gap exists between you and an agent. The fix is a **grilling session**: the agent asks you detailed questions about what you're building until nothing is left assumed.

**The Fix** is to use:

- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) inside a project. It also records the terms and decisions you settle (see #2)
- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) for anything with no repo under it

Run one before you make a change, so you and the agent agree on it first.

### #2: The Agent Doesn't Speak The Project's Language

> With a ubiquitous language, conversations among developers and expressions of the code are all derived from the same domain model.
>
> Eric Evans, [Domain-Driven-Design](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

**The Problem**: At the start of a project, devs and the people they're building for (the domain experts) speak different languages.

Agents have it worse. They are dropped into a project and left to work out the jargon as they go, so they use 20 words where 1 would do, and name the same thing three ways across the code.

**The Fix** is a shared language: a glossary that defines the project's terms once.

<details>
<summary>
Example
</summary>

A project's `GLOSSARY.md` defines shared terms (see the [glossary docs](./docs/engineering/glossary.md)). In a course-management app, which description is easier to read?

- **BEFORE**: "There's a problem when a lesson inside a section of a course is made 'real' (i.e. given a spot in the file system)"
- **AFTER**: "There's a problem with the materialization cascade"

</details>

[`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) builds this as you go. It is a grilling session that also writes each term you settle into the glossary and records hard-to-explain decisions as ADRs.

> [!TIP]
> A shared language does more than shorten messages:
>
> - Variables, functions and files get named consistently
> - The codebase becomes easier for the agent to navigate
> - The agent spends fewer tokens thinking, because it has a concise word for each concept

### #3: The Code Doesn't Work

> "Always take small, deliberate steps. The rate of feedback is your speed limit. Never take on a task that’s too big."
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**The Problem**: You and the agent agree on what to build, and the result still doesn't work.

Look at your feedback loops. An agent that can't see how its code runs is working blind.

**The Fix**: Give it the usual feedback loops: static types, browser access, and automated tests.

- [`/tdd`](./skills/engineering/tdd/SKILL.md) works one red-green slice at a time: a failing test, then just enough code to pass it. It carries guidance on what makes a test worth keeping.
- [`/code-review`](./skills/engineering/code-review/SKILL.md) checks the finished change against your standards, the spec, and for bugs.
- [`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md) handles the hard failures: it builds a command that reproduces the bug before it forms any theory about the cause.

### #4: We Built A Ball Of Mud

> "Invest in the design of the system _every day_."
>
> Kent Beck, [Extreme Programming Explained](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)

> "The best modules are deep. They allow a lot of functionality to be accessed through a simple interface."
>
> John Ousterhout, [A Philosophy Of Software Design](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)

**The Problem**: Agents write code fast, so they also grow complexity fast. Most apps built with agents become hard to change sooner than a hand-written one would.

**The Fix** is to care about the design of the code at each step:

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) agrees the test seams before anything is built and writes them into the spec.
- [`/codebase-design`](./skills/engineering/codebase-design/SKILL.md) gives you and the agent one vocabulary for module design.
- [`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) surveys the codebase for shallow modules that could become deep ones and reports the candidates. I run it every few days. It finds and ranks; untangling an old codebase is still work you do one candidate at a time.

## Reference

Skills split on who can invoke them. **User-invoked** skills run only when you type them (e.g. `/grill-me`); their job is to orchestrate. **Model-invoked** skills can be typed by you or reached for by the agent when the task fits; they hold the reusable discipline. A user-invoked skill may invoke model-invoked skills, but never another user-invoked one.

### Engineering

Skills for daily code work.

**User-invoked**

- **[which-skill](./skills/engineering/which-skill/SKILL.md)**: Ask which skill or flow fits your situation. A router over the skills in this repo. [Docs](./docs/engineering/which-skill.md)
- **[setup-khanra17-skills](./skills/engineering/setup-khanra17-skills/SKILL.md)**: Configure a repo's issue tracker, triage labels, domain docs, and commit conventions, draft its `AGENTS.md`, and optionally set up a GitHub Project. [Docs](./docs/engineering/setup-khanra17-skills.md)
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**: A grilling session that also writes settled terms into `GLOSSARY.md` and records qualifying decisions as ADRs. [Docs](./docs/engineering/grill-with-docs.md)
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**: Turn the current conversation into a spec and publish it to the issue tracker. No interview; it synthesizes what you've already discussed. [Docs](./docs/engineering/to-spec.md)
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**: Break a plan, spec, or conversation into tracer-bullet tickets, each declaring the tickets that block it. [Docs](./docs/engineering/to-tickets.md)
- **[implement](./skills/engineering/implement/SKILL.md)**: Build a spec or ticket: test-first at the agreed seams, verified on every surface it touches, reviewed, committed, and the ticket finished. [Docs](./docs/engineering/implement.md)
- **[triage](./skills/engineering/triage/SKILL.md)**: Evaluate incoming issues and move them through triage states, ending in an implementation brief or a recorded rejection. [Docs](./docs/engineering/triage.md)
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**: Plan work too big for one session as a shared map of decision tickets on the issue tracker, resolved one at a time until the route is clear. [Docs](./docs/engineering/wayfinder.md)
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**: Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick. [Docs](./docs/engineering/improve-codebase-architecture.md)

**Model-invoked**

- **[tdd](./skills/engineering/tdd/SKILL.md)**: Test-driven development in red-green slices at agreed seams, leaving refactoring to review. [Docs](./docs/engineering/tdd.md)
- **[code-review](./skills/engineering/code-review/SKILL.md)**: Review changes since a fixed point on three separate axes: Standards, Spec, and Correctness, each in its own sub-agent. [Docs](./docs/engineering/code-review.md)
- **[git-commit](./skills/engineering/git-commit/SKILL.md)**: Make coherent commits with a fixed type-to-emoji convention, including squash messages. [Docs](./docs/engineering/git-commit.md)
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**: A diagnosis loop for bugs with no obvious cause: build a command that goes red on the bug, minimise, hypothesise, instrument, fix, regression-test. [Docs](./docs/engineering/diagnosing-bugs.md)
- **[prototype](./skills/engineering/prototype/SKILL.md)**: Build a throwaway logic or UI prototype to answer a design question. [Docs](./docs/engineering/prototype.md)
- **[research](./skills/engineering/research/SKILL.md)**: Answer a question from primary sources, including how established projects solve a problem, and return a cited report. [Docs](./docs/engineering/research.md)
- **[glossary](./skills/engineering/glossary/SKILL.md)**: Build and sharpen the project's domain language, maintaining `GLOSSARY.md` and `GLOSSARY-MAP.md`. [Docs](./docs/engineering/glossary.md)
- **[adr](./skills/engineering/adr/SKILL.md)**: Record significant architectural decisions as ADRs, and supersede them when they change. [Docs](./docs/engineering/adr.md)
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**: Vocabulary and principles for designing deep modules: a lot of behaviour behind a small interface, at a clean seam, testable through that interface. [Docs](./docs/engineering/codebase-design.md)
- **[technical-writing](./skills/engineering/technical-writing/SKILL.md)**: Write or review human-facing technical material, from guides and READMEs to issue and PR descriptions. [Docs](./docs/engineering/technical-writing.md)
- **[github-project](./skills/engineering/github-project/SKILL.md)**: Keep an opted-in GitHub Project's membership and delivery fields current. [Docs](./docs/engineering/github-project.md)
- **[wizard](./skills/engineering/wizard/SKILL.md)**: Generate an interactive bash script that walks a human through steps only they can perform: provisioning, credentials, third-party dashboards, one-off cutovers. [Docs](./docs/engineering/wizard.md)

### Productivity

General workflow tools, not code-specific.

**User-invoked**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**: Get relentlessly interviewed about a plan or design until every branch of the decision tree is resolved. [Docs](./docs/productivity/grill-me.md)
- **[handoff](./skills/productivity/handoff/SKILL.md)**: Write a handoff document so another agent or session can continue the work. [Docs](./docs/productivity/handoff.md)
- **[reflect](./skills/productivity/reflect/SKILL.md)**: Review a session for lasting lessons and propose instruction or documentation changes for your approval. [Docs](./docs/productivity/reflect.md)
- **[teach](./skills/productivity/teach/SKILL.md)**: Explain a concept plainly, or teach a topic over several sessions with lessons, practice, and a learning record. [Docs](./docs/productivity/teach.md)
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**: Have the agent re-explain its last message with the context you were missing, in plain English and glossary terms. [Docs](./docs/productivity/wait-what.md)

**Model-invoked**

- **[grilling](./skills/productivity/grilling/SKILL.md)**: The interview primitive behind `grill-me`, `grill-with-docs`, `triage`, `wayfinder` and `improve-codebase-architecture`: rounds of questions in dependency order, each with a recommended answer. [Docs](./docs/productivity/grilling.md)
- **[unslop](./skills/productivity/unslop/SKILL.md)**: Plain, natural writing for human-facing prose, and smallest-useful-edit rewrites of existing text. [Docs](./docs/productivity/unslop.md)
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**: The reference for documents agents consume: skills, `AGENTS.md`, and any doc reached by a pointer. [Docs](./docs/productivity/writing-for-agents.md)
