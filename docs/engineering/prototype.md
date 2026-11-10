# prototype

## What it does

`prototype` builds throwaway code to answer one design question. It has two branches:

- **Logic or state model:** one self-contained HTML file with the state on show, a button per action, and guided scenarios. It opens by double-click, so a non-developer can drive it.
- **UI direction:** three structurally different variants of one page or screen, switched from a floating bar that exists only in development builds.

When the question is answered, it records the verdict and the evidence (screenshots for appearance, recordings for interaction or timing, the scenarios and a model snippet for logic) on the issue or spec, then removes the prototype code. The chosen direction is rebuilt under normal production standards.

## When to reach for it

Type `/prototype`, or let the agent reach for it, when talking can't settle how something should behave or look.

Use [diagnosing-bugs](./diagnosing-bugs.md) when existing behavior is broken, and [implement](./implement.md) when the design is settled.

## Common questions

**Should I build it in the same session as the planning?**

A small one, yes: the planning conversation is what defines the question. If building it would crowd that conversation's context, use [handoff](../productivity/handoff.md) to fork it into a fresh session and bring the verdict back.

**Why do the UI variants go on an existing page?**

Real navigation, data, and density expose problems an isolated mock hides. A new throwaway route is the fallback for something with no page to live in.

**Does it work for mobile or desktop apps?**

Yes. The same approach is applied on the project's native screens, with its own preview or debug variant picker.

## It's working if

- The question being answered is written at the top of the prototype.
- UI variants differ in layout and hierarchy, not only in color or copy.
- After the verdict, the issue or spec holds the decision and its evidence, and the prototype code is gone from the branch.
