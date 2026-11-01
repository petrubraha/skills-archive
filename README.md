# skills-archive

A collection of [Agent Skills](https://github.com/agentskills/agentskills) that encode coding, writing, and workflow conventions for AI coding agents.

Each skill is a folder with a `SKILL.md` file (frontmatter with `name` and `description`, followed by instructions) and optional `references/`.

## Skills

| Skill | Purpose |
| --- | --- |
| `annotate-types` | Annotate parameters, return values, and variables in optionally typed languages |
| `commit-changes` | Branch and commit message naming with shared type prefixes |
| `design-code` | Modularity, single responsibility, DRY, one step per line, named constants |
| `implement-feature` | End-to-end workflow for any coding task, plus the definition of done |
| `localize-text` | Which text is English, which follows user languages, diacritics, UTC everywhere |
| `name-identifiers` | Descriptive names for variables, functions, and classes, no abbreviations |
| `organize-files` | File size limits, package exports, spacing, and developer scripts |
| `refactor-code` | When and how far to refactor existing code |
| `review-changes` | Static re-review of a finished change with `git status` and `git diff` |
| `sort-imports` | Import placement, grouping, order, and circular imports |
| `structure-classes` | Class size limits and polymorphism over type switches |
| `structure-functions` | Function size and signature limits |
| `test-code` | Writing, running, and fixing unit tests, plus coverage reports |
| `write-comments` | When and how to write comments and docstrings |
| `write-errors` | Error message style |
| `write-logs` | Log message style and no sensitive user data |
| `write-prose` | Punctuation and style for any human-readable text |
| `write-spec` | Writing step-by-step implementation specs |

## Workflow

Every skill is developed on its own branch named `feat/<skill-name>` and merged into `main` through a dedicated pull request.

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
