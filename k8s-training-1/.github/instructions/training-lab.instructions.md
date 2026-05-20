---
applyTo: "labs/**/*.md,labs/**/*.yaml,labs/**/*.yml,labs/**/*.sh"
description: >
  K8s training lab authoring standards. Applied to lab READMEs, Kubernetes manifests,
  and verify scripts inside labs/. Covers format, manifest conventions for instructional
  use, and verify script robustness requirements.
---

# Training Lab Standards

## Lab README Format (`labs/labN/README.md`)

Every lab README must open with:
```
Lab N — Short descriptive title

Duration: XX minutes

Objectives:
- What students will do or learn (action-verb form)
- ...

Pre-requisites:
- What must already be complete or installed
```

Then numbered task sections:
```
Tasks:
N. Task description

```bash
# Commands
```

Expected output (or "you should see"):
...
```

### Rules

- **Duration** is required — use realistic estimates (30 / 60 / 90 / 120 min).
- **Objectives** use action verbs: Deploy, Configure, Verify, Debug, Apply.
- Every task must include the exact commands to run — no "apply the manifest" without showing the command.
- Show expected output for non-trivial commands so students can self-verify.
- Verification command (typically the `lab-verify.sh`) is referenced in the final task.
- No inline solutions — solutions live in `solutions/labN-solution.md`.

## Kubernetes Manifests for Labs

Lab manifests are **intentionally simplified** vs production. The goal is teachability, not prod-readiness.
Still required:
- Correct `apiVersion` and `kind` for the target cluster version (see `ENVIRONMENT.md` compatibility table).
- Explicit `namespace` on every resource (use `demo` or a day-specific namespace).
- `labels:` block with at least `app: <name>` so students can use label selectors.
- Comments explaining non-obvious fields (`# readiness probe — removes pod from Service endpoints on failure`).

Not required in lab manifests (unlike prod):
- `resources.limits/requests` (unless the lab topic is resource management)
- `securityContext` (unless the lab topic is security)
- `readOnlyRootFilesystem` or capability drops

When the lab **intentionally omits** a production best practice, add a comment:
```yaml
# Note: no resource limits — added in Day 3 Module 9
```

## Verify Scripts (`labs/labN/labN-verify.sh`)

Every lab that has a verify script must follow:

```bash
#!/usr/bin/env bash
set -euo pipefail
```

### Required patterns

- **Namespace parameter**: accept `NAMESPACE="${1:-demo}"` so the script is reusable.
- **Trap cleanup**: define a `cleanup()` function and `trap cleanup EXIT` for any background processes (port-forwards, etc.).
- **Meaningful exit codes**: 0 = pass, 2 = tool not found, 3 = cluster not ready, 1 = assertion failed.
- **Informative output**: `echo` progress messages so students know where the script is; print failure reason on stderr before exiting non-zero.
- **Port cleanup**: kill any `kubectl port-forward` background PIDs in the cleanup trap, not with `pkill`.
- **Timeouts**: use `--timeout=120s` on `kubectl rollout status`; do not block indefinitely.

### Avoid

- `kill -9` — use `kill` without a signal for graceful termination.
- `pkill`, `killall`, or name-based process killing — track PIDs explicitly.
- Hardcoded local ports — use a `find_free_port` helper.
- Silent failures — every `if !` check must print why it failed.

## Lab Directory Naming

```
labs/labN/             # e.g., labs/lab01/, labs/lab06/
  README.md
  labN-verify.sh       # verify script (executable, 755)
  *.yaml               # manifests (use descriptive names: deployment.yaml, service.yaml)
```

Do not prefix manifest filenames with the lab number — `deployment.yaml` not `lab01-deployment.yaml`.
