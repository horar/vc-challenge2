---
applyTo: "assessments/**/*.md"
description: >
  K8s training assessment authoring standards. Applied to quiz files in assessments/
  and answer keys in assessments/answers/.
---

# Training Assessment Standards

## Quiz File Format (`assessments/day-N-quiz.md`)

```markdown
# Day N Quiz — Topic Title

Instructions: Answer all questions. Multiple-choice: circle one answer. Short-answer: 2–3 sentences.

---

## Section 1: Multiple Choice (N points)

**Q1.** Question text?

- A) Option
- B) Option
- C) Option
- D) Option

---

**Q2.** ...

---

## Section 2: Short Answer (N points)

**Q6.** Question text?

---

**Q7.** ...

---

## Section 3: Hands-On / Scenario (optional, N points)

**Q9.** Given this manifest snippet / this error output: ...
What is wrong and how do you fix it?

```yaml
# manifest or error output here
```
```

## Rules

- Every quiz file starts with `# Day N Quiz — Topic Title` (H1).
- `---` divides every question from the next.
- Multiple choice: 4 options (A–D), exactly one correct answer.
- Short answer: open-ended, 2–3 sentence expected length.
- Scenario/hands-on: optional section for days with complex material; include a YAML snippet or `kubectl` output for students to diagnose.

## Question Count & Distribution

| Day type | MC | Short answer | Scenario | Total points |
|---|---|---|---|---|
| Standard day | 5–7 | 2–3 | 0–1 | 10–15 |
| Heavy topic (security, storage) | 6–8 | 3–4 | 1 | 15–20 |

## Difficulty Distribution

- 40% recall (define a term, name a component)
- 40% application (given a scenario, pick the right answer)
- 20% analysis (explain why, debug a config)

Avoid trivia questions. Every question should map to a learning objective from the day's syllabus.

## Answer Key Format (`assessments/answers/day-N-answers.md`)

```markdown
# Day N — Answer Key

> Instructor only — do not distribute to students.

**Q1.** C — Explanation of why C is correct and why distractors are wrong (1–2 sentences).

**Q6.** Expected answer: [complete expected response].
Accept also: [acceptable variants].
Do not accept: [common wrong answers and why].
```

## Naming

- Quiz: `assessments/day-N-quiz.md` (hyphenated, e.g., `day-06-quiz.md`)
- Answer key: `assessments/answers/day-N-answers.md` (hyphenated)
- Both filenames use the same day number.
