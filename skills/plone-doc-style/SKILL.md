---
name: plone-doc-style
description: "Writes, edits, reviews, and plans documentation for Plone and Plone add-ons in MyST Markdown, following the Plone documentation style guide and the Diataxis framework. Use whenever the user works on Plone documentation or the docs directory of a Plone package: a new or changed page, a tutorial, how-to guide, explanation, or reference page, a documentation pull request or review, a table of contents or documentation plan, or a check of prose against the Plone style guide, even when the request does not mention Plone style, MyST, Sphinx, or Diataxis."
license: MIT
compatibility: Any Agent Skills client. The bundled prose check needs a POSIX shell with awk.
metadata:
  version: "0.5.0"
  author: Jens W. Klein
allowed-tools: Read Grep Glob Write Edit
---

# Plone documentation style

This skill holds what an agent gets wrong about Plone documentation without being told: the style rules, the sentence shapes that reviewers reject as machine-written, the Diataxis discipline, the MyST conventions, and the planning method.
Reference files hold the detail.
Load each one only when the table below says so, because every loaded line competes with the page you are writing.

## Modes

Pick the mode from the request.

- **Plan**: words like plan, structure, organize, audit, outline, TOC, gap analysis. Follow the [planning workflow](#planning-workflow).
- **Write or edit**: identify the Diataxis quadrant first and ask when it is ambiguous. Follow the [writing workflow](#writing-workflow).
- **Review**: run the writing checklist against the existing text and report findings per line.

| Read this file | When |
|---|---|
| `references/diataxis.md` | you write a tutorial or an explanation, a page seems to need two quadrants, or you audit pages for mixed content |
| `references/myst-markup.md` | a page needs tabs, cards, grids, figures, video, diagrams, definition lists, or version directives |
| `references/planning.md` | you plan, audit, or outline a documentation set |
| `references/sphinx-setup.md` | the user sets up or changes `conf.py`, the theme, or Sphinx extensions |

## Style rules

Plone follows the Microsoft Writing Style Guide in American English.
Vale enforces the spelling.

- Address the reader as "you".
- Use the active voice and, for instructions, the imperative mood: "Configure the server".
- Keep the tone informational but friendly.
- Write headings in sentence case.
- Name files with dashes and the `.md` extension.
- Give every page exactly one H1, then divide the body into H2 sections, each with a `(label)=` line above it.

### One sentence per line

Every sentence starts on its own line.
Never break a sentence across lines and never put two sentences on one line.
Pull request diffs and review comments then address one sentence each.
Ignore line-length limits, because docs are prose.

### Sentence construction

Documentarians recognize machine-written prose by its sentence shapes.
Write every sentence as one independent clause that carries one idea.
Apply these tests to each draft sentence:

- **Does the second clause stand alone as a sentence?** Make it one.
  This applies to clauses joined with `, so`, `, and`, `, but`, or a semicolon.
  A `so that` purpose clause without a comma is not a join and may stay.
  Draft: `Transactions are ACID, so a request commits all of its changes or none.`
  Final: `Transactions are ACID. A request commits all of its changes or none.`
- **Does it state a cause and its effect?** Put the cause in one sentence and the effect in the next.
  Do not chain them with `, so`, `which means`, or `therefore`.
  Draft: `Run it with uvx, so you do not have to install anything first.`
  Final: `Run it with uvx. You do not need to install anything first.`
- **Does it say what something is not?** Keep the positive half.
  Draft: `A website is a tree of dissimilar things, not a set of uniform rows.`
  Final: `A website is a tree of dissimilar things.`
  When the reader needs the warning, give the negation its own sentence that starts with `Do not` or `It is not`.
- **Is it longer than 25 words?** Split it.
  The first sentence of a page states the task or topic in under 20 words.
  List what the page covers in a second sentence or in bullets.
- **Vocabulary.** Avoid: ensure, leverage, utilize, seamless, robust, comprehensive, crucial, delve, streamline, foster, enhance, simply, easily, trivial, "it's worth noting", "it's important to note", "in order to", and Additionally, Furthermore, or Moreover as sentence openers.
  Do not use em dashes. Use a comma, a colon, or a new sentence.

The bundled script `scripts/check-prose.sh` finds these shapes and the markup mistakes below.
It lists lines to reread and gives no verdicts.

### Page metadata

Plone core documentation requires this block at the top of every page.
Add-on documentation benefits from it on landing pages and section indexes, the pages people share.
Projects outside Plone may use their own metadata.

```markdown
---
myst:
  html_meta:
    "description": "What the page covers, in one sentence."
    "property=og:description": "What the page covers, in one sentence."
    "property=og:title": "Page title"
    "keywords": "Plone, keyword1, keyword2"
---
```

The `description` and `property=og:description` values must be identical.
Search engines ignore `keywords`.
Keep it on core docs for consistency and skip it elsewhere.

## Diataxis in brief

Each page belongs to exactly one quadrant.
Mixing quadrants is the most common documentation failure.

| Quadrant | The reader is | The page gives | Quick test |
|---|---|---|---|
| Tutorial | learning | one guaranteed-safe path to a visible result | Can a beginner complete it every time? |
| How-to guide | working | steps to one real-world result, with no teaching | Does it solve one problem for someone who has the skill? |
| Reference | working | austere, complete facts structured like the product | Is it boring and purely factual? |
| Explanation | learning | context, design decisions, and trade-offs | Could you read it away from the keyboard and learn something? |

Language cues: a tutorial says "we will" and "notice that".
A how-to guide opens with "This guide shows you how to".
Reference states facts and uses "must".
Explanation says "the reason is" and weighs alternatives.
Keep teaching out of how-to guides and instructions out of explanations, and link to the other quadrant instead.

## Markup essentials

- **Labels and cross-references.** Put `(my-label)=` on its own line above a heading. Link with `` {ref}`my-label` ``, `` {ref}`Display text <my-label>` ``, or `` {doc}`/path/to/page` ``. Link to a shared fact instead of repeating it, because duplicated facts drift.
- **Admonitions.** At most one or two per page. `warning` when the reader can break something, `important` when a step is required for a correct result, `note` for a side fact, `tip` for an optional shortcut, `seealso` for related links. Delete a note that only restates the previous paragraph.
- **Code blocks.** Always name a lexer. `shell` for commands without prompts, `console` for a session with output, `text` when nothing else highlights. Never include `$` or `#` prompts in `shell` blocks. Never use `...` to elide code. JSON has no comment syntax.
- **UI elements.** `` {guilabel}`Save` `` for labels and `` {menuselection}`Site Setup --> Mail` `` for paths. They render as badges and help screen readers.
- **Glossary terms.** `` {term}`content type` `` for terms defined in the glossary.
- **Images.** At most 740 pixels wide, Volto screenshots taken at a 1180 pixel browser width, and `:alt:` text on every image.
- **Version changes.** `{versionadded}`, `{versionchanged}`, `{versionremoved}`, and `{deprecated}` directives instead of prose.

## Writing workflow

Copy this checklist and work through it in order:

```text
- [ ] Quadrant identified, and the matching section of references/diataxis.md read for a tutorial or an explanation
- [ ] Neighboring pages read for terminology, existing labels, and cross-references
- [ ] Draft written: metadata, one H1, labels above headings, one sentence per line
- [ ] bash scripts/check-prose.sh PAGE.md run, every reported line reread and fixed, rerun until it prints "clean"
- [ ] make html, make vale, and make linkcheckbroken run when the project has the Plone docs Makefile
```

The script path is relative to this skill's directory.
Run it on every page you wrote or changed.
When `make vale` flags a Plone proper noun, add the word to `styles/config/vocabularies/Plone/accept.txt` in alphabetical order rather than rewording the sentence.
When `make html` warns, fix the markup rather than the warning filter.

## Planning workflow

Read `references/planning.md` first.
It holds the coverage matrix and the plan template.

1. Settle the scope: one package, a feature area, or a whole site.
2. Inventory what exists: current docs, README files, docstrings, changelog.
3. Name the audiences, because they set the Diataxis balance.
4. Fill one coverage grid per topic area and mark each quadrant as exists, partial, missing, or not applicable.
5. Deliver the plan: overview, coverage audit, document tree, page specifications, prioritized roadmap, and style notes.

Plan pages by what the reader wants to achieve, never by user role.
Plan two pages when a topic needs both a how-to guide and an explanation.

## Gotchas

- Blog links rot. Copy the fact into the page and cite the source in a `seealso` admonition.
- Links must be public URLs. Never link to pages that need authentication.
- Never disable linkcheck to hide a broken link. Exclude a URL by wrapping it in single backticks or by adding it to `linkcheck_ignore` in `conf.py`.
- Every directory has an `index.md`.
- Static assets live under `/_static/` in a subdirectory named after the section. Include fragments live under `/_inc/`.
- Vale rejects Plone proper nouns until they are in `accept.txt`.
- The `{versionremoved}` directive comes from `plone-sphinx-theme`. Projects on another theme have only the stock Sphinx version directives.
- A tutorial must work for every reader every time. Remove choices and environmental surprises instead of documenting them.
- End a page with its last step, its last fact, or a `seealso` admonition. Never add a section titled Conclusion, Summary, or Next steps, and never close with a paragraph that restates the page or praises the design. Both are machine-writing tells.

## Beyond Plone core

For Plone add-ons, the style rules, Diataxis, and MyST conventions apply unchanged.
For documentation outside Plone, keep the style rules, Diataxis, and MyST conventions, adapt the directory layout and metadata to the project, and note in a plan when Vale or linkcheck is not configured.
