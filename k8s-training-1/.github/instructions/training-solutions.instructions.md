---
applyTo: "solutions/**/*.md"
description: >
  K8s training solution guide authoring standards. Applied to all labN-solution.md
  files in solutions/. Defines structure, expected output blocks, and common mistakes section.
---

# Training Solution Guide Standards

## File Header

```markdown
# Lab N Solution Guide — Short Title

> Week N / Day N | Lab: `labs/labN/README.md`

## Objectives (recap)

- Action-verb objective restated from the lab README
- ...
```

- H1 must include the lab number and a short title matching the lab README.
- The `>` blockquote cross-references the day and lab README.
- Restate objectives verbatim from the lab README so the solution is self-contained.

## Section Structure

Each lab task gets a numbered section:

```markdown
## Task N: Short Task Title

Brief explanation of what this task does and why (1–2 sentences).

```bash
# Commands to run
kubectl apply -f deployment.yaml
kubectl rollout status deployment/nginx -n demo
```

**Expected output:**
```
deployment.apps/nginx condition met
```

> **Why:** Explain what the command does and what the output means.
```

### Rules

- Every task from the lab README has a corresponding solution section.
- Include **Expected output** blocks for every non-trivial command. Use real output, not placeholder text.
- `> **Why:**` callouts explain the reasoning — not just the "what" but the "why this approach".
- If a task has multiple valid approaches, show the recommended one first, then note alternatives.
- Commands must be copy-pasteable and correct for the supported cluster versions (see `ENVIRONMENT.md`).

## Common Mistakes Section

Every solution guide ends with:

```markdown
## Common Mistakes

| Symptom | Root cause | Fix |
|---|---|---|
| `ImagePullBackOff` | Image name typo or wrong registry | `kubectl describe pod` → check Events section |
| PVC stays `Pending` | No default StorageClass | `kubectl get sc` → verify a StorageClass is marked default |
| ... | ... | ... |
```

Include at least 3 entries. Pull from `TROUBLESHOOTING.md` and `INSTRUCTOR.md` for the day.

## Naming

Solution guide files: `solutions/labN-solution.md` (compact form, no hyphen in `labN`).
Example: `solutions/lab06-solution.md` — **not** `lab-6-solution.md`.

## What Solution Guides Are Not

- Not a full tutorial — assume students attempted the lab first.
- Not a copy of the lab README — don't repeat task descriptions verbatim; provide answers.
- Not exhaustive — cover the happy path plus the 2–3 most common failure modes.
