# technical-writing

## What it does

`technical-writing` guides the writing and review of human-facing technical material: documentation, READMEs, guides, RFCs, issue descriptions, and PR descriptions. It checks technical claims against the code or sources before stating them, and shapes the document around what the reader came to do: follow a tutorial, complete a task, look something up, or understand a decision.

## When to reach for it

The agent reaches for it when there is technical writing to do. You can also type `/technical-writing` with the text or document, and say who it is for when that isn't obvious.

For example: "Write a backup guide for someone running this project locally." A useful result covers the prerequisites, the actual backup command, where the backup goes, and how to check it worked.

Use [unslop](../productivity/unslop.md) when the content is right and you want only the wording edited. Use [writing-for-agents](../productivity/writing-for-agents.md) for instructions an agent will read.

## Common questions

**What happens when another skill calls it?**

That skill keeps control of the format, the required detail, and the approvals. A spec keeps its sections and an ADR keeps its format; technical-writing works on how clearly the content is expressed.

**How does it write issue and PR descriptions?**

Problem and outcome first, then the approach and how it was verified, with the detail a reviewer needs to judge risk. Stated benefits and measurements need evidence. The description is a draft; publishing it is your call.

**Does it test the examples it writes?**

It traces commands, paths, and defaults back to their source. It runs an example only when that is safe and you have allowed it, and it tells you which steps it ran and which it only read.

**What does a review return?**

Findings about the document. It edits files only when you ask for edits.

## It's working if

- Every command, path, and flag in the document exists in the project as written.
- Each procedure tells the reader how to recognize success.
- The delivery note says which steps were run and which were only read.
