## What it does

`prototype` builds throwaway code to answer one design question. It has two branches:

- **Logic or state model:** one self-contained HTML file with visible state, free-play actions, and guided scenarios.
- **UI direction:** three radically different variants on one route, selectable through `?variant=` and a development-only switcher.

The prototype skips production hardening so feedback arrives quickly. After the question is answered, the validated decision moves into real code and the prototype is kept on a throwaway branch as a primary source.

## When to reach for it

Type `/prototype`, or let the agent reach for it when conversation alone cannot settle how something should behave or look.

Use [diagnosing-bugs](./diagnosing-bugs.md) when existing behavior is broken. Use [implement](./implement.md) when the design is already settled and needs production code.

## Common questions

**How does it choose between logic and UI?**

The question decides. State transitions, business rules, and data shape use the logic branch. Layout, hierarchy, and visual direction use the UI branch. If the prompt is ambiguous, the skill asks or states its assumption.

**Why is a logic prototype one HTML file?**

It opens without a server or toolchain and can be shared with a non-developer. The decision-making logic remains separate from the DOM so it can later inform the real module.

**Why put UI variants on an existing page?**

Real navigation, data, density, and surrounding layout expose problems that an isolated mock page hides. A new prototype route is the last resort.

**Does prototype code go to production?**

No. The winner is rebuilt or folded into production under normal testing and error-handling expectations. Losing variants and prototype controls stay off main.

**Why use a separate session and handoff?**

A prototype can create a lot of context. [Handoff](../productivity/handoff.md) lets the planning conversation remain intact while another session builds the artifact, then returns the answer.

## It's working if

- The question appears clearly in the prototype.
- A non-developer can drive a logic demo without reading code.
- UI variants differ in structure, not only color or copy.
- Feedback exposes an assumption about the idea.
- Main keeps the validated decision, while the full prototype remains available on its branch.
