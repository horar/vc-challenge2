---
applyTo: "slides/*-speaker-notes.md"
description: >
  K8s training speaker notes authoring standards. Applied to all day-N-speaker-notes.md
  files in slides/. Encodes the narrator-bullet format from CONVENTIONS.md.
---

# Training Speaker Notes Standards

## File Header

```markdown
# Day N — Speaker Notes (Topic Title)

> Slide deck: `slides/day-N-topic.md` | Lab: `labs/labN/README.md`
```

- Title must include the day number and topic name matching the slide deck H1.
- The `>` blockquote cross-references the companion slide deck and lab.

## Per-Slide Section Format

```markdown
---

## Slide: [Title matching the slide deck's ## Slide: heading]

- Narrator bullet — what to say, analogy, or key concept (~45–90 seconds per bullet group)
- Narrator bullet
- Narrator bullet
- Narrator bullet (4–8 bullets per slide section)

**Demo:**
```bash
# Commands shown on screen during this section (omit entire block if no demo)
```
```

## Rules

- `## Slide:` heading text **must match exactly** the corresponding slide deck heading (same text after `## Slide N:` or `## Slide:`).
- `---` dividers separate every slide section.
- Bullets represent narrator speech — analogies, gotchas, emphasis, real-world context.
- 4–8 bullets per slide. Each bullet ≈ one sentence; no paragraph prose.
- No "Talking points (X sec):" blocks — bullets only.
- `**Demo:**` block is optional; include only when live commands are shown.
- Demo commands must be copy-pasteable and tested.
- No slide may be left with zero bullets — add at least "Reinforce the concept on the slide" if needed.

## Tone

- Bullets are written in third person as narration cues, not full-sentence scripts.
- Prefer "Explain that..." or direct bullets ("Pod scheduling happens on the worker node, not the control plane.").
- Include "Gotcha:" or "Common mistake:" prefixed bullets where students reliably get confused.

## Synchronisation Check

Before committing, verify: every `## Slide N:` heading in the deck file has a matching `## Slide:` section in the speaker notes, and vice versa. No orphaned sections.
