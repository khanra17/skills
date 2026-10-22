## What it does

`technical-writing` provides reusable guidance for writing or reviewing human-facing technical material, including documentation, READMEs, guides, RFCs, issue descriptions, and PR descriptions. It focuses on what the reader needs to do or understand, checks technical claims against relevant sources, and organizes the material so the reader can use it.

It can produce a tutorial, a how-to guide, reference material, an explanation, or a document that combines useful sections. A README does not have to become several files just because it includes both an overview and installation steps.

## When to reach for it

The agent can invoke it when writing or reviewing technical material. You can also type `/technical-writing` with the text or document you want to work on. Say who it is for when that is not obvious.

For example: "Write a backup guide for someone running this project locally." A useful result would cover prerequisites, the actual backup command, where the backup goes, and how to check success. Clearer sentences alone would not make the guide complete.

Use [unslop](../productivity/unslop.md) when the content is already right and you mainly want a wording edit. Use [writing-for-agents](../productivity/writing-for-agents.md) when you are designing instructions for an agent rather than documentation for a person.

## Common questions

**Does it run after every code change?**

No. It is available when there is technical writing to do, not a requirement to create documentation after every code change. It invokes [unslop](../productivity/unslop.md) for plain, natural wording.

**Can it override another skill's workflow?**

No. The active workflow keeps control of the scope, format, required detail, interaction, and approvals. For example, a spec keeps its required sections and extensive user stories, and an ADR keeps its decision-record format. Technical-writing helps express that content clearly without restarting discovery or repeating completed checks. Short artifacts such as commit messages receive a proportionate writing pass, not a full guide-writing process.

**How does it write issue and PR descriptions?**

It leads with the problem and intended or verified outcome, then explains the approach and relevant verification. It keeps technical details needed for review without turning the description into a file inventory. Benefits and measurements must have evidence. Spec and ticket templates keep their required detail; a concise PR summary does not replace them.

Writing a description does not authorize publishing an issue or opening a PR, and it does not choose draft versus ready status. Squash-message titles follow the repository's commit convention.

**Does every document have to follow the same template?**

No. It uses the reader's purpose to choose a structure and respects useful existing templates. A task guide needs steps and a success check; a decision explanation needs context and trade-offs.

**Will it check the examples?**

It checks commands, paths, defaults, and other claims against the available sources. It runs examples only when safe and authorized, and distinguishes reading the source from actually testing a procedure. Missing facts remain questions or qualified claims, not invented details.

**Does it enforce short sentences and particular words?**

Clarity matters more than a word count. It preserves precise terms and meaningful uncertainty, follows project formatting conventions, and changes wording when doing so helps the reader.

**What does a review return?**

Actionable findings about the requested document. Asking for a review does not by itself request file edits. When you ask it to edit files, it identifies the changed files and any important unresolved questions.

## It's working if

- The intended reader can find what they need without guessing missing steps.
- Commands, paths, and examples match the actual system or are clearly marked as proposals.
- Procedures explain how to recognize success.
- Useful context and genuine uncertainty survive the edit.
- The document fits its purpose without unnecessary splitting or unrelated rewrites.
