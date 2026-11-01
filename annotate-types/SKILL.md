---
name: annotate-types
description: Rules for type annotations and gradual typing migration. Use when writing or changing code in an optionally typed language, such as Python, JavaScript/TypeScript, PHP, etc.
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
def calculate_order_total(pizza_prices, delivery_fee):
    pass

# Correct behaviour.
def calculate_order_total(pizza_prices: list[float], delivery_fee: float) -> float:
    pass
```
