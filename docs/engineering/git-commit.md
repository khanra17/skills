## What it does

`git-commit` makes coherent commits with consistent Gitmoji + Conventional Commit messages. Each type has one fixed emoji; the agent does not choose a different symbol for each feature or fix.

```text
feat(auth): ✨ add passkey sign-in
fix(sync): 🐛 retry interrupted uploads
```

The full mapping lives in the [skill](../../skills/engineering/git-commit/SKILL.md). Repository choices belong in `docs/agents/git-commit.md`.

## When to reach for it

Use it to commit a completed change, choose boundaries between independent changes, or draft a commit or squash-merge message. It is model-invoked, and [implement](./implement.md) calls it after review and checks.

## Common questions

**Can a client repository use a different convention?**

Yes. [Setup](./setup-khanra17-skills.md) asks whether to use the standard convention, then records only repository-specific differences, scope restrictions, and existing template or validator paths. The default mapping stays in the skill rather than being copied into every project.

**What about breaking changes?**

They keep the type's emoji, add `!` before the colon, and explain the incompatibility in a `BREAKING CHANGE:` footer.

**Does every file become a separate commit?**

No. Each commit should be one independently understandable, reversible change. Its tests and documentation belong with it; unrelated changes get separate commits even when they share a file or hunk.

**Will it disturb my staging or push the result?**

It preserves unrelated work and asks before rearranging existing staging. A commit request does not authorize a push, history amendment, or bypassing hooks. Asking for a message draft does not authorize committing.

**Does this enforce the format automatically?**

No. It follows existing validators but does not install one. Setup does not add hooks or dependencies automatically. If you squash-merge, the convention applies to the final combined message too, without requiring a particular merge strategy.

## It's working if

- The same type consistently gets the same emoji.
- Each commit is one reversible change, with unrelated intentions split even inside a file.
- Repository conventions and existing validation agree.
- Unrelated changes and staging remain intact.
- The final squash message is consistent with the rest of the history.
