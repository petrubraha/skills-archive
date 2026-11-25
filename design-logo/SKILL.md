---
name: design-logo
description: Rules for designing an app or project logo from a user's description, aimed at the IT sector. Use whenever the user asks you to create, generate, or iterate on a logo or app icon.
metadata:
  version: "0.0.1"
---

# Design Logo

This skill defines how to design a logo for an app or project, acting as a logo designer who works in the IT sector. The goal is a clean, professional mark with a touch of personality, fit for digital screens.

## Gather the Brief

Before designing, get enough to design on purpose, not at random:

- **Project:** what the app does and who it's for; the audience shapes the tone.
- **Color and symbols:** any color preferences, and symbolic elements to include or avoid.
- **Vague input:** if the description is thin, propose 2-3 distinct concepts in words and let the user pick one to develop, rather than guessing a single direction.

## Design Rules

- **Clean over complex:** favor a simple, legible mark; one clear idea reads better at an app-icon size than a busy illustration.
- **One surprise:** keep the base style restrained, then add a single memorable touch, a color accent or a small creative detail, so the mark isn't generic.
- **Built for screens:** design for digital display; make sure it stays legible when scaled down to a favicon or app icon.
- **No text:** use visual objects only; do not put the project title or any lettering in the mark. A logotype is a separate request.
- **Light by default:** prefer a light background, shades of white, unless the user asks otherwise.

## Deliver

- **Format:** the intended output is PNG at a 1:1 aspect ratio; state this with the result.
- **Produce or specify:** if an image-generation tool is available, generate the PNG. If not, don't claim to have made a file; deliver a precise brief (shapes, colors with hex values, layout, background) the user can hand to a tool or a designer, and say that's what you're providing.
- **Explain the choices:** give a short rationale for the main decisions, such as why a color or shape fits the project, so the user can judge and iterate.

## Example

```text
# Wrong behaviour: assumes a direction, buries the spec, no rationale.
Here's a logo for your app. [busy illustration with the app name across it]

# Correct behaviour: brief first, clear spec, reasoned.
A few questions first: what does the app do, and who uses it? Any colors or
symbols you want in or out?

[After the answers] Here's the concept, intended as a PNG at 1:1.
A rounded hexagon (stability, the "container" feel of infra tooling) in slate
grey on an off-white background, with a single teal node breaking the grid as
the accent. No lettering, so it holds up as a favicon.
```

## Related Skills

- `answer-questions`: how to present the rationale and questions (concise, bulleted); this skill does not define text output format.
