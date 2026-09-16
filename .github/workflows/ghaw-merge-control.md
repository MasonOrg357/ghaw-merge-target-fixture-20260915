---
"on":
  pull_request:
    types: [edited]
    branches: [upper-control]

permissions:
  contents: read
  copilot-requests: none

engine:
  id: copilot
  version: "1.0.80"
max-turns: 4
timeout-minutes: 10

tools:
  bash: false
  cli-proxy: false
  github: false

safe-outputs:
  merge-pull-request:
    target: triggering
    allowed-branches: ["ghaw-control-trigger"]
    max: 1
---

# Owned triggering-target control

This is an authorized security test using only researcher-owned accounts, branches, and inert canaries.

Call `merge_pull_request` exactly once with `merge_method` set to `squash`. Omit `pull_request_number` so the configured triggering pull request is used. Do not call any other tool or act on any other pull request.
