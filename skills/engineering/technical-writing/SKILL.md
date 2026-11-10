---
name: technical-writing
description: Write or review human-facing technical material. Use for documentation, READMEs, guides, RFCs, issue descriptions, and PR descriptions.
---

# Technical writing

Write for a reader who needs to learn, complete a task, look something up, or understand a decision. Technical accuracy and a usable structure come before polished sentences.

When another skill or workflow called this one, that workflow governs scope, format, required detail, and approval gates. Apply this guidance inside those requirements, using the audience and evidence already established.

## 1. Check the source material

Read the relevant code, diff, configuration, existing docs, or supplied sources before making a technical claim. Use the actual symbols, paths, flags, and UI labels, and the project's established terms.

Separate implemented behavior from proposals, assumptions, and unknowns. A fact you cannot verify is written as a qualified claim or raised as a question.

## 2. Organize around the reader's need

Pick the emphasis that matches what the reader came to do. One document can hold several of these as sections; each section does one job.

- **Tutorial:** takes a learner to a concrete result, with prerequisites, steps, and visible checkpoints.
- **How-to:** solves a specific problem: the setup, the ordered actions, the branches that matter, and a way to verify success.
- **Reference:** makes facts findable: options, defaults, limits, and errors, grouped by the thing described, with version or environment limits stated.
- **Explanation:** answers a bounded why question: constraints, decisions, trade-offs, and alternatives, with facts kept apart from recommendations.

Put prerequisites, conditions, and warnings before the steps they affect. Give each procedure an observable success check.

### Issue and PR descriptions

Lead with the problem and the intended or verified outcome, then the approach and how it was verified. Describe the change in terms of what it means; keep the technical detail a reviewer needs to judge risk. Every stated benefit or measurement has evidence behind it.

A description you wrote is a draft: publishing it or opening the PR is the user's call. A title that will become a squash message follows the repository's commit convention.

## 3. Write and verify

Invoke the `unslop` skill for plain, natural prose.

Before delivering, trace every command, path, default, and example back to its source, and check local links when editing files. Run examples only when it is safe and authorized, and say which steps you ran and which you only read. Report unresolved factual questions and untested critical steps briefly.

Deliver what was asked for: the draft, the file edits, or review findings. For file edits, name the changed files and summarize the material changes.
