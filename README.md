# skills-archive

A collection of [Agent Skills](https://github.com/agentskills/agentskills) that encode coding, writing, and workflow conventions for AI coding agents.

Each skill is a folder with a `SKILL.md` file (frontmatter with `name` and `description`, followed by instructions) and optional `references/`.

## Skills

| Skill                 | Covers                                               |
| --------------------- | ---------------------------------------------------- |
| `annotate-types`      | Annotating parameters and returns, gradual migration |
| `commit-changes`      | Shared type prefixes for branches and commits        |
| `design-code`         | Modularity, DRY, named constants, etc.               |
| `implement-feature`   | Plan-to-docs workflow and definition of done         |
| `localize-text`       | English vs. user languages, diacritics, UTC          |
| `name-identifiers`    | Descriptive names, no abbreviations                  |
| `organize-files`      | 1000-line limit, explicit exports, scripts folder    |
| `refactor-code`       | Plan first, stay local, no unasked migrations        |
| `review-changes`      | Re-reading the diff, then an honest summary          |
| `sort-imports`        | Three groups, relative paths, circular imports       |
| `structure-classes`   | 500-line limit, polymorphism over type switches      |
| `structure-functions` | Max 3 parameters, no booleans, 60-line limit         |
| `test-code`           | Isolation with mocks, test scope, coverage           |
| `write-comments`      | When to comment, docstrings over inline comments     |
| `write-errors`        | Capitalization, no trailing period                   |
| `write-logs`          | No sensitive data, capitalization, final period      |
| `write-prose`         | No em dash, short enumerations                       |
| `write-spec`          | Step-by-step plans, one commit per step              |

## Workflow

Every skill is developed on its own branch named `feat/<skill-name>` and merged into `main` through a dedicated pull request.

## Comment Resolver Agent

[`comment-resolver-agent`](https://github.com/petrubraha/comment-resolver-agent), included as a submodule, is a reusable workflow that applies submitted pull request reviews with Gemini CLI and pushes the fixes to the reviewed branch.

## Validation

The [agentskills](https://github.com/agentskills/agentskills) repository is included as a submodule and provides the `skills-ref` validator.

```bash
git clone --recurse-submodules https://github.com/petrubraha/skills-archive.git
# or, in an existing clone
git submodule update --init

cd agentskills/skills-ref
python -m venv .venv
.venv/Scripts/activate   # Windows; use .venv/bin/activate on macOS and Linux
pip install -e .

skills-ref validate ../../<skill-name>
```
