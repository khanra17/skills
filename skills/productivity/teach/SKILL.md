---
name: teach
description: Explain a concept plainly or teach a topic over several sessions with practical lessons and a learning record.
disable-model-invocation: true
argument-hint: "What would you like to understand or learn?"
---

# Teach

Help the user understand something and, when they want practice, learn to use it. This applies to everyday life as well as technical subjects.

## Choose the kind of teaching

Use the request and conversation to distinguish:

- **An explanation now:** answer in the conversation. No workspace, files, or surprise quizzes.
- **Learning over several sessions:** use a teaching workspace, short lessons, practice, and records that let the next session continue.

An existing teaching workspace is a reason to resume it when the user asks for another lesson, not to turn every question into a new lesson. If the intended scope is unclear, ask whether they want an explanation or ongoing lessons.

## Explain plainly

Start with the smallest complete explanation that answers the question. Say what the thing is, how it works, and why it matters to the user. Walk through a concrete example instead of listing facts or names without connecting them.

Use plain spoken English, short sentences, and one name per concept. Define unfamiliar words when they first appear. Skip what the conversation shows the user already understands. Infer their starting point from the conversation; ask only about a gap that affects what you should teach.

Give the first useful layer, then let the user respond. Go deeper where they ask. Don't announce teaching techniques, demand a paraphrase, or add stock phrases about the "key insight." When there is no live exchange, deliver a complete explanation at the requested depth.

Use a diagram, demonstration, or worked example when it explains more clearly than prose. Build complex pictures in stages rather than showing every moving part at once. Choose a medium available in the environment; a simple point needs no diagram.

Distinguish verified facts, interpretations, and uncertainty. Simplifying the wording must not turn a possible explanation into a certain one. For code or an existing artifact, inspect the relevant material before explaining its behavior or claiming why it was designed that way. Explanation alone does not authorize changing it.

## Teaching workspace

For ongoing learning, use the directory the user chose. If none was chosen, confirm the location before writing. All learning files below belong to that workspace, never to the installed skill directory. The format links in this skill refer to bundled instructions, not output locations.

Read the existing mission, preferences, and relevant learning records before planning a lesson. Create files only when there is content to put in them:

- `MISSION.md`: why the user is learning, their starting point, constraints, and observable goals. See [MISSION-FORMAT.md](./MISSION-FORMAT.md).
- `RESOURCES.md`: annotated trusted sources and optional communities. See [RESOURCES-FORMAT.md](./RESOURCES-FORMAT.md).
- `lessons/0001-topic.html`: numbered lessons, each teaching one tightly scoped thing.
- `reference/`: printable HTML cheat sheets, procedures, examples, and other material useful across lessons.
- `learning-records/0001-topic.md`: demonstrated understanding, stated prior knowledge, corrected misconceptions, and changes that affect future teaching. See [LEARNING-RECORD-FORMAT.md](./LEARNING-RECORD-FORMAT.md).
- `assets/`: shared lesson styles and components.
- `GLOSSARY.md`: understood topic terms, when a glossary is useful. See [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md).
- `NOTES.md`: the user's teaching preferences and relevant working notes.

Use one mission per workspace. Different unrelated topics belong in separate learning workspaces. No engineering setup or project glossary skill is required.

## Ground the lesson

Every lesson should serve the mission. If the goal or starting knowledge is missing, ask enough to establish what the user wants to be able to do and where they are starting. Keep the mission short. Confirm with the user before changing it.

Choose the next lesson from the mission, the user's request, and their learning records. It should be challenging enough to require effort but close enough to their current ability to be achievable.

Find trusted sources for the next lesson, not a large resource library before teaching anything. Reuse suitable entries in `RESOURCES.md`. Prefer primary sources, authoritative guidance, and recognized experts. Verify the factual and procedural claims the lesson depends on; don't invent a procedure when the source is missing. Cite the supporting sources where the claims are taught and say when something could not be verified.

Teach only the background knowledge needed for the next practical step. Clear explanations support understanding; useful practice builds retention.

## Build and use the lesson

A lesson teaches one thing tied to the mission and gives the user one tangible win. Write a short, readable HTML lesson in `lessons/`, using the next sequential number. It should be easy to open locally and print. Open it for the user when possible.

Reuse existing assets. Create a shared stylesheet with the first HTML lesson so the course stays visually consistent. Add another reusable component when a lesson needs it; don't build a component library ahead of the lessons. Lessons may use relative links to local assets, references, and other lessons.

Each lesson should include:

- A plain explanation and a concrete example.
- A relevant exercise or real-world action, with feedback the learner can use.
- Citations and one recommended trusted source to explore further.
- An invitation to ask follow-up questions.

Match practice to the topic. Cooking may need a real-world task; a language lesson may need recall or a short conversation. Use quizzes when they serve the lesson, not as a compulsory ending to every exchange. Keep options comparable in detail and presentation so formatting does not give away the answer; vary the correct answer's position. Feedback should explain the result, not only mark it right or wrong.

For retention, revisit earlier material over later lessons and mix related skills when useful. Spacing is a teaching choice here, not an automatic calendar or reminder service. Don't treat an explanation that felt easy to follow as evidence of mastery.

After practice, record what was demonstrated or what the user reported, keeping that distinction clear. Merely generating a lesson is not evidence that it was completed or learned. Use the result to choose between more explanation, practice, review, or a new lesson. When the mission's goals have been met, say so rather than extending the course indefinitely.

## Reference and real-world practice

Keep reusable knowledge out of long lesson narratives: add or update a concise reference when it will help across lessons. Add terms to the workspace glossary as they become understood, and use that vocabulary consistently without dropping explanations the user still needs.

For judgment that benefits from real experience, offer a practical way to try the skill and get feedback. A trusted community, class, or practitioner can help, but joining one is optional. Respect the user's budget and preferences, and record an opt-out so it is not repeatedly suggested.
