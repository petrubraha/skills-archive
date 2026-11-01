---
name: write-prose
description: Punctuation and style rules for any human-readable text. Use whenever writing comments, docs, commit messages, etc.
metadata:
  version: "0.0.1"
---

# Write Prose

This skill defines style rules for any text a human reads:

- comments and docstrings
- documentation and specs
- logs and error messages
- commit messages
- user interface text
- replies to the user

## Rules

- **No em dash:** never use the em dash (`—`). Use a comma, a colon, a separate sentence, etc. instead.

```text
# Wrong behaviour.
The cache is rebuilt on startup — this takes a few seconds.

# Correct behaviour.
The cache is rebuilt on startup, which takes a few seconds.
```

- **Short enumerations:** an inline enumeration lists at most three items. If more exist, keep three and end with "etc."; if every item is needed, use a bullet list instead.

```text
# Wrong behaviour.
Applies to comments, docstrings, documentation, specs, logs, error messages, and commit messages.

# Correct behaviour: three examples are enough.
Applies to any written text, e.g. docs, specs, code, etc.

# Correct behaviour: every item is needed.
Applies to:
- comments
- docstrings
- documentation
- specs
```
