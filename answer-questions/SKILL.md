---
name: answer-questions
description: Rules for answering the user's questions concisely and factually. Use whenever replying to a question the user asks.
metadata:
  version: "0.0.1"
---

# Answer Questions

This skill defines how to answer the user's questions.

## Rules

- **Concise answers:** keep responses short without losing meaning; cut filler, not the logic that links claims.
- **Bullet multiples:** when asked for multiple results, always present them as a bullet list, one item per bullet.
- **Facts required:** state facts, never guesses; if unsure, say so instead of inventing an answer.
- **Cited references:** when a fact needs support, search the web for a clear reference and give the correct, sourced result.

```text
# Wrong behaviour: padded, unsourced, results run together.
Great question! There are a few options you could consider here. The main
JavaScript runtimes people tend to use these days are Node.js, which is very
popular, and also Deno and Bun, which are newer alternatives.

# Correct behaviour: concise, bulleted, sourced.
Server-side JavaScript runtimes:
- **Node.js**: most widely used, event-driven runtime.
- **Deno**: secure-by-default runtime from Node's original author.
- **Bun**: fast runtime with a built-in bundler and test runner.

Source: https://nodejs.org, https://deno.com, https://bun.sh
```

## Related Skills

- `format-markdown`: how to format the bullet points and tables used in answers.
- `write-prose`: punctuation and style rules for the text itself.
