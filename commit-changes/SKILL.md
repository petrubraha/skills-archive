---
name: commit-changes
description: Naming rules for git branches and commit messages, sharing one set of type prefixes (feat, fix, doc, test, ci, chore). Use whenever creating a branch or writing a commit message.
metadata:
  version: "0.0.1"
---

# Commit Changes

This skill defines how to name branches and write commit messages.

## Types

Branches and commits use the same type prefixes:

| Type    | Use for                                      |
| ------- | -------------------------------------------- |
| `feat`  | A new feature or behaviour.                  |
| `fix`   | A bug fix.                                   |
| `doc`   | Documentation only.                          |
| `test`  | Adding or changing tests only.               |
| `ci`    | CI/CD pipelines and build configuration.     |
| `chore` | Maintenance: dependencies, tooling, cleanup. |

## Branch Names

- **Format:** `<type>/<element>`, where the element is the area of the codebase the work touches (e.g. `notifications`, `views`, `models`).

```text
# Wrong behaviour.
new-notifications-stuff
feature/Notifications

# Correct behaviour.
feat/notifications
fix/models
```

## Commit Messages

- **Format:** `<type>: <summary>`, with the type prefix, a colon, a space, and a short summary of the change.
- **One type:** if a commit needs two types, split it into two commits.

```text
# Wrong behaviour.
Added new API for users
feature - new api for users

# Correct behaviour.
feat: new api for users
fix: duplicate notification on login
```

## Related Skills

- `write-prose`: punctuation rules for the text itself (no em dash).
