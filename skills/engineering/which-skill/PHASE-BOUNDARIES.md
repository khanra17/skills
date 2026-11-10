# Phase boundaries

A **phase** is a chunk of work inside a session: the grilling, the implementation, the QA. A phase ends when you think "ok, we're done with that".

The **phase boundary** is the gap between two phases, and the only place this decision belongs. Mid-phase, continue, or split the work that's left into subagents. Compacting mid-phase makes the agent lose the thread.

## The five options

| Option | What it does |
| --- | --- |
| **Continue** | Stay in the session. No context switch at all. |
| **Clear** | Empty the context window and start from nothing (`/clear`, or your harness's new-session command). |
| **`/handoff`** | Write a portable markdown file and open a session anywhere against it. |
| **Subagent** | Send the task to its own context window and get a report back. |
| **Compact** | Compress this context into a summary and carry on from it (`/compact`). |

## The tree

Work top to bottom at the boundary. The first **yes** wins.

**1. Can you continue in this session?** Yes when the next phase needs this phase as a **primary source**, or when enough of the smart zone (the early part of the window, roughly the first 150k tokens, where the model still reasons sharply) is left for the next phase to fit. Grilling → implementation is the standard yes: the implementation wants the reasoning verbatim, not a summary of it. Continue costs nothing and loses nothing, so settle it first.

**2. Is the context irrelevant to what comes next?** If everything in this session (the exploration, the decisions, the dead ends) is disposable, **clear**. It takes no time and hands back the whole window, and in most harnesses the old session stays resumable.

Getting this wrong is one-way. Clear a relevant context and you lose the why behind what you built, and reading the diff back does not return it.

**3. Does the work have to travel?** `/handoff` is for exactly four cases:

- swapping to a new harness (Claude Code → Codex),
- moving to a new directory or repo,
- sending the work to a colleague,
- forking a side task you found mid-phase without derailing the current one.

What `/handoff` buys is a file that travels. If nothing is travelling, skip it.

**4. Can the task be done AFK?** If it is scoped tightly enough to run with no steering, send it to a **subagent** and leave this session untouched. Automated review is the standard case: the agent reads the diff and reports while you do something else.

**5. Otherwise, compact.** Relevant context, same harness, same directory, and you need to stay in the loop. Pass an instruction (`/compact we're going to QA this area`) so the summary keeps what the next phase needs.

Compact sits last because the four questions above it are all cheaper or more precise. Start with it and you risk a session that is confidently wrong about a decision the summary flattened.

## Primary and secondary sources

Every move except **Continue** turns a **primary source** into a **secondary source**: the session as it happened, replaced by a summary of it.

| Source | Information | Noise | Room to move |
| --- | --- | --- | --- |
| Primary (Continue) | Full | Lots | Little |
| Secondary (compact, `/handoff`) | Lossy | Less | Lots |

This is why question 1 comes first. You pay the lossiness only when staying costs more than it saves.

## These are judgement calls

Each question has taste in it, and the same boundary can go two ways on two days. The value is in asking them in order, at the boundary.
