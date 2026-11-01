---
name: name-identifiers
description: Naming rules for variables, functions, and classes - descriptive, suggestive names and no abbreviations. Use whenever declaring or renaming an identifier.
metadata:
  version: "0.0.1"
---

# Name Identifiers

This skill defines how to name variables, functions, and classes. The rules are project, language, and framework agnostic; examples use Python for illustration.

## Rules

- **Descriptive names:** names say what the value is or what the function does.
- **No abbreviations:** spell out every word in local variables, functions, and classes.

```python
# Wrong behaviour.
usr_obj = get_usr(uid)

# Correct behaviour.
user_profile = get_user(user_id)
```
