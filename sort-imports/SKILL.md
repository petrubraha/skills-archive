---
name: sort-imports
description: Import rules - placement, grouping and order, shortest relative paths for a package's own modules, multi-line imports, and resolving circular imports. Use whenever adding, moving, or reordering imports.
metadata:
  version: "0.0.1"
---

# Sort Imports

This skill defines how to write and order imports. The rules are project, language, and framework agnostic; examples use Python for illustration.

## Rules

- **Top of file:** keep imports at the top of the file.
- **Three groups:** standard library, third-party, then project imports, separated by a blank line; sort by module path and imported name within each group. Use the project's import sorter when one is configured.
- **Relative own imports:** inside a package, import its own modules with relative imports, never absolute ones, in every kind of module (views, services, models, tests, commands).
- **Absolute exceptions:** generated code (e.g. database migrations) keeps the imports its generator wrote, never rewrite them; code outside the package (e.g. the project's configuration package) imports it absolutely.
- **Shortest path:** use the simplest relative form, with the fewest steps up that reach the module (`from .bar import x` inside the same package, not `from ..views.bar import x`), and import from a package's entry file when it re-exports the symbol.
- **Multi-line imports:** an import of more than 3 symbols goes on multiple lines, one symbol per line inside parentheses, with a trailing comma.
- **Circular imports:** move shared code into a common module first. Use local imports or other workarounds only as a last resort.

```python
# Wrong behaviour (in shop/views/cart_views.py).
from shop.services import pricing
import os
from requests import Session
from shop.models import Cart, CartItem, Discount, Product

# Correct behaviour.
import os

from requests import Session

from ..models import (
    Cart,
    CartItem,
    Discount,
    Product,
)
from ..services import pricing
```

## Technology-Specific References

- If working with Django, review the [django reference](./references/django-imports.md) file.
