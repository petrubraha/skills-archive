---
name: refactor-code
description: Rules for when and how far to refactor existing code. Use when a change requires touching existing code, when facing technical debt, or when asked to refactor.
metadata:
  version: "0.0.1"
---

# Refactor Code

This skill defines when and how far to refactor.

## Rules

- **Plan first:** new code sometimes requires refactoring existing code. Clearly explain your plan first and wait for human review before proceeding.
- **No unasked migrations:** do not start refactoring towards a new architecture unless explicitly told so. Modules or apps planned by an architecture refactor are created only when explicitly requested.
- **No new stacks:** never introduce an alternate framework, backend, or platform alongside the existing one.
- **Local scope:** refactors you start on your own stay local to the code you touch (a function, a class, a module), never app-wide.
- **Raise the bar:** existing technical debt is no excuse to lower your standards; write new code with best practices, and refactor when appropriate within the rules above.

```text
# Wrong behaviour.
Asked to add a delivery notes field to the checkout form, the agent also
moves every form in the app to a new validation layer, without asking.

# Correct behaviour.
The agent adds the field, extracts the duplicated address check it touched
into a helper in the same module, and proposes the app-wide validation layer
as a plan for human review.
```
