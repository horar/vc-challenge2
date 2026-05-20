---
applyTo: "slides/**/*.md"
description: >
  K8s training slide deck authoring standards. Applied to all slide deck Markdown files
  in slides/ (day-N-*.md, capstone.md). Encodes the conventions from slides/template.md.
---

# Training Slide Deck Standards

## File Header

Every slide deck opens with:
```markdown
# Day N — Topic Title
**Week N / Module tag**
```

- `#` H1 is the only H1 in the file — it is the deck title.
- Include a week/module tag on the line immediately after the H1.

## Slide Structure (Week 2 canonical format)

```markdown
---

## Slide N: Descriptive Title
**Section label (optional)**
- Bullet 1
- Bullet 2
- Bullet 3
**Callout or key takeaway**
- Key insight or result
```

### Rules

- `---` separates every slide. One blank line before and after each `---`.
- `## Slide N:` opens each slide. Numbers are sequential within the deck.
- Bullets carry actual content — 3–6 per slide, one idea per bullet.
- `**Bold label**` introduces logical sub-sections within a slide (replaces sub-headings).
- No inline `Note:` or `Speaker:` lines — speaker notes go in `day-N-speaker-notes.md`.
- Code blocks: keep inline snippets ≤ 8 lines; put longer examples on a dedicated slide.
- No nested bullet lists deeper than two levels.

## Week 1 Legacy Format

`day-01-intro.md` through `day-05-observability-delivery.md` and `capstone.md` use:
- `## Slide: Title` (no number)
- Inline `Note:` lines
- No `---` separators between slides

These files remain valid as-is. **New content and revisions must use the Week 2 format.**
When editing a Week 1 file: keep its existing format unless the whole deck is being rewritten.

## Naming

- Deck files: `slides/day-N-topic-slug.md` (e.g., `day-06-cluster-bootstrap.md`)
- Speaker notes companion: `slides/day-N-speaker-notes.md` (same N)
- Capstone: `slides/capstone.md` (Week 1) or `slides/day-10-production-capstone.md` (Week 2)

## Content Guidelines

- Every slide should have a single, clear teaching point — avoid "overview" slides that list too many concepts.
- The first slide after the title should orient: what problem does today solve?
- The last slide should recap objectives met and point to the lab.
- Acronyms: spell out on first use (e.g., "Container Network Interface (CNI)").
- CLI commands on slides: show only the command, not full terminal output; output goes in speaker notes or labs.
