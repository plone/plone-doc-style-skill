# plone-doc-style

A Claude Code skill for writing, editing, reviewing, and planning Plone
documentation. Encodes the Plone docs style guide, the Diataxis framework,
MyST markup conventions, TOC planning, and gap analysis.

## Install

In Claude Code:

```
/plugin marketplace add plone/plone-doc-style-skill
/plugin install plone-doc-style@plone-doc-style
```

Then invoke from any Claude Code session:

```
/plone-doc-style:plone-doc-style plan <topic>
/plone-doc-style:plone-doc-style tutorial <topic>
/plone-doc-style:plone-doc-style how-to <topic>
/plone-doc-style:plone-doc-style explanation <topic>
/plone-doc-style:plone-doc-style reference <topic>
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
/plugin marketplace update plone-doc-style
/reload-plugins
```

## License

MIT
