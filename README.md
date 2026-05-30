# plone-docstyle

A Claude Code skill for writing, editing, reviewing, and planning Plone
documentation. Encodes the Plone docs style guide, the Diataxis framework,
MyST markup conventions, TOC planning, and gap analysis.

## Install

In Claude Code:

```
/plugin marketplace add jensens/plone-docstyle
/plugin install plone-docstyle@plone-docstyle
```

Then invoke from any Claude Code session:

```
/plone-docstyle:plone-docstyle plan <topic>
/plone-docstyle:plone-docstyle tutorial <topic>
/plone-docstyle:plone-docstyle how-to <topic>
/plone-docstyle:plone-docstyle explanation <topic>
/plone-docstyle:plone-docstyle reference <topic>
```

Without an explicit mode, the skill detects intent from your request and
asks if the Diataxis quadrant is ambiguous.

## What it covers

- **Style rules** — voice, tense, terminology, capitalization, link style
- **Diataxis** — tutorial / how-to / reference / explanation quadrants and when each applies
- **MyST markup** — admonitions, cross-references, code blocks, directives
- **TOC planning** — structuring sections, ordering pages, avoiding orphans
- **Gap analysis** — auditing an existing docs tree for missing or misplaced material

## Updating

```
/plugin marketplace update plone-docstyle
/reload-plugins
```

## License

MIT
