<!-- SUMMARY
File: README.md
Topic: Public README for the learning-through-dialogue skill repo
Status: Draft v0.1
Owner: Farhanur Rahaman
Key refs: learning-through-dialogue/SKILL.md
Covers: what the skill is, why, install, behaviour, design notes, credits, license
-->

# Learning Through Dialogue

An AI skill that teaches adults by dialogue instead of lectures.

Most AI answers explain a topic to you. This skill helps you work it out. It asks one question at a time, builds on your answers, brings evidence when you need it, and stays neutral on contested topics. The method comes from Paulo Freire's problem-posing education, in which the teacher and learner investigate a question together and the learner does the thinking.

## How it behaves

- **You ask for dialogue** ("teach me by asking", "help me think this through", "Socratic"): it starts with one question about what you already believe, then alternates between what is right in your answer, what it misses, and the next question.
- **You ask a complex question** (history, philosophy, politics, economics, science, ethics, "why does X happen"): it asks once, in one line, whether you want a direct answer or a dialogue. Your choice holds for the session.
- **You get stuck or say "just tell me":** it gives a short answer and carries on.
- **Factual lookups** are answered directly, with no offer.
- **Sources** are introduced with who they are and what they found, one at a time at most. When it is unsure, it marks the claim *verify* instead of guessing.
- **Contested topics:** it gives the strongest version of each side and holds back its own preference. Settled facts are stated plainly.
- **Closing:** a short summary of what you now understand, plus one optional task to test the idea outside the chat.

A worked example is in [learning-through-dialogue/references/example-dialogue.md](learning-through-dialogue/references/example-dialogue.md).

## Install

The skill follows the open Agent Skills format: a folder with a `SKILL.md` and optional reference files.

- **Claude Code:** copy the `learning-through-dialogue` folder into `~/.claude/skills/` (all projects) or `.claude/skills/` inside a project.
- **Claude.ai:** zip the `learning-through-dialogue` folder and upload it under Settings, Capabilities, Skills. *(Menu names change; check the current Skills docs.)*
- **Other agents that read `SKILL.md` folders:** place the folder in that tool's skills directory.

`SKILL.md` is written to work alone. If a platform does not load the `references/` files, the core behaviour still works.

## Files

```
learning-through-dialogue/
  SKILL.md                         core behaviour
  references/
    freire-method.md               the method, adapted, with its limits
    citations-and-neutrality.md    how to use sources and stay neutral
    example-dialogue.md            a short worked example
```

## Design notes

- The core file is kept short so the rules still hold in a long conversation.
- Dialogue is a default you can leave at any time. It is not a trap.
- Freire worked on adult literacy and political awareness. This is an adaptation for one adult learning one topic with an AI, not his own protocol. The reference file lists the limits, including the evidence that unguided discovery works poorly for complete beginners.
- An AI can cite wrongly. The skill tells the model to mark uncertain sources *verify*, but you should still check any source or figure you plan to rely on.

## Credits

Paulo Freire, *Pedagogy of the Oppressed* (1968) and *Education as the Practice of Freedom* (1967).

## License

MIT. See [LICENSE](LICENSE).
