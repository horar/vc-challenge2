---
applyTo: "self-study/**/*.md"
description: >
  K8s training self-study guide authoring standards. Applied to all day-N.md files
  in self-study/. Defines the standalone structure for independent learners.
---

# Training Self-Study Guide Standards

## File Header

```markdown
# Day N — Self-Study Guide: Topic Title

> Estimated time: N hours | Lab: `labs/labN/README.md` | Quiz: `assessments/day-N-quiz.md`
```

- H1 must match the format `Day N — Self-Study Guide: Topic Title`.
- The `>` blockquote states estimated total time and cross-references lab and quiz.

## Required Sections (in order)

```markdown
## Prerequisites

- What you should already know or have installed
- ...

## Concepts

### Concept Name

Explanation of the concept. Include:
- What it is (definition)
- Why it matters (motivation)
- Where it fits in the architecture

### Next Concept

...

## Key Commands

```bash
# Annotated command examples — explain what each flag does
kubectl get pods -n demo -o wide    # -o wide: adds node name and IP columns
```

## Lab

This session's lab is **[Lab N — Title]** → `labs/labN/README.md`.

Before starting the lab:
- [ ] Minikube is running (`minikube status`)
- [ ] Correct kubectl context is set (`kubectl config current-context`)
- [ ] [Any other day-specific prerequisite]

## Quiz

Test your understanding → `assessments/day-N-quiz.md`

Focus areas for this day's quiz:
- [2–3 bullet hints at what the quiz covers, without giving answers]

## Further Reading

| Resource | URL | Why it's useful |
|---|---|---|
| Kubernetes docs: Topic | https://kubernetes.io/docs/... | Official reference for X |
| ... | ... | ... |
```

## Rules

- The guide must be **self-contained** — a student with no instructor can follow it alone.
- Concepts section: cover every concept introduced in the day's slide deck.
- Key Commands section: every command a student runs in the lab should appear here with annotation.
- The Lab section checklist must be actionable (`minikube status`, `kubectl config current-context`).
- Further Reading: minimum 2 entries; maximum 5. Prefer official Kubernetes documentation over blog posts.
- No inline answers to quiz questions.
- Tone: direct, instructional. Address the reader as "you". Avoid passive voice.

## Naming

Files: `self-study/day-N.md` (e.g., `self-study/day-06.md`) — no topic slug in the filename.

## Length Guidelines

| Section | Target length |
|---|---|
| Prerequisites | 3–6 bullets |
| Concepts | 300–600 words total across all sub-sections |
| Key Commands | 5–15 annotated commands |
| Lab checklist | 3–5 items |
| Further Reading | 2–5 entries |

Keep guides focused. Depth comes from the lab and further reading, not from the guide prose.
