---
name: design-code
description: Core code design rules - modularity, single responsibility, strict DRY, one step per line, and named constants instead of magic numbers. Use whenever writing or reviewing source code.
metadata:
  version: "0.0.1"
---

# Design Code

This skill defines the core design rules for all new code. Examples use Python, but the rules apply to any language.

## Rules

- **Ensure modularity:** build small, decoupled units that other features can reuse.
- **Single responsibility:** methods and functions have a single responsibility.
- **Don't repeat yourself (DRY):** this is a very strict rule.
- **Search first:** before writing new logic, search the codebase for an existing implementation. Never add a second copy of an existing feature; reuse it, or consolidate the copies.

```python
# Wrong behaviour (in views/profile_views.py, while utils/phone.py already has format_phone_number).
def format_phone(raw_phone):
    return "+40" + raw_phone.lstrip("0")

# Correct behaviour.
from ..utils.phone import format_phone_number
```

- **One step per line:** declare each intermediate value in a named variable, then pass it on, instead of nesting calls inline. It reads top to bottom and keeps indentation shallow; new refactors follow it.

```python
# Wrong behaviour.
notify_group(ChatRoom(request.user.id).group_name, {"type": EventType.DISCONNECT})

# Correct behaviour.
user_id = request.user.id
user_chat = ChatRoom(user_id)
event = {"type": EventType.DISCONNECT}
notify_group(user_chat.group_name, event)
```

- **No magic numbers:** always create constants for literals that won't change; inside a class, make them static (class-level) constants.

```python
# Wrong behaviour.
if password_length < 8:
    pass

# Correct behaviour.
MINIMUM_PASSWORD_LENGTH = 8
if password_length < MINIMUM_PASSWORD_LENGTH:
    pass
```

## Technology-Specific References

- If working with Django, review the [django reference](./references/django-design.md) file.
