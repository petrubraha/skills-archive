---
name: write-comments
description: Rules for code comments and docstrings - when to comment, when to delete, preferring docstrings, length, capitalization, and punctuation. Use whenever adding, editing, or reviewing comments, docstrings, or doc comments.
metadata:
  version: "0.0.1"
---

# Write Comments

This skill defines when and how to write comments. The rules are project, language, and framework agnostic; examples use Python for illustration.

## Rules

- **Prefer docstrings:** use docstrings or the language's doc comments (JSDoc, `///`) instead of inline comments when possible.
- **No boilerplate:** avoid boilerplate comments, and delete pleonastic comments that add no value to the code.
- **Complex logic only:** add comments when the logic is complex and the behaviour is not obvious.
- **Concise:** comments are descriptive but concise, always under 2–3 lines.
- **Capitalized:** capitalize the first letter of the first word.
- **Final period:** end each comment with a period (`.`).

```python
# Wrong behaviour.
# this calculates total price
def get_price(x, y):
    pass

# Correct behaviour.
def get_price(base_amount: float, tax: float) -> float:
    """Calculates the final price including tax."""
    pass
```

## Related Skills

- `write-prose`: punctuation rules for the text itself (no em dash).
