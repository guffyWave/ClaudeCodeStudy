---
name: security-check
description: Scan recent changes for security issues
disable-model-invocation: true
---

## Changes
!`git diff HEAD`

Review for: SQL injection, XSS, hardcoded secrets, insecure dependencies,
missing auth checks, unvalidated inputs. Flag anything critical.