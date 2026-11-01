# Django Localization

## Translation Catalogs

After changing a user-facing string, regenerate the `.po` files and compile them into `.mo` files:

```bash
python manage.py makemessages --all
python manage.py compilemessages
```

The translation tests read the compiled `.mo` files, which git ignores, so a stale local copy makes them fail.

_Note: if the project's docs list its own `makemessages` flags (e.g. ignored paths), use those._
