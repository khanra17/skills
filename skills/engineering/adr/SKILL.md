---
name: adr
description: Record and revise architectural decision records. Use when a significant architectural decision needs documenting or an existing ADR needs updating.
---

# Architectural Decision Records

## File structure

System-wide ADRs live in root `docs/adr/`; context-scoped decisions live in the relevant context's `docs/adr/` directory. Create the directory when the first ADR is written.

## Offer ADRs sparingly

Offer to create an ADR only when all three are true:

1. **Hard to reverse**: the cost of changing your mind later is meaningful
2. **Surprising without context**: a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off**: there were genuine alternatives and you picked one for specific reasons

If any of the three is missing, skip the ADR. Write it in the format in [ADR-FORMAT.md](./ADR-FORMAT.md).

## Revising

When the decision stands and only its wording or detail needs fixing, edit the ADR in place. When the decision itself changes, write a new ADR and mark the old one `superseded by ADR-NNNN`, keeping the old file so the history of the reasoning survives.
