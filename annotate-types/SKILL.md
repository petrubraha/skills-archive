---
name: annotate-types
description: Type annotation rules - annotate parameters, return values, and variables whenever possible, migrating untyped code gradually. Use whenever writing or changing functions or variables in a language with optional typing (Python, JavaScript/TypeScript, PHP, Ruby).
metadata:
  version: "0.0.1"
---

# Annotate Types

This skill defines how to adopt types in gradually typed code. Examples use Python, but the rules apply to any language with optional typing.

## Rules

- **Gradual migration:** slowly migrate to a typing system; annotate new and touched code, without a big-bang rewrite.
- **Annotate when possible:** annotate parameters, return values, and variables whenever the type is known.

```python
# Wrong behaviour.
def calculate_total(price, tax_rate):
    pass

# Correct behaviour.
def calculate_total(price: float, tax_rate: float) -> float:
    pass
```
