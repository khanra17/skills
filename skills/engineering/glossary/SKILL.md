---
name: glossary
description: Build and sharpen a project's domain glossary. Use when resolving ambiguous or conflicting domain terminology, or creating or editing GLOSSARY.md or GLOSSARY-MAP.md.
---

# Glossary

Build and sharpen the project's domain model as you design: challenge terms, invent edge-case scenarios, and write resolved terms down the moment they are settled. This skill is for changing the model. Reading `GLOSSARY.md` for vocabulary needs no skill.

Most repos have one `GLOSSARY.md` at the root. A root `GLOSSARY-MAP.md` means the repo has several contexts, each with its own glossary. [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md) has the entry format, both layouts, and how to pick the right glossary. Create files lazily: the first `GLOSSARY.md` appears when the first term is resolved.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `GLOSSARY.md`, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y. Which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. "You're saying 'account': do you mean the Customer or the User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it: "Your code cancels entire Orders, but you just said partial cancellation is possible. Which is right?"

### Update GLOSSARY.md inline

When a term is resolved, update the relevant `GLOSSARY.md` right there, one term at a time as each is settled.

`GLOSSARY.md` holds domain terms and their definitions only. Implementation details, specs, and decisions belong in the code, the spec, and ADRs.
