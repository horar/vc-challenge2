---
applyTo: "**"
---

# Conventional Commits

All commit messages in this repository follow the [Conventional Commits](https://www.conventionalcommits.org/) specification.

## Format

```
type(scope)?: subject

optional body

optional footer(s)
```

### Subject line (required)
- Pattern: `type(scope)?: description`
- **type** — one of the types listed below (lowercase)
- **scope** — optional, in parentheses: `feat(labs):` or `feat:`
- **description** — imperative mood, lowercase start, no trailing period
- Maximum **120 characters**

### Body (optional)
- Separated from subject by a **blank line**
- Explains *what* changed and *why* (not how)
- Wrap at 120 characters

### Footer (optional)
- `BREAKING CHANGE: <description>` — for breaking API/interface changes
- `Closes #<n>` / `Fixes #<n>` — links to issues
- Multiple footers on separate lines

## Types

| Type       | Use for                                              |
|------------|------------------------------------------------------|
| `feat`     | New feature or capability                            |
| `fix`      | Bug fix                                              |
| `refactor` | Code restructuring with no behavior change           |
| `docs`     | Documentation only                                   |
| `test`     | Adding or updating tests                             |
| `ci`       | CI/CD pipeline changes                               |
| `chore`    | Maintenance (deps update, tooling, config)           |
| `perf`     | Performance improvement                              |

## Breaking changes

```
feat!: redesign lab verify script interface

BREAKING CHANGE: verify scripts now require a namespace argument.
Pass the target namespace: ./lab01-verify.sh my-namespace
```

## Examples

```
feat(labs): add NetworkPolicy verify check to lab07
```

```
fix(slides): correct kubectl port-forward syntax on day-03

The previous example used deprecated --address flag syntax that
was removed in kubectl v1.28.
```

```
docs: update CONVENTIONS.md with 2-digit file naming rules
```

```
refactor(assessments): extract shared quiz header template

Reduces duplication across all 10 quiz files. No content changes.

Closes #18
```

## What NOT to do

```
# Bad — no type
Update lab README

# Bad — vague
fix stuff

# Bad — past tense
Added new verify script

# Bad — exceeds 120 chars on subject line
feat: add a very long description that goes way beyond the limit and becomes impossible to scan in git log
```
