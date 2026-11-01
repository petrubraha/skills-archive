# Django Files

## Package Exports

Keep each app package's `__init__.py` exports explicit, e.g. `orders/services/delivery/__init__.py` re-exports `assign_courier` and nothing it doesn't intend to make public.

## Scripts

- **Scripts folder:** translation fixers, generators, and data fixes live in `scripts/`. `Path(__file__).resolve().parent.parent` is the project root.
- **App logic:** logic the app runs belongs in a management command (`<app>/management/commands/`), not in `scripts/`.
- **Clean root:** only `manage.py` and the entry points a tool requires stay at the repository root.
