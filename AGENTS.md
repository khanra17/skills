Skills are organized into bucket folders under `skills/`:

- `engineering/`: daily code work
- `productivity/`: daily non-code workflow tools

Every skill in `engineering/` or `productivity/` must have a reference in the top-level `README.md`.

Each skill entry in the top-level `README.md` must link the skill name to its `SKILL.md`, include a one-line description, and link its human-facing docs. Group entries by bucket, then into **User-invoked** and **Model-invoked**. Keep this index in the top-level `README.md`, without separate bucket READMEs.

Human-facing docs live at `docs/engineering/<skill-name>.md` or `docs/productivity/<skill-name>.md`, mirroring the skill buckets. Use relative links. When you add, rename, or change a skill's behaviour, re-sync its docs if the page exists. A finished page opens with `# <skill-name>` and carries four sections: **What it does**, **When to reach for it**, **Common questions**, and **It's working if**. Common questions holds questions a user would actually ask, each answered with what the skill does. It's working if lists things the user can observe.

Every `SKILL.md` is either user-invoked (`disable-model-invocation: true`, reachable only by the human) or model-invoked (model- or user-reachable).

[`which-skill`](./skills/engineering/which-skill/SKILL.md) is the router that maps every user-reachable skill and how they relate. The same trigger that re-syncs a docs page applies to it: whenever you add, rename, remove, or change how a user-reachable skill fits the flows, re-read `which-skill`'s `SKILL.md` and update it so the map stays accurate: a new skill it never mentions, or a stale one it still routes to, is a router that lies.

A skill's behaviour is described in four places: its `SKILL.md`, its README entry, the router, and its docs page. The `SKILL.md` is the source of truth. After changing one, read the other three and bring them into line.

One skill invokes another with the wording "invoke the `<name>` skill", which reads correctly in every harness. A link inside `skills/` may only point inside `skills/`: an install copies the skill folders and nothing else.

No em-dashes anywhere in this repo's prose (`SKILL.md` files, docs, `README.md`, `CHANGELOG.md`, ADRs, changesets, code comments). Where a sentence reaches for one, rewrite it instead with a comma, colon, period, parentheses, or a conjunction, whichever the sentence actually wants; never do a blind character substitution.

Every skill that dispatches a subagent says to start it with a fresh context window. Some harnesses (Codex, for one) fork the parent conversation by default, and a fork inherits the parent's context, which is what the subagent was meant to escape.

Skills are read by a model that copies the patterns it is fed, so write them to the standard the `writing-for-agents` skill sets: state the wanted behaviour once at normal volume, and leave out sentences that deny a past mistake.
