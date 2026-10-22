## What it does

`teach` helps you understand a subject or learn to use a skill. It works for cooking, languages, money, music, software, and other topics.

For a question such as "Why does bread dough need to rest?", it explains in the conversation. It starts with a short answer, uses a concrete example, and adds detail where you ask. It does not create files or give you a surprise quiz.

For a goal such as "I want to cook five affordable meals", it builds a teaching workspace with short lessons, practice, trusted sources, and records that let the next session continue.

## When to reach for it

Type `/teach` when you want to understand something, practise a skill, or continue learning a topic over several sessions. Say what you want to learn and why, if you already know.

Use [wait-what](./wait-what.md) when you only want the agent's last message explained again. Use [grill-me](./grill-me.md) to challenge a plan you already have. Use [research](../engineering/research.md) when you want a cited research document rather than teaching.

## How ongoing lessons work

Choose a directory for your learning. This is where the skill writes its files, not the directory where `/teach` is installed. No engineering setup is required.

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

Files appear when there is something to put in them. Each lesson teaches one useful thing tied to your goal. A cooking course might begin with controlling pan temperature rather than explaining every cooking method at once.

The teacher finds sources for that lesson, explains what happens and why, then gives you suitable practice and feedback. An exercise may be an in-browser task, a conversation, or something to try away from the computer. The HTML lessons use relative links to shared assets, so keep the workspace together when moving it.

## Common questions

**Do I need a workspace for a quick explanation?**

No. Ask the question in your current conversation. A workspace is for learning you want to continue and record across sessions.

**Will it ask lots of questions before teaching me?**

It uses what the conversation already says about your goal and knowledge. It asks only about missing information that affects the teaching. Ongoing learning needs a clear goal and starting point; a simple explanation does not need a mission document.

**Will it quiz me?**

Not during an ordinary explanation unless you ask. Lessons can use exercises or quizzes when practice helps. For example, learning unit prices is more useful when you try comparing two grocery items yourself.

**How does it know what I have learned?**

It records what you demonstrated or what you said you already know, keeping those distinct. Receiving a lesson does not mean you completed it or mastered its contents.

**Can I continue in a new session?**

Yes. Open the same learning workspace and ask for the next lesson or more practice. The teacher reads your mission, preferences, and relevant learning records instead of starting over.

**Does it schedule reviews?**

No calendar or reminder service is built in. It can revisit material during later lessons and choose review or practice instead of adding new material. When you meet the mission's goals, it should say so.

**How does it check what it teaches?**

Lessons use trusted sources, cite the claims they support, and recommend a source to explore further. The teacher must say when it cannot verify something. Citations help you check the lesson; they do not guarantee every statement is correct.

**Do I have to join a community?**

No. A class, community, or practitioner may help when you need real-world feedback. It is optional, and the teacher remembers if you do not want those suggestions.

## It's working if

- The explanation uses words you understand and examples related to your question.
- A quick question stays a conversation rather than becoming a course setup.
- Each lesson leaves you able to do one useful thing tied to your goal.
- Practice receives useful feedback, not just a right-or-wrong label.
- Learning records distinguish material covered from ability demonstrated.
- A later session continues from the workspace without re-teaching what you already know.
