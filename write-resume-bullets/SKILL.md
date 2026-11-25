---
name: write-resume-bullets
description: Rules for turning a project description or repository into high-impact, senior-level resume bullet points. Use whenever the user asks you to write or improve resume bullets from a project or repo.
metadata:
  version: "0.0.1"
---

# Write Resume Bullets

This skill defines how to turn a project description or repository into resume bullet points that read like a senior engineer's work, from the perspective of a technical recruiter. The goal is to market real engineering merit, not to inflate it.

## Analyze First

Read the project before writing, and pull out what a recruiter cares about:

- **Core function:** what the project does and the problem it solves.
- **Tech stack:** the languages, frameworks, and infrastructure that show relevant skill.
- **Hard parts:** the genuine challenges solved (scale, concurrency, migration, reliability), which separate senior work from routine work.
- **Select:** keep the 5-6 most impactful aspects; drop the rest.

## Write with X-Y-Z

- **X-Y-Z method:** each bullet follows "Accomplished [X], measured by [Y], by doing [Z]". X is the outcome, Y is the metric, Z is the technical approach. The formula comes from Laszlo Bock, former Google SVP of People Operations ([source](https://www.businessinsider.com/laszlo-bock-gives-key-to-perfect-resume-2016-10)).
- **First bullet, the what:** the first bullet states the application's primary purpose and function, so the reader knows what the project is before the details.
- **Then the how:** the rest cover implementation, performance work, and specific features.
- **Strong verbs:** lead with precise action verbs (Architected, Optimized, Implemented, Reduced) and standard industry terms, one claim per bullet.

## Keep It Honest

- **No invented metrics:** never fabricate a number. A false metric on a resume is a real risk to the user in an interview.
- **Ask or mark:** if the impact metric (Y) isn't in the source, ask the user for it, or write the bullet with a clearly bracketed placeholder like `[X%]` for them to fill in. Don't silently drop the metric or make one up.
- **Claims must trace:** every bullet maps to something in the project; if you can't point to it, cut it.

## Example

```text
# Wrong behaviour: vague, no metric structure, invented number.
- Worked on the backend using Python and made the API 300% faster.

# Correct behaviour: X-Y-Z, honest about an unknown metric.
- Built a REST API serving the app's order workflow in Python and FastAPI,
  handling [N] requests/day across [N] endpoints.  (first bullet: the what)
- Cut p95 latency by [Y%] by adding a Redis cache and replacing N+1 ORM
  queries with batched joins.  (Y bracketed: ask the user for the real figure)
```

## Related Skills

- `answer-questions`: how to present the bullets (concise, bulleted); this skill does not add preamble or follow-up questions beyond asking for a missing metric.
- `write-prose`: punctuation and style rules for the bullet text.
