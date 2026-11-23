---
name: format-markdown
description: Formatting rules for Markdown bullet points and tables. Use whenever presenting enumerations in Markdown.
metadata:
  version: "0.0.1"
---

# Format Markdown

This skill defines how to format enumerations in Markdown.

## Bullet Points

- **When to use:** choose bullets for a short enumeration without extra detail per item.
- **Fixed shape:** every bullet reads `- **2-word concept:** max 10 words explanation`.
- **Longer allowed:** exceed 10 words only when the meaning genuinely requires it.

```text
# Correct behaviour.
- **Fast index:** BM25 keyword search, no embeddings needed.
- **Best index:** semantic embeddings, slower to build but more accurate.
```

## Tables

- **When to use:** choose a table when each item needs more detail, held in extra columns.
- **Short cells:** keep each cell under 5 words; avoid long explanations in cells.
- **Category column:** past 5 rows, add a `category` column and sort rows by it.
- **Always indent:** indent the table so it renders as a nested block.

```text
# Correct behaviour: indented, short cells, sorted by category.
| Runtime | Strength            |
| ------- | ------------------- |
| Node.js | Largest ecosystem   |
| Bun     | Fast, built-in tools|
| Deno    | Secure by default   |
```

## Related Skills

- `answer-questions`: when to use bullets vs. tables while answering.
- `write-prose`: punctuation and style rules for the text itself.
