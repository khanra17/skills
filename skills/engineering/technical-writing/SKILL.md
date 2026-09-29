---
name: technical-writing
description: Write or review human-facing technical material. Use for documentation, READMEs, guides, RFCs, issue descriptions, and PR descriptions.
---

# Technical writing

Write for a reader who needs to learn, complete a task, look something up, or understand a decision. Technical accuracy and a usable structure come before polishing sentences.

When supporting another skill or workflow, its instructions govern scope, format, required detail, interaction, and approval gates. Apply this writing guidance within those requirements, using the established audience and evidence rather than restarting discovery or repeating completed checks.

## 1. Establish the reader and task

Use the request and existing document to identify the audience, what they already know, and what they need to accomplish. Ask only when missing information would change the document.

Stay within the requested scope: draft text, edit the named files, or return review findings. Preserve the project's document templates and useful existing content.

## 2. Check the source material

Read the relevant code, diff, configuration, existing docs, or supplied sources before making technical claims. Use the actual symbols, paths, flags, and UI labels. Reuse established project terminology rather than inventing synonyms.

Separate implemented behavior from proposals, assumptions, and unknowns. If a fact cannot be verified, qualify it or flag the question rather than writing a plausible answer as fact.

## 3. Organize around the reader's need

Use the Diátaxis distinction to choose an emphasis, not to force every document into a separate file:

- **Tutorial:** guide a learner through a concrete result. Include prerequisites, manageable steps, and visible checkpoints. Explain enough to keep the learner oriented.
- **How-to:** solve a specific problem. Give the required setup, ordered actions, relevant branches, and a way to verify success. Link background that would interrupt the task.
- **Reference:** make facts easy to find. Group options, defaults, limits, errors, and examples by the thing being described. State version or environment limits where they matter.
- **Explanation:** answer a bounded why question. Explain constraints, decisions, trade-offs, and alternatives. Distinguish facts from recommendations.

A README may combine an overview, installation instructions, and a reference index. Give each section a clear job; split and link only when that helps navigation. Keep short technical summaries, such as PR descriptions, proportional to their purpose rather than imposing a full guide structure.

### Issue and PR descriptions

Lead with the problem and the intended or verified outcome, then explain the approach and relevant verification. Prefer a meaningful change over an inventory of edited files; retain technical detail needed to understand risk or review the work. Do not invent a benefit or measurement to make a title sound stronger.

Writing a description does not authorize publishing it or opening a PR. For titles used as squash messages, follow the repository's commit convention.

## 4. Make the document usable

Call the Skill tool with "unslop" for plain, natural prose.

- Put prerequisites, conditions, and warnings before the steps they affect. Number ordered steps and include expected output or another observable success check where useful.
- State who does what. Use direct commands for instructions and ordinary words for explanations, while preserving precise technical terms.
- Keep instructions easy to follow. Split sentences when they carry too many actions or conditions, not merely because they exceed a word count.
- Keep modifiers such as "only" next to what they modify. Make pronouns point to an obvious noun and break up ambiguous noun strings.
- Name each concept consistently. Use descriptive headings and link text that helps the reader find the next piece of information.
- Use code formatting for commands, symbols, and paths. Follow the language and repository conventions in examples, including indentation.
- Keep meaningful qualifications, useful context, and natural sentence variety. Edit wording when it helps the reader, not to satisfy a word blacklist.

## 5. Verify and deliver

Check that the document answers the reader's original question. Trace its commands, paths, defaults, and examples back to the sources. For a procedure, check that its steps are complete and its success checks match the described behavior. Check local links when editing files.

Run examples only when safe and authorized. Distinguish source inspection from actual execution; do not claim a procedure was tested when it was only read. Report unresolved factual questions or untested critical steps briefly.

Return the draft, make the requested file edits, or present actionable review findings. For file edits, name the changed files and summarize material changes. Leave unrelated docs and skills alone.

This skill provides reusable writing guidance, not an extra required stage of implementation. Agent instruction design belongs to `/writing-for-agents`; this skill focuses on human-facing technical material.
