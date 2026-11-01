---
name: structure-classes
description: Size and design rules for classes, including polymorphism over type switches. Use whenever writing or changing a class or class hierarchy.
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
def get_preparation_minutes(menu_item):
    if isinstance(menu_item, Pizza):
        return menu_item.oven_minutes
    if isinstance(menu_item, Salad):
        return menu_item.assembly_minutes

# Correct behaviour.
class MenuItem:
    @property
    def preparation_minutes(self):
        raise NotImplementedError

class Pizza(MenuItem):
    @property
    def preparation_minutes(self):
        return self.oven_minutes

class Salad(MenuItem):
    @property
    def preparation_minutes(self):
        return self.assembly_minutes
```
