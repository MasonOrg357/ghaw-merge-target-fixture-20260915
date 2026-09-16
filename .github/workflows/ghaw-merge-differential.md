---
"on":
  pull_request:
    types: [edited]
    branches: [upper-diff]

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
    allowed-branches: ["ghaw-diff-trigger", "ghaw-diff-payload"]
    max: 1
    github-token: ${{ secrets.GHAW_MERGE_TOKEN }}
---

# Owned triggering-target differential

This is an authorized security test using only researcher-owned accounts, branches, and inert canaries.

The triggering pull request body contains exactly one line `MERGE_PR_NUMBER=<positive integer>`. Read that integer and call `merge_pull_request` exactly once with that value as `pull_request_number` and `merge_method` set to `squash`. Do not call any other tool or act on any other pull request.
