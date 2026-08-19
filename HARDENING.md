<!-- markdownlint-disable -->

# Hardening Report: y-mehta--vulnalerts/v1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **y-mehta--vulnalerts/v1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/alert.yml references two actions using the mutable branch ref '@master' instead of a pinned 40-character commit SHA. This means a compromised or updated upstream action could silently change the code executed in the workflow. Affected lines: 'uses: actions/checkout@master' and 'uses: y-mehta/vulnalerts@master'.

Locations:

- `.github/workflows/alert.yml:10`
- `.github/workflows/alert.yml:11`

### missing-permissions (severity: medium)

The workflow file .github/workflows/alert.yml has no top-level 'permissions:' key and the single job 'alert' also has no job-level 'permissions:' key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. Explicit minimal permissions should be declared.

Locations:

- `.github/workflows/alert.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `actions/checkout@master` to full SHA `61b9e3751b92087fd0b06925ba6dd6314e06f089 # master`. 2. Pinned `y-mehta/vulnalerts@master` to full SHA `745cd030a84f8602e7aa7b2fd24516ef33196cc9 # master`. 3. Added top-level `permissions: {}` to enforce least-privilege — the workflow only runs a scheduled Slack alert and requires no GitHub token permissions.

