---
name: localize-text
description: Language and timezone rules - which parts of a codebase are in English, which follow the product's user languages, proper diacritics, primary-language-first user text, and UTC everywhere. Use whenever writing user-facing text, error messages, API responses, or date and time handling.
metadata:
  version: "0.0.1"
---

# Localize Text

This skill defines which language each part of a codebase uses, and how to handle time. The rules are project, language, and framework agnostic; examples use Python for illustration.

## Language

| Component                                  | Language                     |
| ------------------------------------------ | ---------------------------- |
| Documentation (Markdown)                   | English                      |
| Code (variables, functions, classes)       | English                      |
| Comments (single-line, JSDocs, docstrings) | English                      |
| Logs                                       | English                      |
| Errors (throw messages)                    | The product's user languages |
| API responses                              | The product's user languages |
| User interface                             | The product's user languages |

- **Respect the table:** code, in general, is always in English.
- **User languages:** the project's docs name its user languages (e.g. Romanian and English). If they don't, ask.
- **Proper diacritics:** always use the correct diacritics and orthography of each language.

```python
# Wrong behaviour.
raise ValidationError(_("Traseul nu a fost gasit"))

# Correct behaviour.
raise ValidationError(_("Traseul nu a fost găsit"))
```

- **Primary language first:** implement user-facing text in the product's primary language first, then adopt localization/translation methods for the others.
- **Rebuild catalogs:** after changing a user-facing string, regenerate and recompile the translation catalogs. Compiled catalogs are often ignored by git, so a stale local copy makes translation tests fail.

## Timezone

- **UTC everywhere:** store, compute, and exchange times in UTC; convert to a local timezone only for display.

```python
# Wrong behaviour.
created_at = datetime.now()

# Correct behaviour.
created_at = datetime.now(timezone.utc)
```

## Technology-Specific References

- If working with Django, review the [django reference](./references/django-localization.md) file.
