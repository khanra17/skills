---
name: subagent-models
description: Pick the Claude model and reasoning effort for a sub-agent. Use in Claude Code before every launch of a sub-agent, background agent, or parallel worker, whether the user, a skill, or your own plan called for the launch.
---

# Sub-agent models

Every sub-agent launch carries a model and an effort. This skill picks both. Whether to delegate at all is settled before you get here, by the user's request or the skill you are following.

## Whose choice wins

1. A model or effort the user named for this launch.
2. The `model` a custom agent definition sets for itself.
3. The table below.

## The table

Find the row that describes the sub-agent's task and pass its model and effort on the launch. These rows are the whole menu.

| The sub-agent's task | Model | Effort |
| --- | --- | --- |
| Mechanical reading in bulk: classify, tag, extract fields, sweep many files for a known pattern, pull the failures out of logs | `haiku` | leave unset |
| Read-only finding and summarising that takes comprehension: locate code across a codebase, trace callers, summarise a module or a set of docs | `sonnet` | `medium` |
| Writing or editing code to an agreed design, or a scoped task that needs judgment | `opus` | `medium` |
| Review, verification, debugging, cited research, implementation backed by tests | `opus` | `high` |
| Exhaustive audit, where one missed case is the failure: a stone-by-stone review of a high-risk change, replaying a large body of logs or data against an implementation, platform work that needs many extra checks | `opus` | `xhigh` |
| Divergent or unprovable work: several different designs, architecture, UI or visual direction, a second opinion on a thread going in circles, a ship-or-hold verdict on finished work | `fable` | `medium` |
| The hardest technical problem, or a task `opus` at `high` fell short on | `fable` | `high` |

Two questions place a task that no row names:

- **Can the result be proven?** Work a test, a build, or a source can check goes to `opus`, which checks everything twice. Work with no objective better goes to `fable`, which offers a wider spread of ideas and judges when good is good enough.
- **Does it change files?** Every edit runs on `opus` or `fable`. `haiku` and `sonnet` agents read and report, so brief them as read-only.

## When a sub-agent falls short

Climb one rung at a time:

1. Give it a way to check its own work (a test, a build, a script) and relaunch on the same model and effort.
2. Raise effort one step, stopping at `high`.
3. Move up one model (`haiku`, `sonnet`, `opus`, `fable`) at `medium`.

## Launch mechanics

- Pick per agent. A parallel batch whose agents do different kinds of work gets a different row for each.
- A fork inherits this session's model and effort. When the table names another model, launch a fresh agent with a complete brief.
- `fable` costs twice what `opus` does per token. In a wide fan-out, give `fable` to the one agent that designs or judges and `opus` to the workers.
