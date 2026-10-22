---
name: git-commit
description: Create coherent commits with a fixed Gitmoji and Conventional Commits convention. Use when committing changes, choosing commit boundaries, or drafting commit and squash-merge messages.
---

# Git Commit

Read `docs/agents/git-commit.md` if present for repository overrides, scopes, and existing validation or template paths. Otherwise use the convention below, unless the repository documents a different one. Resolve conflicts with an existing validator rather than bypassing it. Drafting a message does not authorize a commit; the active workflow owns approval.

## Commit boundaries

Inspect the staged and unstaged changes against the requested scope. Plan commit groups before staging. Make each commit one independently understandable, reversible change, with its directly related tests and documentation. Split unrelated intentions even when they share a file or hunk; do not split a working change merely because it spans files.

Preserve unrelated work and the user's staging choices. Stage paths only when all their changes belong to this commit; otherwise select or split hunks. If existing staged work would enter the wrong commit, ask before rearranging it. Verify the staged patch and message agree before committing, and check the resulting commit and remaining changes afterward.

Reuse checks already run for this patch; rerun affected checks if it changed. A commit request does not authorize pushing, amending history, or bypassing hooks or signing.

## Message convention

```text
<type>(<scope>): <emoji> <description>
```

Scope is optional. Use the repository's vocabulary, not scopes borrowed from another project. Write an imperative description without a trailing period; aim for a subject under 72 characters. Explain non-obvious reasons in the body, without a mandatory report template.

**The type determines the emoji.** Use exactly one from this mapping, never a thematic alternative for the same type:

| Type | Emoji | Use |
| --- | --- | --- |
| `feat` | ✨ | New capability |
| `fix` | 🐛 | Bug fix |
| `docs` | 📝 | Documentation only |
| `refactor` | ♻️ | Restructuring without behavior change |
| `perf` | ⚡️ | Performance improvement |
| `test` | ✅ | Tests or fixtures |
| `build` | 📦 | Dependencies, packaging, or build configuration |
| `ci` | 👷 | CI workflows |
| `chore` | 🔧 | Maintenance outside the other types |
| `style` | 🎨 | Code formatting without behavior change |
| `revert` | ⏪ | Reverting a previous change |

A feature stays `feat` with ✨ even when it changes tests, docs, or UI. `style` means code formatting, not a new visual feature. A breaking change keeps its type's emoji, adds `!` before the colon, and explains the incompatibility in a `BREAKING CHANGE:` footer.

```text
feat(auth): ✨ add passkey sign-in
fix(sync): 🐛 retry interrupted uploads
feat(api)!: ✨ replace the authentication response

BREAKING CHANGE: clients must read tokens from the credentials object.
```

## Squash merges

When preparing a squash-merge message, apply the same convention to the combined patch. Check the actual final message, not just the individual commits or PR title. This does not require PRs or change the repository's merge strategy.
