---
name: training-extend
description: >-
  Add one or more new days to an existing training course. Generates the new day's artifacts
  using @training-day-generator, validates the lab, and checks that the new content integrates
  consistently with the existing training days. Use when the user says "add a day on X",
  "extend the training with Y", or "add Day N about Z to this course".
user-invocable: true
---

# Skill: training-extend

Add new days to an existing training without breaking consistency with what's already there.

## What This Skill Does

1. Reads the existing training structure to understand what's already covered
2. Determines the correct next day number and naming
3. Scaffolds the new day using `@training-day-generator`
4. Validates the new lab with `@training-lab-validator`
5. Checks integration with existing days using `@training-consistency-checker`
6. Reports what was added and any issues found

## Step 1 — Understand the Existing Training

Before generating, read:
- `k8s-training.md` (or equivalent syllabus file) to understand what's already covered
- `CONVENTIONS.md` for naming rules
- The most recent day's artifacts to match style and complexity level

```bash
# What days already exist?
ls slides/day-*.md | grep -v speaker-notes | sort
ls labs/
ls self-study/
ls assessments/day-*-quiz.md | sort
```

Identify:
- The next available day number (N+1 after the last existing day)
- What concepts have already been taught (to correctly set prerequisites and avoid repetition)
- The current week label (to match the new day's header)

## Step 2 — Collect the Brief for the New Day

Confirm these inputs:

```
Day number:     [auto-detected or user-specified]
Topic:          [e.g., "ArgoCD GitOps Workflow", "Vault Secrets Integration"]
Focus:          [2–4 sentence description of what this day teaches]
Lab goal:       [what students will build or configure in the hands-on lab]
Prerequisites:  [auto-detected from existing days + any additional requirements]
```

## Step 3 — Scaffold the New Day

Invoke `@training-day-generator` with:
- The confirmed brief
- Context about what prior days covered (paste the relevant syllabus sections)
- The correct day number and week label

The generator creates the full 8-artifact set for the new day.

## Step 4 — Validate the New Lab

```bash
@training-lab-validator labs/labN/
```

Fix any ❌ ERROR findings before proceeding.

## Step 5 — Consistency Check (Integration)

Run `@training-consistency-checker` targeting the new day and the full repo:

```bash
@training-consistency-checker Day N
```

This checks:
- New speaker notes headings match the new slide deck
- New lab is referenced correctly if the syllabus was updated
- New files follow naming conventions
- Self-study cross-references (lab and quiz) resolve correctly

## Step 6 — Update the Syllabus

After generating, update `k8s-training.md` (or equivalent) to include the new day:
- Add a Day N entry with modules, objectives, and lab references
- Update the course overview table if one exists

## Step 7 — Summary

```
EXTENDED: Added Day 6 — "ArgoCD and GitOps" to existing 5-day training
===========================================================================

New files:
  slides/day-06-argocd-gitops.md           ✅ 16 slides
  slides/day-06-speaker-notes.md           ✅ 16 sections
  labs/lab06/README.md                     ✅ 5 tasks, 90 min
  labs/lab06/application.yaml              ✅
  labs/lab06/appproject.yaml               ✅
  labs/lab06/lab06-verify.sh                ✅
  solutions/lab06-solution.md              ✅
  self-study/day-06.md                     ✅
  assessments/day-06-quiz.md               ✅ 7 MC, 3 SA
  assessments/answers/day-06-answers.md    ✅

Updated:
  k8s-training.md                         ✅ Day 6 added to syllabus

Validation:  ✅ 0 lab errors
Consistency: ✅ 0 issues
```

## Rules

- Always read existing days before generating — avoid repeating covered concepts.
- Day numbers must be sequential with no gaps.
- If extending a Week 1 training into a Week 2, note the style difference (see `slides/template.md`): Week 2 uses `## Slide N:` with `---` separators.
- Update the syllabus file after generating — the training is incomplete without it.
