---
name: write-logs
description: Rules for log messages - standard logging utilities, no sensitive user data, capitalization, and punctuation. Use whenever adding or changing a log statement.
metadata:
  version: "0.0.1"
---

# Write Logs

This skill defines how to write log messages. The rules are project, language, and framework agnostic; examples use Python for illustration.

## Rules

- **Standard utilities:** use the language's or framework's standard logging utilities, not prints.
- **No sensitive data:** never expose sensitive user information (passwords, tokens, personal data); refer to users by ID.
- **Capitalized:** capitalize the first letter of the first word.
- **Final period:** end each log message with a period (`.`).

```python
# Wrong behaviour.
logger.info(f"user password {user.password} changed")

# Correct behaviour.
logger.info(f"Password updated for user {user.id}.")
```

## Related Skills

- `write-prose`: punctuation rules for the text itself (no em dash).
