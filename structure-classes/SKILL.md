---
name: structure-classes
description: Size and design limits for classes - at most 500 lines, ideally one class per file, and overridden methods instead of type switches inside a class hierarchy. Use whenever writing or changing a class or class hierarchy.
metadata:
  version: "0.0.1"
---

# Structure Classes

This skill defines size and design limits for classes. Examples use Python, but the rules apply to any language.

## Rules

- **No more than 500 lines:** break a class into multiple components if it exceeds this.
- **A class per file:** this is an ideal; in practice it may be violated.
- **No type switches:** inside a class hierarchy, never branch on the runtime type (`isinstance`, `instanceof`, `is`) to pick a subclass's behaviour; give the base class a method or property each subclass overrides. Elsewhere (input validation, third-party types such as exceptions), type checks are fine.

```python
# Wrong behaviour.
def get_author(publication):
    if isinstance(publication, Post):
        return publication.writer
    if isinstance(publication, Review):
        return publication.reviewer

# Correct behaviour.
class Publication:
    @property
    def author(self):
        raise NotImplementedError

class Post(Publication):
    @property
    def author(self):
        return self.writer

class Review(Publication):
    @property
    def author(self):
        return self.reviewer
```

## Technology-Specific References

- If working with Django, review the [django reference](./references/django-classes.md) file.
