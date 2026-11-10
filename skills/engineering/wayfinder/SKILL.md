---
name: wayfinder
description: Plan a huge chunk of work (more than one agent session can hold) as a shared map of decision tickets on your issue tracker, and resolve them one at a time until the way to the destination is clear.
disable-model-invocation: true
---

An idea has arrived that is too big for one agent session, and the way from here to its **destination** isn't visible yet. This skill charts that way as a **shared map** on the repo's issue tracker, then works its **decision tickets** (questions whose resolution is a decision, not slices of a build) one at a time until the route is clear.

The destination varies per effort, and naming it is the first act of charting: it shapes every ticket. It might be a spec to hand off and iterate on, a decision to lock before planning starts, or a change made in place like a data-structure migration. The map is domain-agnostic: engineering work, course content, whatever fits the shape.

## Plan, don't do

Wayfinder is **planning** by default: each ticket resolves a decision, and the map is done when the way is clear, with nothing left to decide before someone goes and does the thing. The pull to just do the work is usually the signal you've reached the edge of the map and it's time to hand off. An effort can override this in its **Notes**, carrying execution into the map itself, but absent that, produce decisions, not deliverables.

## Refer by name

Every map and ticket is an issue, so it has a **name**: its title. In everything the human reads (narration, the map's Decisions-so-far), refer to it by that name, never by a bare id, number, or slug. A wall of `#42, #43, #44` is illegible; names read at a glance. The id and URL don't vanish; a name wraps its link, but they ride _inside_ the name, never stand in for it.

Where the map, its tickets, blocking, and frontier queries physically live is tracker-specific. Read the "Wayfinding operations" section of `docs/agents/issue-tracker.md` for how this repo expresses them. If that guide is missing, tell the user to run `/setup-khanra17-skills`.

### The map body

The whole map at low resolution, loaded once per session. Open tickets are **not** listed: they are open child issues, found by query.

```markdown
## Destination

<what reaching the end of this map looks like: the spec, decision, or change this effort is finding its way to. One or two lines; every session orients to it before choosing a ticket.>

## Notes

<domain; skills every session should consult; standing preferences for this effort>

## Decisions so far

<!-- the index: one line per closed ticket, enough to judge relevance, then zoom the link for the detail the ticket holds -->

- [<closed ticket title>](link): <one-line gist of the answer>

## Not yet specified

<!-- see "Fog of war": in-scope fog you can't ticket yet; graduates as the frontier advances -->

## Out of scope

<!-- see "Out of scope": work ruled beyond the destination; closed, never graduates -->
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

A session **claims** a ticket by assigning it to the dev driving the map, **first**, before any work, so concurrent sessions skip it. That assignee _is_ the claim: an open, unassigned ticket is unclaimed.

A ticket is **HITL** (worked with a human who speaks for themselves) or **AFK** (driven by the agent alone). A HITL ticket resolves only through that live exchange; the agent never answers the human's side of it.

The answer isn't part of the body; it's recorded on resolution (see [Work through the map](#work-through-the-map)). Assets created while resolving a ticket are linked from the issue, not pasted in.

## Ticket Types

Every ticket is either **HITL** (human in the loop, worked _with_ a human who speaks for themselves) or **AFK**, driven by the agent alone. A HITL ticket only resolves through that live exchange; the agent never stands in for the human's side of it (a grilling agent that answers its own questions has broken this).

**Fog or ticket?** The test is whether you can state the question precisely now, whether or not you can answer it now.

## Fog of war

The map is _deliberately_ incomplete: don't chart what you can't yet see. Beyond the live tickets lies the **fog of war**: the dim view of decisions and investigations you can tell are coming but can't yet pin down, because they hang on questions still open. Resolving a ticket clears the fog ahead of it, graduating whatever's now specifiable into fresh tickets, one at a time, until the way to the destination is clear and no tickets remain.

The map's **Not yet specified** section is where that dim view is written down: the suspected question, the area to revisit later. It's the undiscovered frontier _toward_ the destination: everything here is in scope, just not sharp enough to ticket. Write as loosely or as fully as the view allows; it doubles as a signpost for collaborators reading where the effort is headed.

**Fog or ticket?** The test is whether you can state the question precisely now, _not_ whether you can answer it now.

- **Ticket when** the question is already sharp, even if it's blocked and you can't act on it yet.
- **Not yet specified when** you can't yet phrase it that sharply. Don't pre-slice the fog into ticket-sized pieces: it's coarser than a ticket, and one patch may graduate into several tickets, or none, once the frontier reaches it.

**Not yet specified** excludes what's already decided (Decisions so far), what's already a live ticket, and what's out of scope (the next section).

## Out of scope

Fog only ever gathers _toward_ the destination. The destination fixes the scope, so work beyond it is **out of scope**: it isn't fog, and it doesn't belong in **Not yet specified**. It gets its own **Out of scope** section on the map: work you've consciously ruled out of _this_ effort. Scope, not sharpness, lands it here.

Out-of-scope work never graduates (the frontier stops at the destination), so it returns only if the destination is redrawn, and then as a fresh effort, not a resumption.

Ruling something out of scope is a scoping act, not a step on the route. When a ticket that already exists turns out to sit past the destination (mis-scoped in while charting, or exposed by a resolution), **close it** (a closed ticket is unambiguously off the frontier) and leave one line in the **Out of scope** section: the gist plus why it's out of scope, linking the closed ticket. It stays out of **Decisions so far**, which records the route actually walked; a scope boundary isn't a step on it.

## Invocation

Two modes. Either way, **never resolve more than one ticket per session**, with the exception of research tickets.

### Chart the map

User invokes with a loose idea.

1. **Name the destination.** Invoke the `grilling` skill (with `glossary` and `adr` as terms and decisions settle) to pin down what this map is finding its way to.
2. **Map the frontier.** Grill again, breadth-first: fan out across the whole space, surfacing the open decisions and the first steps takeable now. If this surfaces no fog (the way is already clear and the whole journey fits one session), the effort needs no map: stop and ask the user how they'd like to proceed.
3. **Create the map**: Destination and Notes filled in, Decisions so far empty, the fog sketched into Not yet specified.
4. **Create the tickets you can specify now** as child issues, then wire blocking edges in a second pass (issues need ids before they can reference each other).
5. **Start the research.** For each `research` ticket on the frontier, claim it, then dispatch a subagent with a fresh context window that follows the `research` skill, in parallel. Post each full cited report as the ticket's resolution comment, close the ticket, and link it from the map. Then handle what the answers surfaced as in step 5 of Work through the map.
6. Stop. Charting is one session's work, and every non-research ticket waits for its own session.

### Work through the map

User invokes with a map (URL or number). A ticket is **optional**: without one, you pick the next decision, not the user.

1. Load the map body, not every ticket.
2. Choose the ticket: the one the user named, otherwise the first on the frontier. Claim it before any work.
3. Resolve it. Fetch the full body of any related or closed ticket when you need its detail, and invoke the skills the map's Notes name. With no guidance there, invoke `grilling`.
4. Record the resolution: post the answer as a resolution comment, close the issue, and append its gist and link to Decisions so far.
5. Update the map: create and wire newly surfaced tickets, graduate any fog the answer made specifiable, rule out of scope any ticket the answer shows to sit beyond the destination, and update or close tickets the decision invalidated.

The user may run unblocked tickets in parallel, so expect other sessions to be editing the tracker concurrently.
