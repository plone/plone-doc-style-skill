# plone-doc-style

A skill for AI coding agents that write, edit, review, and plan Plone
documentation. It encodes the Plone documentation style guide, the sentence
shapes that reviewers reject as machine-written, the Diataxis framework,
MyST markup conventions, table-of-contents planning, and gap analysis.

The skill follows the [Agent Skills](https://agentskills.io/) format, so it
works in Claude Code and in any other agent that reads `SKILL.md` files, such
as Mistral Vibe, GitHub Copilot CLI, OpenAI Codex, and Gemini CLI. The
repository doubles as a Claude Code plugin marketplace for one-command
installs.

## Layout

```
skills/plone-doc-style/
├── SKILL.md                   # core rules and workflows, always loaded when the skill runs
├── references/
│   ├── diataxis.md            # the four quadrants in depth
│   ├── myst-markup.md         # page structure, directives, images, diagrams
│   ├── planning.md            # coverage matrix and plan template
│   └── sphinx-setup.md        # extensions, theme, conf.py
└── scripts/
    └── check-prose.sh         # lists lines that break the style rules
evals/                         # test cases for `claude plugin eval`
```

The agent loads `SKILL.md` when the skill triggers and reads a reference file
only when the task calls for it.

## Install

### Claude Code, terminal CLI

```
/plugin marketplace add plone/plone-doc-style-skill
/plugin install plone-doc-style@plone-doc-style-skill
```

### Claude Code, VSCode extension

The `/plugin` slash command is not wired up in the VSCode extension. Use the
GUI instead:

1. Open the **Claude** panel.
2. From the panel menu (or command palette), choose **Manage Plugins**.
3. Click **Add marketplace** and paste:
   ```
   plone/plone-doc-style-skill
   ```
4. Once the marketplace loads, find **plone-doc-style** in the plugin list
   and click **Install**.
5. Reload Claude Code (close and reopen the panel, or restart the editor).

### Claude Code, settings.json

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

### Other agents

Copy or symlink the skill directory into the place your agent reads skills
from:

```shell
git clone https://github.com/plone/plone-doc-style-skill.git
ln -s "$PWD/plone-doc-style-skill/skills/plone-doc-style" ~/.agents/skills/plone-doc-style
```

`~/.agents/skills/` is a shared location that several agents read. Check your
agent's documentation for its own path, for example a `skills` directory
under its configuration folder, or a project-level `.agents/skills/`
directory for a single repository. Everything another agent needs is inside that directory. The `.claude-plugin/`
manifests and the `evals/` suite at the repository root are Claude Code
specific.

## Use

In Claude Code, invoke the skill directly:

```
/plone-doc-style plan <topic>
/plone-doc-style tutorial <topic>
/plone-doc-style how-to <topic>
/plone-doc-style explanation <topic>
/plone-doc-style reference <topic>
```

In every agent, including Claude Code, the skill also triggers from a plain
request, for example "write a how-to for configuring caching in our Plone 6
docs" or "audit docs/ for Diataxis gaps". Without an explicit mode, the skill
detects intent from your request and asks when the Diataxis quadrant is
ambiguous.

### Check prose without an agent

The bundled script runs anywhere with a POSIX shell and awk. It lists the
lines that break the style rules and exits non-zero when it finds any:

```shell
bash skills/plone-doc-style/scripts/check-prose.sh docs/**/*.md
```

It reports two sentences on one line, `, so` and semicolon clause joins,
`X, not Y` contrasts, sentences over 25 words, machine-writing vocabulary, em
dashes, shell prompts and ellipses in code blocks, comments in JSON blocks,
mismatched `html_meta` descriptions, and pages without exactly one H1.

## What it covers

- **Style rules**: voice, tense, one sentence per line, sentence case, filenames, link rules
- **Sentence construction**: the `, so` chains, semicolon joins, and `X, not Y` contrasts that mark prose as machine-written
- **Diataxis**: tutorial, how-to, reference, and explanation quadrants and when each applies
- **MyST markup**: admonitions, cross-references, code blocks, directives, images, diagrams
- **TOC planning**: structuring sections, ordering pages, avoiding orphans
- **Gap analysis**: auditing an existing docs tree for missing or misplaced material
- **Sphinx setup**: extensions, theme, and `conf.py` for Plone ecosystem docs

## Test the skill

Validate the manifests and frontmatter:

```shell
claude plugin validate .
```

Run the eval suite. Each case runs once with the plugin and once without,
and the graders check that the skill fired, that the agent ran the prose
checker and it reported clean, that the page carries the metadata block and
none of the machine-writing patterns, and that it stays in its Diataxis
quadrant. The Bash grant lets the agent run the checker. These are real model
runs billed to your account, so pass `--model` to pick a cheaper model for
routine runs:

```shell
claude plugin eval . --allow-tools Write Edit "Bash(bash *)" --no-publish
```

Add `--case 'write-howto-*'` to run a subset or `--runs 3` for a less noisy
score before a release. Results land in `evals/results/`, which is ignored by git.

## Updating

In the terminal CLI:

```
/plugin marketplace update plone-doc-style-skill
/reload-plugins
```

In the VSCode extension: open **Manage Plugins**, find the marketplace,
click **Update**, then reload the panel.

For other agents, pull the repository.

## Changes

- **0.5.0**: the skill is renamed from `author` to `plone-doc-style`, so the
  Claude Code command changes from `/plone-doc-style:author` to
  `/plone-doc-style`. `SKILL.md` shrinks to the core rules and workflows;
  the detail moves to `references/`. New prose checker script and eval suite.
  Frontmatter reduced to the Agent Skills specification fields.
- **0.4.0**: sentence construction rules against machine-written prose.
- **0.3.0**: review findings applied.

## License

MIT
