# Django Imports

## Sorter

Sort imports with `isort`, configured in `.isort.cfg` to skip migrations. Pass the app and project packages:

```bash
python -m isort orders pizzeria
```

## Relative Imports

- **Own apps:** import code from the project's own Django apps (e.g. `orders`) with relative imports only, never `from orders.… import …` or `import orders.…`. This holds for every module, e.g. views, services, tests, etc.
- **Migrations:** keep migrations exactly as `makemigrations` generates them; never rewrite their imports.
- **Project package:** the project package (e.g. `pizzeria/`, holding settings and root URLs) imports the apps absolutely, from outside them.
- **Package re-exports:** import from a package's `__init__.py` when it re-exports the symbol, e.g. `from ..services.delivery import assign_courier`.

```python
# Wrong behaviour.
from orders.services import kitchen_queue
import os
from django.utils import timezone
from orders.models import Order, OrderItem, Pizza, Topping

# Correct behaviour (in orders/views/kitchen_views.py).
import os

from django.utils import timezone

from ..models import (
    Order,
    OrderItem,
    Pizza,
    Topping,
)
from ..services import kitchen_queue
```
