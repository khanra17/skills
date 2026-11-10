# teach

## What it does

`teach` helps you understand a subject or learn to use a skill. It works for cooking, languages, money, music, software, and other topics.

For a question such as "Why does bread dough need to rest?", it explains in the conversation: a short answer first, a concrete example, and more detail where you ask for it.

For a goal such as "I want to cook five affordable meals", it builds a teaching workspace with short lessons, practice, trusted sources, and records that let the next session continue where you stopped.

## When to reach for it

Type `/teach` when you want to understand something, practise a skill, or continue learning a topic over several sessions. Say what you want to learn and, if you know, why.

Use [wait-what](./wait-what.md) when you only want the agent's last message explained again. Use [grill-me](./grill-me.md) to challenge a plan you already have. Use [research](../engineering/research.md) when you want a cited report.

## How ongoing lessons work

Choose a directory for your learning. The skill writes its files there:

| Path | Purpose |
| --- | --- |
| `MISSION.md` | Your goal, starting knowledge, constraints, and what success looks like |
| `RESOURCES.md` | Trusted sources and optional places to get practical feedback |
| `lessons/` | Short, numbered HTML lessons |
| `reference/` | Printable cheat sheets, examples, and procedures |
| `learning-records/` | Demonstrated understanding, stated experience, and corrected misconceptions |
| `assets/` | Shared lesson styling and reusable exercises or diagrams |
| `GLOSSARY.md` | Topic terms you understand, when a glossary is useful |
| `NOTES.md` | Your teaching preferences and relevant working notes |

Files appear when there is something to put in them. Each lesson teaches one useful thing tied to your goal. A cooking course might begin with controlling pan temperature, not with a survey of every cooking method.

The teacher finds sources for that lesson, explains what happens and why, then gives you practice and feedback. An exercise may be an in-browser task, a conversation, or something to try away from the computer. Lessons link to shared assets with relative paths, so move the workspace as a whole.

## Common questions

**Will it quiz me?**

In a lesson, when practice helps: learning unit prices sticks better when you compare two grocery items yourself. A plain explanation in the conversation comes without a quiz unless you ask for one.

**How does it know what I have learned?**

It records what you demonstrated and what you said you already knew, and keeps the two apart. Receiving a lesson is not recorded as having learned it.

**Can I continue in a new session?**

Yes. Open the same workspace and ask for the next lesson. The teacher reads your mission, preferences, and learning records first.

**How does it check what it teaches?**

Lessons cite trusted sources for their claims and recommend one to explore further. The teacher says when it could not verify something. Citations let you check the lesson; they don't guarantee every statement.

**Does it schedule reviews?**

It revisits earlier material inside later lessons. Reminders and calendars are outside what it does.

## It's working if

- A quick question gets an answer in the conversation and creates no files.
- Each lesson leaves you able to do one thing tied to your goal.
- Feedback on practice explains the result, beyond marking it right or wrong.
- A later session picks up from the workspace without re-teaching what the records say you know.
