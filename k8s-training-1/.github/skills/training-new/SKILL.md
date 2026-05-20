---
name: training-new
description: >-
  Create a complete new training course on any technical topic. Orchestrates the full
  creation workflow: gather topic brief, scaffold all days using @training-day-generator,
  validate labs with @training-lab-validator, check consistency, and review content.
  Use when the user says "create a training on X", "build a new course on X", or
  "scaffold a N-day training about X".
user-invocable: true
---

# Skill: training-new

Create a complete, consistent training course from a topic brief.

## What This Skill Does

1. Collects a structured topic brief from the user
2. Scaffolds all training artifacts for each day using `@training-day-generator`
3. Validates each lab with `@training-lab-validator`
4. Checks cross-file consistency with `@training-consistency-checker`
5. Reviews content accuracy with `@training-content-reviewer`
6. Prints a final manifest of all created files and any outstanding issues

## Step 1 — Collect the Brief

Before generating anything, confirm these inputs:

```
Topic:            [e.g., "ArgoCD and GitOps", "HashiCorp Vault for Kubernetes", "Istio Service Mesh"]
Number of days:   [1–10]
Week label:       [e.g., "Week 1 / GitOps Fundamentals"]
Target audience:  [beginner / intermediate / advanced, default: mixed software engineers]
Prerequisites:    [what students must already know]
Day topics:       [list each day's focus — can be brief: "Day 1: Install + first app, Day 2: ..."]
```

If any of these are missing, ask before proceeding. Do not generate with ambiguous inputs.

## Step 2 — Scaffold Each Day

For each day, invoke `@training-day-generator` with:
- Day number
- Week label
- Topic brief for that day
- Prerequisites (mention what was covered in prior days)

The generator produces 8 artifacts per day:
- `slides/day-N-topic.md`
- `slides/day-N-speaker-notes.md`
- `labs/labN/README.md`
- `labs/labN/*.yaml` (manifests)
- `labs/labN/labN-verify.sh`
- `solutions/labN-solution.md`
- `self-study/day-N.md`
- `assessments/day-N-quiz.md` + `assessments/answers/day-N-answers.md`

## Step 3 — Validate Labs

After all days are scaffolded, invoke `@training-lab-validator` for each lab directory:

```bash
# Example: validate lab for day 1
@training-lab-validator labs/lab01/
```

Collect all ❌ ERROR findings. These must be fixed before proceeding.

## Step 4 — Consistency Check

Invoke `@training-consistency-checker` on the full set of generated files:

```bash
@training-consistency-checker
```

Fix all reported inconsistencies (mismatched headings, broken references, naming violations).

## Step 5 — Content Review

Invoke `@training-content-reviewer` for each day's slides and lab:

```bash
@training-content-reviewer Day 1
@training-content-reviewer Day 2
...
```

Flag all CRITICAL findings for immediate resolution. WARN findings are advisory.

## Step 6 — Final Manifest

Print a summary table:

```
TRAINING CREATED: "ArgoCD and GitOps" (3 days)
================================================

Day 1: ArgoCD Installation & First App
  slides/day-01-argocd-intro.md            ✅ 14 slides
  slides/day-01-speaker-notes.md           ✅ 14 sections
  labs/lab01/README.md                     ✅ 4 tasks, 90 min
  labs/lab01/deployment.yaml               ✅
  labs/lab01/lab01-verify.sh                ✅
  solutions/lab01-solution.md              ✅
  self-study/day-01.md                     ✅
  assessments/day-01-quiz.md               ✅ 6 MC, 3 SA

Day 2: ...

Validation:    ✅ 0 lab errors
Consistency:   ⚠️  2 warnings (non-blocking)
Content:       ✅ 0 critical errors

Total files:   27
Ready for:     delivery (address 2 warnings before final publish)
```

## Rules

- Do not start generating until the brief is confirmed.
- Generate days sequentially — each day's prerequisites reference prior days.
- Do not skip the validation, consistency, and review steps.
- If a step produces CRITICAL/ERROR findings, pause and fix before moving to the next step.
- All filenames must follow `CONVENTIONS.md` naming rules.
