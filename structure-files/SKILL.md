---
name: structure-files
description: File-level rules for length, package exports, file placement, etc. Use when creating or splitting files, or editing package entry files.
metadata:
  version: "0.0.1"
---

# Structure Files

This skill defines how source files are sized, exported, placed, etc. Examples use Python, but the rules apply to any language.

## Rules

- **File length:** keep files under 1000 lines. If a file exceeds this limit, refactor it into multiple components.
- **Package exports:** keep package entry files (`__init__.py`, `index.ts`, barrel files) explicit; re-export only intentionally public symbols, never everything from a module.

```python
# Wrong behaviour (in services/__init__.py).
from .delivery import *

# Correct behaviour.
from .delivery import assign_courier, estimate_delivery_time
```

- **Whitespace:** separate methods with one blank line and top-level functions and classes with two, unless the language's standard formatter decides otherwise.
- **One helpers location:** shared helpers live only in the project's single helpers location (e.g. `utils/`); never create ad-hoc helper modules beside it.

```text
# Wrong behaviour.
orders/views/_helpers.py
orders/services/common.py

# Correct behaviour.
utils/prices.py
utils/addresses.py
```
