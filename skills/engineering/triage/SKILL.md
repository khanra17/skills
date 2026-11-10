---
name: triage
description: Move issues through a state machine of triage roles, categorise, verify, grill if needed, and write implementation briefs.
disable-model-invocation: true
---

# Triage

Move issues on the project issue tracker through a small state machine of triage roles.

## Roles

Two **category** roles:

- `bug`: something is broken
- `enhancement`: new feature or improvement

Four **state** roles:

- `needs-triage`: needs evaluation
- `needs-info`: waiting on missing information
- `ready-for-implementation`: fully specified; no further triage needed, not an implementation assignment
- `suspended`: not pursuing this request; closed as not planned

Every open, evaluated issue carries exactly one category role and one state role. If state roles conflict, flag it and ask the maintainer before doing anything else.

These are canonical role names. `docs/agents/triage-labels.md` maps them to this repo's label strings, and `docs/agents/issue-tracker.md` says how to read and write issues. If either is missing, tell the user to run `/setup-khanra17-skills`.

State transitions: move an evaluated issue to `needs-info`, `ready-for-implementation`, or `suspended`; use `needs-triage` while evaluation is unfinished. Re-evaluate `needs-info` once the missing information arrives. The maintainer can override at any time.

## Invocation

The maintainer invokes `/triage` and describes what they want in natural language. Interpret the request and act. Examples:

- "Show me anything that needs my attention"
- "Let's look at #42"
- "Move #42 to ready-for-implementation"
- "Which issues need no further triage?"

## Show what needs attention

Query the issue tracker and present three buckets, oldest first:

1. **Unlabeled**: never triaged.
2. **`needs-triage`**: evaluation in progress.
3. **`needs-info` with reporter activity since the last triage notes**: needs re-evaluation.

Show counts and a one-line summary per item. Let the maintainer pick.

## Triage a specific issue

1. **Gather context.** Read the full issue (body, comments, labels, author, dates). If prior triage notes exist, read them and check whether the reporter has answered the outstanding questions, so resolved questions are not asked again. Explore the codebase using the project's domain glossary, respecting ADRs in the area. Run two checks:
   - **Redundancy**: search for an existing implementation of the requested behavior by domain concept, beyond the request's wording, and report where you looked.
   - **Prior decisions**: search related closed issues and relevant ADRs for earlier rejections or trade-offs. Surface matching reasons and links; the maintainer decides whether they still apply.

2. **Verify the claim.** For a bug, reproduce it from the reporter's steps. Report what happened: confirmed (with code path), failed, or insufficient detail (a strong `needs-info` signal). For an enhancement, confirm the gap it describes exists.

3. **Recommend.** Tell the maintainer your category and state recommendation with reasoning: the verification result, a brief codebase summary relevant to the request, and whether it is already implemented. Wait for direction.

4. **Grill (if needed).** If the request needs fleshing out, invoke the `grilling` skill and grill it into shape a round of questions at a time. Invoke `glossary` as domain terms are resolved and `adr` when an architectural decision is made.

5. **Apply the outcome:**
   - **Already implemented**: remove the triage-state label, point to the existing behavior, and close as completed.
   - `ready-for-implementation`: post an implementation brief written to [AGENT-BRIEF.md](AGENT-BRIEF.md), including any manual steps or access requirements.
   - `needs-info`: post triage notes (template below).
   - `suspended`: record on the issue why the request is being declined or cancelled, apply the state label, and close as not planned. Link earlier issues or relevant ADRs.
   - `needs-triage`: apply the role, with a comment if there is partial progress worth keeping.

## Quick state override

If the maintainer says "move #42 to ready-for-implementation", trust them. Confirm what you're about to do (role changes, comment, close), then act, with no grilling. If moving to `ready-for-implementation` without a grilling session, ask whether they want an implementation brief written.

## Needs-info template

```markdown
## Triage Notes

**What we've established so far:**

- point 1
- point 2

**What we still need from you (@reporter):**

- question 1
- question 2
```

Capture everything resolved during grilling under "established so far" so the work isn't lost. Each question names the specific fact needed and how the reporter can supply it.
