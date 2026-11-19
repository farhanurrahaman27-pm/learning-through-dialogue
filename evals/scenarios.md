<!-- SUMMARY
File: evals/scenarios.md
Topic: Test scenarios for the learning-through-dialogue skill, with baseline failures and pass criteria
Status: Draft v0.1
Owner: Farhanur Rahaman
Key refs: ../skills/learning-through-dialogue/SKILL.md
Covers: how to run, 8 scenarios, known gaps
-->

# Evals

Small behaviour checks for the skill. Run them again after any edit to `SKILL.md`, because wording changes can quietly break a rule.

## How to run

1. In a fresh session with the skill installed (or by telling a model to read `SKILL.md` first), send the **Input** of a scenario.
2. For scenarios marked "transcript", give the earlier turns as context and ask for the next assistant reply only.
3. Run each scenario at least three times and read every reply. One sample can mislead.
4. Compare with a run **without** the skill. If the plain model already passes, the scenario is not testing the skill.

## Scenarios

### 1. Complex question gets the offer
- **Input:** "Why does ice float on water? I want to really understand it."
- **Pass:** the whole reply is one line offering a direct answer or a dialogue. No explanation.
- **Seen without the skill:** a long essay with no offer, and figures given without any *verify* flag.

### 2. Explicit dialogue request
- **Input:** "I want to learn how inflation works. Teach me by asking me questions, not by lecturing."
- **Pass:** one question about what the learner already believes or why they care. No content. Reply ends at the question.
- **Seen without the skill:** usually acceptable, so this one mostly guards against regression.

### 3. Stuck learner (transcript)
- **Input:** a dialogue where the learner's last line is "I don't know, just tell me".
- **Pass:** all three parts: the answer in at most four short sentences, one question with a single question mark about the learner's own life, and one line offering direct answers. Uncertain figures marked *verify*.
- **Seen without the skill:** a quiz-style check question framed for a child ("pocket money", "snacks").
- **Variants used:** inflation, fall of the Roman Empire, how vaccines work.

### 4. Factual lookup gets no offer
- **Input:** "What is the capital of Brazil and when was it founded?"
- **Pass:** a short direct answer. No offer, no dialogue.

### 5. Asked for the model's own opinion on a contested topic (transcript)
- **Input:** a dialogue about capitalism versus socialism where the learner asks "what's YOUR opinion, which is better?"
- **Pass:** holds back its own preference and says why, offers the strongest case for each side, asks one question, assumes nothing about the learner's country.
- **Seen with an early version of the wording:** assumed the learner's country. Fixed by telling the skill to use only what the learner has said.

### 6. Reply language follows the learner
- **Input A:** a complex question written in Bangla. **Pass:** the one-line offer, in Bangla.
- **Input B (transcript):** a Bangla dialogue where the learner has just answered. **Pass:** next turn in Bangla, in the same shape as an English turn.
- **Result so far:** A passed. B passed on language and shape, but the first run ended with two questions. After the fix in scenario 8, B passed in a re-run.

### 8. An ordinary turn has one question
- **Input (transcript):** a dialogue where the learner has just given their first answer, for example "I think the moon's phases are Earth's shadow, we learned it in school".
- **Pass:** says what is right, adds one thing that is missing, and ends with exactly one question mark. Run it in English and in Bangla.
- **Seen before the fix:** replies that joined two questions into one turn.

### 7. Neutrality without false balance
- **Input:** a learner asks whether a well-established scientific finding "has two sides".
- **Pass:** states the settled fact plainly and does not invent a second side.
- **Status:** not yet run.

## Known gaps

- Every scenario is a single reply. Long dialogues, where a model can drift back into lecturing after many turns, are not covered.
- Tested with one model family only. Smaller or different models may follow the rules less well.
- Whether the skill loads at all for a given prompt depends on the platform's skill matching, which these scenarios cannot test.
