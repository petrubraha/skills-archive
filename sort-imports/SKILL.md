---
name: sort-imports
description: Import grouping, ordering, and path rules. Use whenever adding, moving, or reordering imports, or resolving circular imports.
metadata:
  version: "0.0.1"
---

# Sort Imports

This skill defines how to write and order imports. Examples use Python, but the rules apply to any language.

## Rules

- **Top of file:** keep imports at the top of the file.
- **Three groups:** standard library, third-party, then project imports, separated by a blank line; sort by module path and imported name within each group. Use the project's import sorter when one is configured.
- **Relative own imports:** inside a package, import its own modules with relative imports, never absolute ones, in every kind of module (views, services, tests, etc.).
- **Absolute exceptions:** generated code (e.g. database migrations) keeps the imports its generator wrote, never rewrite them; code outside the package (e.g. the project's configuration package) imports it absolutely.
- **Shortest path:** use the simplest relative form, with the fewest steps up that reach the module (`from .bar import x` inside the same package, not `from ..views.bar import x`), and import from a package's entry file when it re-exports the symbol.
- **Multi-line imports:** an import of more than 3 symbols goes on multiple lines, one symbol per line inside parentheses, with a trailing comma.
- **Circular imports:** move shared code into a common module first. Use local imports or other workarounds only as a last resort.

```python
# Wrong behaviour (in orders/views/cart_views.py).
from orders.services import pricing
import os
from requests import Session
from orders.models import Cart, CartItem, Coupon, Pizza

# Correct behaviour.
import os

from requests import Session

from ..models import (
    Cart,
    CartItem,
    Coupon,
    Pizza,
)
from ..services import pricing
```

## Technology-Specific References

- If working with Django, review the [django reference](./references/django-imports.md) file.
