---
name: wayfinder
description: Plan a huge chunk of work (more than one agent session can hold) as a shared map of decision tickets on your issue tracker, and resolve them one at a time until the way to the destination is clear.
disable-model-invocation: true
---

An idea has arrived that is too big for one agent session, and the way from here to its **destination** isn't visible yet. This skill charts that way as a **shared map** on the repo's issue tracker, then works its **decision tickets** (questions whose resolution is a decision, not slices of a build) one at a time until the route is clear.

Naming the destination is the first act of charting, because it fixes the scope of every ticket. It might be a spec to hand off, a decision to lock before planning starts, or a change made in place such as a data-structure migration. The map works for any domain: engineering work, course content, whatever fits the shape.

**Wayfinder plans.** Each ticket resolves a decision, and the map is done when nothing is left to decide before someone goes and does the thing. The pull to just do the work is the signal you've reached the edge of the map and it's time to hand off.

**Refer by name.** Every map and ticket has a title. In everything the human reads (narration, the map's Decisions so far), write the title, linked, and keep bare ids and numbers out of prose: a row of `#42, #43, #44` is illegible.

## The map

The map is a single issue labelled `wayfinder:map`, with its tickets as child issues. It is an **index**: each decision lives in exactly one place, its ticket, and the map carries a one-line gist and a link.

Where the map, its tickets, blocking, and frontier queries physically live is tracker-specific. Read the "Wayfinding operations" section of `docs/agents/issue-tracker.md` for how this repo expresses them. If that guide is missing, tell the user to run `/setup-khanra17-skills`.

### The map body

The whole map at low resolution, loaded once per session. Open tickets are found by query and are not listed here.

```markdown
## Destination

<what reaching the end of this map looks like: the spec, decision, or change this effort is finding its way to. One or two lines; every session orients to it before choosing a ticket.>

## Notes

<domain; skills every session should consult; standing preferences for this effort>

## Decisions so far

<!-- the index: one line per closed ticket -->

- [<closed ticket title>](link): <one-line gist of the answer>

## Not yet specified

<!-- in-scope questions that can't be stated precisely yet -->

## Out of scope

<!-- work ruled beyond the destination: one line each, the gist and why, linking any closed ticket -->
```

### Tickets

Each ticket is a child issue of the map. Its body is the question, sized to resolve in one agent session (about 100k tokens of work):

```markdown
## Question

<the decision or investigation this ticket resolves>
```

- **Type**: a `wayfinder:<type>` label, one of `research`, `prototype`, `grilling`, `task` (see Ticket types).
- **Claim**: a session claims a ticket by assigning it to the dev driving the map, before any work, so concurrent sessions skip it. An open, unassigned ticket is unclaimed.
- **Blocking**: the tracker's native dependency relationship, so the human sees what is takeable in the tracker's own UI. A ticket is **unblocked** when every ticket blocking it is closed.
- **Frontier**: the open, unblocked, unclaimed children.
- **Answer**: recorded on resolution as a comment, not in the body. Assets created while resolving are linked from the issue.

## Ticket types

A ticket is **HITL** (worked with a human who speaks for themselves) or **AFK** (driven by the agent alone). A HITL ticket resolves only through that live exchange; the agent never answers the human's side of it.

- **Research** (AFK): reading documentation, third-party APIs, other projects' code, or local knowledge bases to surface a fact a decision waits on. Resolved by a subagent that follows the `research` skill.
- **Prototype** (HITL): a cheap, concrete artifact to react to (an outline, a stub, UI or logic code), built by invoking the `prototype` skill. Use when "how should it look" or "how should it behave" is the question. The resolution links the verdict and its evidence.
- **Grilling** (HITL): conversation, and the default. Invoke the `grilling` skill, with `glossary` as domain terms are resolved and `adr` when an architectural decision is made.
- **Task** (HITL or AFK): manual work that must happen before a decision can be made: signing up for a service so its API can be judged, provisioning access, moving data so its shape can be seen. It is the one type that does something, and it earns its place by unblocking a decision. The agent does it alone where it can; otherwise it hands the human a precise checklist. The answer records what was done and the facts later tickets depend on (credentials location, new URLs, row counts).

## Fog and scope

The map is deliberately incomplete. Beyond the live tickets lies the **fog**: decisions you can tell are coming but can't pin down, because they hang on questions still open. The **Not yet specified** section is where that view is written down, as loosely or as fully as it can be seen.

**Fog or ticket?** The test is whether you can state the question precisely now, whether or not you can answer it now.

- A sharp question is a ticket, even if it is blocked.
- A question you can't yet phrase sharply stays in Not yet specified, unsliced: one patch of fog may become several tickets, or none, once the frontier reaches it.

Resolving a ticket clears the fog ahead of it: whatever is now specifiable **graduates** into tickets and leaves the section.

Fog only gathers toward the destination. Work beyond the destination is **out of scope** and goes in its own section, with one line saying why. When an existing ticket turns out to sit past the destination, close it and add that line, linking the closed ticket. Out-of-scope work stays out of Decisions so far, which records the route actually walked, and it returns only if the destination is redrawn.

## Invocation

Two modes. In both, a session resolves at most one ticket, research tickets excepted.

### Chart the map

The user invokes with a loose idea.

1. **Name the destination.** Invoke the `grilling` skill (with `glossary` and `adr` as terms and decisions settle) to pin down what this map is finding its way to.
2. **Map the frontier.** Grill again, breadth-first: fan out across the whole space, surfacing the open decisions and the first steps takeable now. If this surfaces no fog (the way is already clear and the whole journey fits one session), the effort needs no map: stop and ask the user how they'd like to proceed.
3. **Create the map**: Destination and Notes filled in, Decisions so far empty, the fog sketched into Not yet specified.
4. **Create the tickets you can specify now** as child issues, then wire blocking edges in a second pass (issues need ids before they can reference each other).
5. **Start the research.** For each `research` ticket on the frontier, claim it, then dispatch a subagent with a fresh context window that follows the `research` skill, in parallel. Post each full cited report as the ticket's resolution comment, close the ticket, and link it from the map. Then handle what the answers surfaced as in step 5 of Work through the map.
6. Stop. Charting is one session's work, and every non-research ticket waits for its own session.

### Work through the map

The user invokes with a map (URL or number), and optionally a ticket.

1. Load the map body, not every ticket.
2. Choose the ticket: the one the user named, otherwise the first on the frontier. Claim it before any work.
3. Resolve it. Fetch the full body of any related or closed ticket when you need its detail, and invoke the skills the map's Notes name. With no guidance there, invoke `grilling`.
4. Record the resolution: post the answer as a resolution comment, close the issue, and append its gist and link to Decisions so far.
5. Update the map: create and wire newly surfaced tickets, graduate any fog the answer made specifiable, rule out of scope any ticket the answer shows to sit beyond the destination, and update or close tickets the decision invalidated.

The user may run unblocked tickets in parallel, so expect other sessions to be editing the tracker concurrently.
