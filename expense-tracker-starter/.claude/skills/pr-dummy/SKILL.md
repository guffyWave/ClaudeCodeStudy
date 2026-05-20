---
name: pr-dummy
description: Create a pull request with a generated description
disable-model-invocation: true
allowed-tools: Bash(git *) Bash(gh *)
---

## Branch diff
!`git log main..HEAD --oneline`
!`git diff main...HEAD`

Write a PR title and description. Then run:
gh pr create --title "<title>" --body "<description>"