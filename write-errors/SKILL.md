---
name: write-errors
description: Style rules for error messages. Use whenever raising or throwing an error, or writing an error message returned to a caller.
metadata:
  version: "0.0.1"
---

# Write Errors

This skill defines how to write error messages. Examples use Python, but the rules apply to any language.

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
