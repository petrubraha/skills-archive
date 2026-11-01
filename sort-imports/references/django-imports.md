# Django Imports

## Sorter

Sort imports with `isort`, configured in `.isort.cfg` to skip migrations. Pass the app and project packages:

```bash
python -m isort trails mountaintrails
```

## Relative Imports

- **Own apps:** import code from the project's own Django apps (e.g. `trails`) with relative imports only, never `from trails.… import …` or `import trails.…`. This holds for every module, e.g. views, services, tests, etc.
- **Migrations:** keep migrations exactly as `makemigrations` generates them; never rewrite their imports.
- **Project package:** the project package (e.g. `mountaintrails/`, holding settings and root URLs) imports the apps absolutely, from outside them.
- **Package re-exports:** import from a package's `__init__.py` when it re-exports the symbol, e.g. `from ..services.notifications_services import build_notifier`.

```python
# Wrong behaviour.
from trails.services import hike_feed
import os
from django.utils import timezone
from trails.models import Blog, Comment, Post, PostLike

# Correct behaviour (in trails/views/feed_views.py).
import os

from django.utils import timezone

from ..models import (
    Blog,
    Comment,
    Post,
    PostLike,
)
from ..services.hike_feed import build_hikes_feed
```
