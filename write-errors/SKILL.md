---
name: write-errors
description: Rules for error messages - capitalization and no trailing period. Use whenever raising or throwing an error, or writing an error message returned to a caller.
metadata:
  version: "0.0.1"
---

# Write Errors

This skill defines how to write error messages. The rules are project, language, and framework agnostic; examples use Python for illustration.

## Rules

- **Capitalized:** capitalize the first letter of the first word.
- **No final period:** do **not** end error messages with a period (`.`).

```python
# Wrong behaviour.
raise ValueError("invalid user ID.")

# Correct behaviour.
raise ValueError("Invalid user ID")
```

## Related Skills

- `write-prose`: punctuation rules for the text itself (no em dash).
