---
name: standup
description: Generate standup notes from yesterday's commits
---

## My recent commits
!`git log --oneline --author="$(git config user.name)" --since="2 days ago"`

Summarize these as a short standup: what I did, what's next, any blockers.