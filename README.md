# Description

Zadanie 2

## Setup & Run

- env. variables:
  - required `COPILOT_GITHUB_TOKEN`
  - optional `COPILOT_HOME`

- export required variables or auto-load `.auth.env` on user's shell start
- when COPILOT_HOME is defined, the CLI redirects the creation and reading of user configuration files:
  ```bash
  export COPILOT_HOME="<CLONED-DIR>/.copilot"

  e.g. in this repo checkout:

  ```bash
  export COPILOT_HOME="$PWD/.copilot" && echo $COPILOT_HOME
  ```

## Purpose

Base for k8s training material (WIP).
