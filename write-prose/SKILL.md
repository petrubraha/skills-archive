---
name: write-prose
description: Punctuation and style rules for any human-readable text - never use the em dash. Use whenever writing comments, docs, specs, logs, error messages, commit messages, UI text, or replies to the user.
metadata:
  version: "0.0.1"
---

# Write Prose

This skill defines style rules for any text a human reads: comments, docstrings, documentation, specs, logs, error messages, commit messages, user interface text, and replies. The rules are project, language, and framework agnostic.

## Rules

- **No em dash:** never use the em dash (`—`). Use a colon, a comma, parentheses, or a separate sentence instead.

```text
# Wrong behaviour.
The cache is rebuilt on startup — this takes a few seconds.

# Correct behaviour.
The cache is rebuilt on startup, which takes a few seconds.
```
