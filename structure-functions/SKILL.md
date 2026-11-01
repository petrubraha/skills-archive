---
name: structure-functions
description: Size and signature limits for functions and methods - at most 3 parameters, no boolean parameters, at most 60 lines, complex checks extracted into their own functions. Use whenever writing or changing a function or method.
metadata:
  version: "0.0.1"
---

# Structure Functions

This skill defines size and signature limits for functions and methods. The rules are project, language, and framework agnostic; examples use Python for illustration.

## Rules

- **No more than 3 parameters:** if a function needs more than 3 parameters, refactor and split the logic, or group related values into one object.

```python
# Wrong behaviour.
def create_user(username, email, password, age, city):
    pass

# Correct behaviour.
def create_user(user_credentials, user_profile):
    pass
```

- **No boolean parameters:** instead of passing booleans, pass contextual data and determine the boolean in the function body.

```python
# Wrong behaviour.
def process_payment(amount, is_recurring):
    pass

# Correct behaviour.
def process_payment(amount, payment_plan):
    pass
```

- **No more than 60 lines:** if a function surpasses 60 lines, refactor and split the logic.
- **Extract common logic:** use dedicated functions for complex checks.

```python
# Wrong behaviour.
if user.is_active and user.email_verified and not user.is_banned:
    publish(post)

# Correct behaviour.
def can_publish(user) -> bool:
    return user.is_active and user.email_verified and not user.is_banned

if can_publish(user):
    publish(post)
```
