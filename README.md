# Skills For Real Engineers

[![skills.sh](https://skills.sh/b/khanra17/skills)](https://skills.sh/khanra17/skills)

My agent skills that I use every day to do real engineering - not vibe coding.

Adapted from [Matt Pocock's skills](https://github.com/mattpocock/skills), customized by khanra17. See [LICENSE](./LICENSE) for the MIT terms and copyright notices.

Developing real applications is hard. Approaches like GSD, BMAD, and Spec-Kit try to help by owning the process. But while doing so, they take away your control and make bugs in the process hard to resolve.

These skills are designed to be small, easy to adapt, and composable. They work with any model. They're based on decades of engineering experience. Hack around with them. Make them your own. Enjoy.

## Installation (30-second setup)

Use [skills.sh](https://skills.sh/khanra17/skills) with pi, Codex, Antigravity, or another supported agent. The installer lets you choose which skills and agents to install them on.

### 1. Get the skills

**Productivity: install globally.**

```bash
npx skills@latest add khanra17/skills --global --skill grill-me grilling handoff i-have-adhd reflect teach unslop wait-what writing-for-agents
```

For a project-specific copy, run the same command from the project without `--global`.

**Engineering: install per project.** Run these from the project directory:

```bash
npx skills@latest add khanra17/skills/skills/engineering --skill '*'
npx skills@latest add khanra17/skills --skill grilling unslop writing-for-agents
```

This installs the engineering set, including `setup-khanra17-skills` and `triage`. The second command installs the productivity companions: `grilling` for interviews, `unslop` for human-facing writing, and `writing-for-agents` for project instructions. Engineering flows do not depend on a global installation.

The installed files are yours to edit. Update when you want with `npx skills update`.

### 2. Run `/setup-khanra17-skills`

For engineering skills, run it once per repo. Productivity skills do not need project setup. It will:

- Ask you which issue tracker you want to use (GitHub, Linear, or local files)
- Ask you what labels you apply to tickets when you triage them (`/triage` uses labels)
- Set up the glossary and ADR consumer guide, confirming the layout for multi-context repos
- Draft stack-aware `AGENTS.md` guidance in a consistent format, with your approval
- Confirm the fixed Gitmoji + Conventional Commits convention, with repository-specific overrides
- Offer GitHub Projects for delivery tracking when needed, without requiring a board for small projects
- Offer optional reference collections for [reference-codebases](./docs/engineering/reference-codebases.md). You can defer this or request reference-only setup later.

### 3. Bam - you're ready to go.

## Why These Skills Exist

These skills address common failure modes with Claude Code, Codex, and other coding agents.

### #1: The Agent Didn't Do What I Want

> "No-one knows exactly what they want"
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**The Problem**. The most common failure mode in software development is misalignment. You think the dev knows what you want. Then you see what they've built - and you realize it didn't understand you at all.

This is just the same in the AI age. There is a communication gap between you and the agent. The fix for this is a **grilling session** - getting the agent to ask you detailed questions about what you're building.

**The Fix** is to use:

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) - for non-code uses
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) - same as [`/grill-me`](./skills/productivity/grill-me/SKILL.md), but adds more goodies (see below)

These skills help you align with the agent before you get started, and think deeply about the change you're making. Use them _every_ time you want to make a change.

### #2: The Agent Is Way Too Verbose

> With a ubiquitous language, conversations among developers and expressions of the code are all derived from the same domain model.
>
> Eric Evans, [Domain-Driven-Design](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

**The Problem**: At the start of a project, devs and the people they're building the software for (the domain experts) are usually speaking different languages.

I felt the same tension with my agents. Agents are usually dropped into a project and asked to figure out the jargon as they go. So they use 20 words where 1 will do.

**The Fix** for this is a shared language. It's a document that helps agents decode the jargon used in the project.

<details>
<summary>
Example
</summary>

A project's `GLOSSARY.md` defines shared terms (see the [glossary docs](./docs/engineering/glossary.md)). In a course-management app, which description is easier to read?

- **BEFORE**: "There's a problem when a lesson inside a section of a course is made 'real' (i.e. given a spot in the file system)"
- **AFTER**: "There's a problem with the materialization cascade"

This concision pays off session after session.

</details>

This is built into [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md). It's a grilling session, but that helps you build a shared language with the AI, and document hard-to-explain decisions in ADR's.

It's hard to explain how powerful this is. It might be the single coolest technique in this repo. Try it, and see.

> [!TIP]
> A shared language has many other benefits than reducing verbosity:
>
> - **Variables, functions and files are named consistently**, using the shared language
> - As a result, the **codebase is easier to navigate** for the agent
> - The agent also **spends fewer tokens on thinking**, because it has access to a more concise language

### #3: The Code Doesn't Work

> "Always take small, deliberate steps. The rate of feedback is your speed limit. Never take on a task that’s too big."
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**The Problem**: Let's say that you and the agent are aligned on what to build. What happens when the agent _still_ produces crap?

It's time to look at your feedback loops. Without feedback on how the code it produces actually runs, the agent will be flying blind.

**The Fix**: You need the usual tranche of feedback loops: static types, browser access, and automated tests.

For automated tests, the red-green loop gives the agent feedback: write a failing test, then implement enough behavior to pass it.

The **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill** works one red-green slice at a time and gives the agent guidance on what makes good and bad tests. Refactoring belongs to the review stage.

For debugging, **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** wraps best debugging practices into a disciplined loop, gated phase by phase.

### #4: We Built A Ball Of Mud

> "Invest in the design of the system _every day_."
>
> Kent Beck, [Extreme Programming Explained](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)

> "The best modules are deep. They allow a lot of functionality to be accessed through a simple interface."
>
> John Ousterhout, [A Philosophy Of Software Design](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)

**The Problem**: Most apps built with agents are complex and hard to change. Because agents can radically speed up coding, they also accelerate software entropy. Codebases get more complex at an unprecedented rate.

**The Fix** for this is a radical new approach to AI-powered development: caring about the design of the code.

This is built in to every layer of these skills:

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) confirms testing seams and captures the agreed requirements and decisions in a spec

And crucially, [`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) surveys a codebase for deepening opportunities and hands you the candidates. I recommend running it on your codebase once every few days. It is a survey, not a rescue: on a genuinely old codebase it will find real candidates, but it won't untangle the mud for you.

### Summary

Software engineering fundamentals matter more than ever. These skills are my best effort at condensing these fundamentals into repeatable practices, to help you ship the best apps of your career. Enjoy.

## Reference

These split on one axis: who can invoke them. **User-invoked** skills are reachable only when you type them (e.g. `/grill-me`); their job is to orchestrate. **Model-invoked** skills can be invoked by you _or_ reached for automatically by the agent when the task fits; they hold the reusable discipline. A user-invoked skill may invoke model-invoked skills, but never another user-invoked one.

### Engineering

Skills I use daily for code work.

**User-invoked**

- **[which-skill](./skills/engineering/which-skill/SKILL.md)**: Ask which skill or flow fits your situation. A router over the skills in this repo. [Docs](./docs/engineering/which-skill.md)
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**: Grilling session that also builds your project's domain model, sharpening terminology and updating `GLOSSARY.md` and ADRs inline. [Docs](./docs/engineering/grill-with-docs.md)
- **[triage](./skills/engineering/triage/SKILL.md)**: Move issues through a state machine of triage roles. [Docs](./docs/engineering/triage.md)
- **[reference-codebases](./skills/engineering/reference-codebases/SKILL.md)**: Learn from established projects to discover approaches, question proposed solutions, and improve implementation. [Docs](./docs/engineering/reference-codebases.md)
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**: Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick. [Docs](./docs/engineering/improve-codebase-architecture.md)
- **[setup-khanra17-skills](./skills/engineering/setup-khanra17-skills/SKILL.md)**: Prepare project agent instructions and configure tracker, triage, domain docs, commit conventions, and optional Projects and reference collections. [Docs](./docs/engineering/setup-khanra17-skills.md)
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**: Turn the current conversation into a spec and publish it to the issue tracker. No interview, just synthesizes what you've already discussed. [Docs](./docs/engineering/to-spec.md)
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**: Break any plan, spec, or conversation into tracer-bullet tickets with blocking edges, using one file per ticket locally or native blocking links on a real tracker. [Docs](./docs/engineering/to-tickets.md)
- **[implement](./skills/engineering/implement/SKILL.md)**: Build the work described by a spec or set of tickets, driving `/tdd` at pre-agreed seams and closing out with `/code-review` before committing. [Docs](./docs/engineering/implement.md)
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**: Plan a huge chunk of work, more than one agent session can hold, as a shared map of decision tickets on the issue tracker, and resolve them one at a time until the way to the destination is clear. [Docs](./docs/engineering/wayfinder.md)

**Model-invoked**

- **[git-commit](./skills/engineering/git-commit/SKILL.md)**: Make coherent commits with a fixed type-to-emoji convention, including final squash messages. [Docs](./docs/engineering/git-commit.md)
- **[github-project](./skills/engineering/github-project/SKILL.md)**: Maintain an opted-in delivery board without replacing issue triage or planning. [Docs](./docs/engineering/github-project.md)
- **[prototype](./skills/engineering/prototype/SKILL.md)**: Build a throwaway prototype to answer a design question, either a single shareable HTML file for state/logic questions, or several radically different UI variations toggleable from one route. [Docs](./docs/engineering/prototype.md)
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**: Disciplined diagnosis loop for hard bugs and performance regressions: build a feedback loop that goes red on this bug → minimise → hypothesise → instrument → fix → regression-test. [Docs](./docs/engineering/diagnosing-bugs.md)
- **[research](./skills/engineering/research/SKILL.md)**: Investigate a question against high-trust primary sources and capture the findings as a cited Markdown file in the repo, run as a background agent. [Docs](./docs/engineering/research.md)
- **[tdd](./skills/engineering/tdd/SKILL.md)**: Test-driven development with a red-green loop. Builds features or fixes bugs one vertical slice at a time, leaving refactoring to review. [Docs](./docs/engineering/tdd.md)
- **[glossary](./skills/engineering/glossary/SKILL.md)**: Build and sharpen the project's domain language, maintaining `GLOSSARY.md` and `GLOSSARY-MAP.md`. [Docs](./docs/engineering/glossary.md)
- **[adr](./skills/engineering/adr/SKILL.md)**: Record and revise significant architectural decisions in ADRs. [Docs](./docs/engineering/adr.md)
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**: Shared discipline and vocabulary for designing deep modules: a lot of behaviour behind a small interface, placed at a clean seam, testable through that interface. [Docs](./docs/engineering/codebase-design.md)
- **[code-review](./skills/engineering/code-review/SKILL.md)**: Two-axis review of committed or work-in-progress changes since a fixed point: **Standards** (repo standards plus a Fowler smell baseline) and **Spec** (the agreed requirements), run as parallel sub-agents so neither pollutes the other. [Docs](./docs/engineering/code-review.md)
- **[wizard](./skills/engineering/wizard/SKILL.md)**: Generate an interactive bash wizard that walks a human through steps only they can perform: provisioning infrastructure, setting up credentials or CI secrets, walking an unfamiliar third-party dashboard, or running a one-off migration or cutover. [Docs](./docs/engineering/wizard.md)

### Productivity

General workflow tools, not code-specific.

**User-invoked**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**: Get relentlessly interviewed about a plan or design until every branch of the design tree is resolved. [Docs](./docs/productivity/grill-me.md)
- **[handoff](./skills/productivity/handoff/SKILL.md)**: Compact the current conversation into a handoff document so another agent can continue the work. [Docs](./docs/productivity/handoff.md)
- **[teach](./skills/productivity/teach/SKILL.md)**: Explain a concept plainly or teach a topic over several sessions with practical lessons and a learning record. [Docs](./docs/productivity/teach.md)
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**: Fire this the moment a message doesn't land. The agent re-pitches it with the context you're missing, in plain English, using `GLOSSARY.md` vocabulary when available. [Docs](./docs/productivity/wait-what.md)

**Model-invoked**

- **[grilling](./skills/productivity/grilling/SKILL.md)**: Interview the user relentlessly about a plan, decision, or idea until every branch of the design tree is resolved. The reusable interview primitive behind `grill-me`, `grill-with-docs`, `triage`, `wayfinder` and `improve-codebase-architecture`. [Docs](./docs/productivity/grilling.md)
- **[unslop](./skills/productivity/unslop/SKILL.md)**: Apply plain, natural writing automatically to human-facing prose, or rewrite selected text on request. [Docs](./docs/productivity/unslop.md)
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**: Writing documents for agents: skills, AGENTS.md, and any doc an agent reaches by a pointer. [Docs](./docs/productivity/writing-for-agents.md)
