---
name: design-code
description: Core code design rules (modularity, DRY, magic numbers, etc.). Use whenever writing or reviewing source code.
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
# Wrong behaviour (format_price already exists in the codebase).
def format_order_total(total_cents):
    return f"{total_cents / 100:.2f} EUR"

# Correct behaviour.
from ..utils.money import format_price
```

- **One step per line:** declare each intermediate value in a named variable, then pass it on, instead of nesting calls inline. It reads top to bottom and keeps indentation shallow; new refactors follow it.

```python
# Wrong behaviour.
kitchen.print_ticket(KitchenTicket(order.id).station, {"status": OrderStatus.CONFIRMED})

# Correct behaviour.
ticket = KitchenTicket(order.id)
update = {"status": OrderStatus.CONFIRMED}
kitchen.print_ticket(ticket.station, update)
```

- **No magic numbers:** always create constants for literals that won't change; inside a class, make them static (class-level) constants.

```python
# Wrong behaviour.
if len(order.pizzas) > 10:
    pass

# Correct behaviour.
# Define constants at the top of the module, after the imports, not just above their first use.
MAXIMUM_PIZZAS_PER_ORDER = 10

...

if len(order.pizzas) > MAXIMUM_PIZZAS_PER_ORDER:
    pass
```
