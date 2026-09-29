Skills are organized into bucket folders under `skills/`:

- `engineering/`: daily code work
- `productivity/`: daily non-code workflow tools

Every skill in `engineering/` or `productivity/` must have a reference in the top-level `README.md`.

Each skill entry in the top-level `README.md` must link the skill name to its `SKILL.md`, include a one-line description, and link its human-facing docs. Group entries by bucket, then into **User-invoked** and **Model-invoked**. Keep this index in the top-level `README.md`, without separate bucket READMEs.

Human-facing docs live at `docs/engineering/<skill-name>.md` or `docs/productivity/<skill-name>.md`, mirroring the skill buckets. Use relative links. When you add, rename, or change a skill's behaviour, re-sync its docs if the page exists. A finished page carries four sections: **What it does**, **When to reach for it**, **Common questions**, and **It's working if**.

Every `SKILL.md` is either user-invoked (`disable-model-invocation: true`, reachable only by the human) or model-invoked (model- or user-reachable).

[`which-skill`](./skills/engineering/which-skill/SKILL.md) is the router that maps every user-reachable skill and how they relate. The same trigger that re-syncs a docs page applies to it: whenever you add, rename, remove, or change how a user-reachable skill fits the flows, re-read `which-skill`'s `SKILL.md` and update it so the map stays accurate: a new skill it never mentions, or a stale one it still routes to, is a router that lies.

Keep `notes.md` as the record of the user's decisions and review rules until they confirm that adding skills from other sources is finished.

No em-dashes anywhere in this repo's prose (`SKILL.md` files, docs, `README.md`, `CHANGELOG.md`, ADRs, changesets, code comments). Where a sentence reaches for one, rewrite it instead with a comma, colon, period, parentheses, or a conjunction, whichever the sentence actually wants; never do a blind character substitution.
