# subagent-models

## What it does

`subagent-models` tells Claude Code which Claude model and reasoning effort to give a sub-agent, based on the kind of task the sub-agent is doing. Cheap bulk reading goes to Haiku, read-only searching to Sonnet, code and verifiable work to Opus, and design, judgment, and the hardest problems to Fable.

It keeps a short menu of model and effort pairs, plus an order for escalating when a sub-agent falls short: let it verify its work, then raise effort, then move up a model.

It is specific to Anthropic's models. No other skill in this repo refers to it, so every flow works the same with it installed or not.

## When to reach for it

You don't type it. The agent loads it on its own each time it is about to launch a sub-agent, whether you asked for the sub-agent directly or a skill such as [code-review](../engineering/code-review.md) or [research](../engineering/research.md) dispatched one.

It only covers sub-agents. For the model to run your own session on, see [Model picks](../../README.md#claude-code-model-picks) in the README.

## Common questions

**Does it make the agent launch more sub-agents?**

No. It picks the model and effort for a launch that was already going to happen. Whether to delegate is still decided by your request or by the skill being followed.

**What if I name a model or effort myself?**

Yours wins. After that comes a custom agent definition's own `model` setting, and the table applies only when neither is set.

**Why is Sonnet only used for searching?**

At medium effort it reads and summarises well for half the Opus token price. At higher effort it spends so many tokens that the saving disappears, and for writing code Opus at medium is more consistent. So Sonnet gets the read-only work where a mistake is cheap to spot.

**Why does Opus get review and Fable get design?**

Opus double-checks everything, which suits work a test or a source can prove right. Fable gives a wider spread of ideas and is willing to say finished work is good enough, which suits design questions and stuck threads.

**How do I turn it off when I switch to another AI subscription?**

Remove the skill: `npx skills remove subagent-models`, or delete its folder. Nothing else needs changing.

**The model names changed. What do I edit?**

The table in the [skill](../../skills/claude-code/subagent-models/SKILL.md), and the Model picks table in the README.

## It's working if

- Each sub-agent launch names a model, and the model differs with the task: Haiku or Sonnet for reading, Opus for code and review, Fable for design.
- Sub-agents that edit files run on Opus or Fable.
- Effort stays at medium or high, with xhigh appearing only on Opus for an exhaustive audit.
- A model you name in your prompt is the one used.
