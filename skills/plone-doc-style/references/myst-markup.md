# MyST markup for Plone documentation

Read this when a page needs markup beyond headings, code blocks, admonitions, and cross-references: tabs, cards, grids, figures, video, diagrams, definition lists, or version directives.

## Contents

- Page structure
- Major section (H2)
- My heading
- MyST markup
- Images, video, and diagrams

## Page structure

### Page metadata (html_meta)

```markdown
---
myst:
  html_meta:
    "description": "Description of the page content."
    "property=og:description": "Description of the page content."
    "property=og:title": "Page Title"
    "keywords": "Plone, keyword1, keyword2"
---
```

The `description` and `property=og:description` values must be identical.

**Scope:**

- **Plone core documentation** (`plone/documentation`): required on every page. This matches the policy stated in the Plone authors guide.
- **Plone ecosystem packages and add-on docs**: strongly recommended on landing pages and section indexes, the URLs people actually share. Optional but encouraged on body pages.
- **Non-Plone projects using this skill** (see "Adapting to non-Plone projects" in `planning.md`): adapt or drop it. This frontmatter shape is a Plone convention.

**Realism notes:**

- Nothing in Plone's CI enforces presence. `make html_meta` only inserts empty stubs. Empty stubs add no value. Fill them or skip them.
- The `keywords` field is SEO-dead (Google ignores it and Bing treats it as a spam signal). Include it on core docs for consistency with the policy; do not bother adding it elsewhere.
- `sphinxext-opengraph` (used by Plone) generates reasonable fallbacks from the H1 and first paragraph when `html_meta` is absent. Missing metadata on body pages degrades gracefully.
- The highest payoff per byte is `og:title` + `og:description` on pages that get linked externally (install, getting-started, top-level indexes). Prioritize there if you are triaging.

### Heading levels

```markdown
# Page title (H1) -- exactly one per page
## Major section (H2)
### Subsection (H3)
#### Sub-subsection (H4)
```

### Labels and cross-references

Create a target above any heading:

```markdown
(my-label-name)=

## My heading
```

Reference it:

```markdown
{ref}`my-label-name`
{ref}`Custom display text <my-label-name>`
```

Link to another document:

```markdown
{doc}`/path/to/document`
```

### Directory structure

- Every directory has an `index.md`.
- Static assets go in `/_static/` with section-named subdirectories.
- Include fragments go in `/_inc/`.

## MyST markup

### When to reach for which markup

Markup is a tool of attention.
Reaching for a directive signals "look here, this is different from prose."
Overuse trains readers to skip the signal.

- **Admonitions** (`note`, `tip`, `warning`, `important`, `seealso`): use sparingly, at most one or two per page.
  - `warning`: the reader can break something (data loss, irreversible action, security).
  - `important`: the reader must do this or the result is wrong, but nothing breaks.
  - `note`: a side fact that does not fit the flow but matters.
  - `tip`: an optional optimization or shortcut.
  - `seealso`: a related link cluster.
  If a `note` only restates the previous paragraph, delete it and let the prose carry the point.
- **Tabs**: use for alternative paths to the same outcome (e.g., `pip` vs `hatch` vs `uv`, or macOS vs Linux vs Windows). Do not use tabs when the outcomes differ. Those are separate pages.
- **Cards and grids**: reserve for landing pages and section indexes. Not for body content.
- **Cross-references** (`{ref}`, `{doc}`, `{term}`): always reference, never duplicate. If two pages need the same fact, one owns it and the other links. Duplicated facts drift.
- **`{guilabel}` and `{menuselection}`**: use whenever naming a real UI element. They render as visual badges and improve scanability for both readers and screen readers.
- **Inline code vs code block**: inline (`` `code` ``) for filenames, identifiers, short literals, command flags. A code block is for anything multi-line or anything needing syntax highlighting.
- **Figures vs images**: use figures (`{eval-rst} .. figure::`) when the visual needs a caption that survives outside the immediate context (search results, mobile linearization). Plain `{image}` for decorative or inline visuals.
- **`{versionremoved}`, `{versionadded}`, `{deprecated}`**: prefer over prose ("This was removed in 6.0"). The directive renders as a styled badge and is machine-readable for changelog tooling.

### Code blocks

Basic:

````markdown
```python
from plone import api
```
````

With options:

````markdown
```{code-block} python
:linenos:
:emphasize-lines: 1, 3

from plone import api
site = api.portal.get()
```
````

### Lexer selection

| Use case | Lexer |
|----------|-------|
| Terminal commands (no output) | `shell` |
| Terminal session with output | `console` |
| Python | `python` |
| XML (if highlighting fails) | try `html` |
| Nothing works | `text` |

- Shell commands: use `shell` lexer, **never include prompts** (`$`, `#`, `%`).
- Always specify a language.
- Code must be valid syntax for its language.
- Never use ellipses for omitted code. Use that language's comment syntax instead.
- Test lexers at <https://pygments.org/demo/>.

### Admonitions

```markdown
```{note}
Content here.
```

```{tip}
Content here.
```

```{warning}
Content here.
```

```{important}
Content here.
```

```{seealso}
Related links and references.
```
```

Custom title:

```markdown
```{admonition} Custom Title
:class: tip
Content here.
```
```

### Nesting directives

Outer fence must use more backticks than inner:

`````markdown
````{note}
Outer note.

```{tip}
Inner tip.
```
````
`````

### Tabs

````markdown
````{tab-set}

```{tab-item} Label1
Content 1
```

```{tab-item} Label2
Content 2
```
````
````

Synchronized tabs:

````markdown
````{tab-set}
:sync-group: category

```{tab-item} Label1
:sync: key1
Content
```
````
````

### GUI elements

```markdown
{guilabel}`Save`
{menuselection}`File --> Preferences --> Settings`
```

### Glossary terms

```markdown
{term}`content type`
```

Terms defined in `/glossary.md`.

### Definition lists

```markdown
Term
:   Definition text here.
```

### Text formatting

```markdown
**bold**
*italic*
`inline code`
~~strikethrough~~
```

### Cards (sphinx-design)

````markdown
````{card}
```{image} /_static/image.png
:alt: Description
```
+++
Caption text
````
````

### Grids (sphinx-design)

`````markdown
`````{grid} 1 1 2 2
````{grid-item-card}
:link: install/index
:link-type: doc
Content
````
`````
`````

## Images, video, and diagrams

### Images

```markdown
```{image} /_static/path/to/image.png
:alt: Description of the image
```
```

- Max width: **740 pixels**.
- For Volto screenshots: browser width 1180px.
- Alt text is **required** (accessibility).

### Figures (with captions)

````markdown
```{eval-rst}
.. figure:: /_static/path/to/diagram.png
   :alt: Description

   Caption text here.
```
````

### Inline images

```html
<img alt="description" src="path" class="inline">
```

### Videos

Local `.mp4`:

````markdown
```{video} /_static/path/to/video.mp4
:alt: Description
```
````

YouTube (privacy mode):

````markdown
```{youtube} VIDEO_ID
:privacy_mode:
:url_parameters: ?privacy_mode=1
```
````

### Mermaid diagrams

````markdown
```{mermaid}
:alt: Description
:caption: Title

graph TD
    A --> B
```
````

### Graphviz diagrams

````markdown
```{eval-rst}
.. graphviz::
    :align: center

    digraph {
        A -> B
    }
```
````
