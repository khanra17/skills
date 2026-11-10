# git-commit

## What it does

`git-commit` makes coherent commits with Gitmoji + Conventional Commit messages. Each type has one fixed emoji, so the same kind of change always looks the same in the log.

```text
feat(auth): ✨ add passkey sign-in
fix(sync): 🐛 retry interrupted uploads
```

The full mapping lives in the [skill](../../skills/engineering/git-commit/SKILL.md). Where a repository differs, its choices are in `docs/agents/git-commit.md`.

## When to reach for it

Use it to commit a finished change, to split work into separate commits, or to draft a commit or squash-merge message. The agent reaches for it when committing, and [implement](./implement.md) calls it after review.

## Common questions

**Can a repository use a different convention?**

Yes. [Setup](./setup-khanra17-skills.md) asks whether to use the standard convention and records the repository's differences: scope restrictions, overrides, and existing template or validator paths.

**How does it decide what goes in one commit?**

One commit is one change you could understand and revert by itself, with its tests and docs. Unrelated changes are split even when they share a file.

**Will it touch my staging, or push?**

It leaves unrelated work and your staged changes alone, and asks before rearranging staging. Pushing, amending, and skipping hooks each need you to ask for them.

**What about breaking changes and issue references?**

A breaking change keeps its type's emoji, adds `!` before the colon, and explains itself in a `BREAKING CHANGE:` footer. An issue reference such as `Closes #42` goes in the footer, and a squash message carries over the references of the commits it combines.

## It's working if

- Every `feat` in the log has ✨, every `fix` has 🐛, and so on down the mapping.
- Each commit can be reverted without taking an unrelated change with it.
- Changes you had staged for something else are still staged afterwards.
