# Writing Agent Briefs

An agent brief records the implementation requirements on an issue marked `ready-for-implementation`, for whoever implements it. The original body and discussion are context; the brief is the contract. It states **what remains to implement**.

## Principles

### Durability over precision

The issue may sit in `ready-for-implementation` for days or weeks while the codebase changes. Write the brief so it survives files being renamed, moved, or refactored: describe interfaces, types, and behavioral contracts, and name the types, function signatures, or config shapes the agent should look for. File paths and line numbers go stale, so leave them out.

### Behavioral, not procedural

Describe what the system should do. The agent will explore the codebase fresh and make its own implementation decisions.

- **Good:** "The `SkillConfig` type should accept an optional `schedule` field of type `CronExpression`"
- **Bad:** "Open src/types/skill.ts and add a schedule field on line 42"

### Complete acceptance criteria

The agent needs to know when it's done. Every criterion is concrete and independently verifiable.

- **Good:** "Running `gh issue list --label needs-triage` returns issues that have been through initial classification"
- **Bad:** "Triage should work correctly"

### Explicit scope boundaries

State what is out of scope, so the agent leaves adjacent features alone.

## Template

```markdown
## Agent Brief

**Category:** bug / enhancement
**Summary:** one-line description of what needs to happen

**Current behavior:**
What happens now. For bugs, the broken behavior.
For enhancements, the status quo the feature builds on.

**Desired behavior:**
What should happen after the work is complete, including edge cases and error conditions.

**Key interfaces:**
- `TypeName`: what needs to change and why
- `functionName()` return type: what it returns now vs what it should return
- Config shape: any new configuration options needed

**Acceptance criteria:**
- [ ] Specific, testable criterion 1
- [ ] Specific, testable criterion 2

**Out of scope:**
- Thing that should stay unchanged in this issue
- Adjacent feature that might seem related but is separate
```
