# plone-doc-style

A Claude Code skill for writing, editing, reviewing, and planning Plone
documentation. Encodes the Plone docs style guide, the Diataxis framework,
MyST markup conventions, TOC planning, and gap analysis.

## Install

The plugin works the same once installed, but the install path differs by
Claude Code surface.

### Terminal CLI (`claude`)

```
/plugin marketplace add plone/plone-doc-style-skill
/plugin install plone-doc-style@plone-doc-style-skill
```

### VSCode extension

The `/plugin` slash command is not wired up in the VSCode extension. Use
the GUI instead:

1. Open the **Claude** panel.
2. From the panel menu (or command palette), choose **Manage Plugins**.
3. Click **Add marketplace** and paste:
   ```
   plone/plone-doc-style-skill
   ```
4. Once the marketplace loads, find **plone-doc-style** in the plugin list
   and click **Install**.
5. Reload Claude Code (close and reopen the panel, or restart the editor)
   so the skill becomes available.

### Cross-surface (settings.json)

Both surfaces read `~/.claude/settings.json`. Adding the marketplace and
plugin there installs it everywhere at once:

```json
{
  "extraKnownMarketplaces": {
    "plone-doc-style-skill": {
      "source": {
        "source": "github",
        "repo": "plone/plone-doc-style-skill"
      }
    }
  },
  "enabledPlugins": {
    "plone-doc-style@plone-doc-style-skill": true
  }
}
```

Restart Claude Code after editing.

## Use

Invoke from any Claude Code session:

```
/plone-doc-style:author plan <topic>
/plone-doc-style:author tutorial <topic>
/plone-doc-style:author how-to <topic>
/plone-doc-style:author explanation <topic>
/plone-doc-style:author reference <topic>
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

In the terminal CLI:

```
/plugin marketplace update plone-doc-style-skill
/reload-plugins
```

In the VSCode extension: open **Manage Plugins**, find the marketplace,
click **Update**, then reload the panel.

## License

MIT
