---
name: organize-files
description: File-level rules for length, package exports, developer scripts, etc. Use when creating or splitting files, editing package entry files, or writing scripts.
metadata:
  version: "0.0.1"
---

# Organize Files

This skill defines how source files are sized, exported, placed, etc. Examples use Python, but the rules apply to any language.

## Rules

- **File length:** keep files under 1000 lines. If a file exceeds this limit, refactor it into multiple components.
- **Package exports:** keep package entry files (`__init__.py`, `index.ts`, barrel files) explicit; re-export only intentionally public symbols, never everything from a module.

```python
# Wrong behaviour (in services/__init__.py).
from .notifications import *

# Correct behaviour.
from .notifications import build_notifier, send_digest
```

- **Whitespace:** use one blank line between functions and methods, and two blank lines between classes, unless the language's standard formatter decides otherwise.
- **Scripts folder:** one-off and developer scripts (translation fixers, generators, data fixes) live only in `scripts/`, never in the repository root or inside an application module.
- **Script paths:** scripts resolve paths from their own location, not from the current directory, so they work wherever they are run from.

```python
# Wrong behaviour (in scripts/fix_translations.py).
translations_path = Path("locale/ro/messages.po")

# Correct behaviour.
PROJECT_ROOT = Path(__file__).resolve().parent.parent
translations_path = PROJECT_ROOT / "locale" / "ro" / "messages.po"
```

- **App logic:** logic the application runs belongs in the framework's command or task mechanism, not in `scripts/`.
- **Clean root:** only the entry points the tooling requires stay in the repository root.
- **One helpers location:** shared helpers live only in the project's single helpers location (e.g. `utils/`). Never create ad-hoc helper modules beside it.

```text
# Wrong behaviour.
app/views/_helpers.py
app/services/common.py

# Correct behaviour.
app/utils/dates.py
app/utils/phone.py
```

## Technology-Specific References

- If working with Django, review the [django reference](./references/django-files.md) file.
