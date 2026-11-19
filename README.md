<!-- SUMMARY
File: README.md
Topic: Public README for the learning-through-dialogue skill repo
Status: Draft v0.1
Owner: Farhanur Rahaman
Key refs: skills/learning-through-dialogue/SKILL.md
Covers: what the skill is, why, install, behaviour, design notes, credits, license
-->

# Learning Through Dialogue

An AI skill that teaches adults by dialogue instead of lectures.

Most AI answers explain a topic to you. This skill helps you work it out. It asks one question at a time, builds on your answers, brings evidence when you need it, and stays neutral on contested topics. The method comes from Paulo Freire's problem-posing education, in which the teacher and learner investigate a question together and the learner does the thinking.

## Example

A shortened, illustrative exchange:

> **You:** Why does ice float on water?
>
> **AI:** Want a direct answer, or shall we work through it by dialogue?
>
> **You:** Dialogue.
>
> **AI:** Start with what you already think. Why do you believe ice floats, and where did you pick that idea up?
>
> **You:** Because ice is lighter than water. I think we learned it in school.
>
> **AI:** Right, floating means being lighter in the sense of less mass in the same space. But it is the same water before and after freezing, so the amount did not change. Here is a case from your kitchen: a full, sealed bottle of water left in the freezer often cracks. What does that tell you about the ice compared with the water it came from?

The full version, with a stuck learner and a closing step, is in [example-dialogue.md](skills/learning-through-dialogue/references/example-dialogue.md).

## How it behaves

- **You ask for dialogue** ("teach me by asking", "help me think this through", "Socratic"): it starts with one question about what you already believe, then alternates between what is right in your answer, what it misses, and the next question.
- **You ask a complex question** (history, philosophy, politics, economics, science, ethics, "why does X happen"): it asks once, in one line, whether you want a direct answer or a dialogue. Your choice holds for the session.
- **You get stuck or say "just tell me":** it gives a short answer and carries on.
- **Factual lookups** are answered directly, with no offer.
- **Sources** are introduced with who they are and what they found, one at a time at most. When it is unsure, it marks the claim *verify* instead of guessing.
- **Contested topics:** it gives the strongest version of each side and holds back its own preference. Settled facts are stated plainly.
- **Closing:** a short summary of what you now understand, plus one optional task to test the idea outside the chat.

## Install

The skill follows the open Agent Skills format: a folder with a `SKILL.md` and optional reference files.

- **Claude Code plugin (easiest):** run these two commands in Claude Code.
  ```
  /plugin marketplace add farhanurrahaman27-pm/learning-through-dialogue
  /plugin install learning-through-dialogue@learning-through-dialogue
  ```
- **Claude Code, manual:** copy the `skills/learning-through-dialogue` folder into `~/.claude/skills/` (all projects) or `.claude/skills/` inside a project.
- **Claude.ai:** zip the `skills/learning-through-dialogue` folder and upload it under Settings, Capabilities, Skills. *(Menu names change; check the current Skills docs.)*
- **Other agents that read `SKILL.md` folders:** place the folder in that tool's skills directory.

`SKILL.md` is written to work alone. If a platform does not load the `references/` files, the core behaviour still works.

## Files

```
.claude-plugin/
  plugin.json                      plugin manifest
  marketplace.json                 lets Claude Code install it from this repo
skills/learning-through-dialogue/
  SKILL.md                         core behaviour
  references/
    freire-method.md               the method, adapted, with its limits
    citations-and-neutrality.md    how to use sources and stay neutral
    example-dialogue.md            a short worked example
evals/
  scenarios.md                     behaviour checks to re-run after any edit
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
