---
name: changelog
description: Generate a changelog from recent commits
---

## Commits since last release
!`git log $(git describe --tags --abbrev=0)..HEAD --oneline`

Write a user-facing changelog entry grouped by: Features, Bug Fixes, Breaking Changes.
Skip chore/internal commits. Use plain language, not commit messages verbatim.