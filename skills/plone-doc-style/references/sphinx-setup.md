# Sphinx setup for Plone documentation

Read this only when the user sets up or changes a documentation build: `conf.py`, the theme, or Sphinx extensions. Writing pages does not need it.

## Contents

- Sphinx extensions in the Plone docs
- Plone Sphinx theme

## Sphinx extensions in the Plone docs

The list mirrors `conf.py` on the `6.0` branch of `plone/documentation`. Check that file when something here looks stale.

| Extension | Purpose |
|-----------|---------|
| `myst_parser` | MyST Markdown |
| `sphinx-design` | Grids, cards, tabs, badges, buttons, dropdowns |
| `sphinx-examples` | Source + rendered side-by-side |
| `sphinx.ext.autodoc` | Python docstring extraction |
| `sphinx.ext.intersphinx` | Cross-project linking |
| `sphinx.ext.graphviz` | Graphviz diagrams |
| `sphinxcontrib.mermaid` | Mermaid diagrams |
| `sphinxcontrib.video` | Local HTML5 video |
| `sphinxcontrib.youtube` | YouTube embedding |
| `sphinxcontrib.httpdomain` | HTTP API domain |
| `sphinxcontrib.httpexample` | curl/wget/httpie/python-requests examples |
| `sphinx_copybutton` | Copy button on code blocks |
| `sphinx-tippy` | Hover tooltips |
| `sphinx_llms_txt` | `llms.txt` export of the docs for AI agents |
| `sphinx_sitemap` | `sitemap.xml` |
| `sphinx_reredirects` | Redirects for moved or renamed pages |
| `notfound.extension` | Custom 404 page |
| `sphinxext.opengraph` | Open Graph metadata, fallbacks from H1 and first paragraph |
| `sphinx.ext.autosummary`, `doctest`, `ifconfig`, `todo`, `viewcode` | Stock Sphinx helpers enabled in the core docs |

### MyST extensions enabled

`attrs_block`, `attrs_inline`, `colon_fence`, `deflist`, `html_image`, `linkify`, `strikethrough`, `substitution`.

### Intersphinx targets

```python
"plone":   "https://6.docs.plone.org/"
"plone5":  "https://5.docs.plone.org/"
"python":  "https://docs.python.org/3/"
"training": "https://training.plone.org/"
"training-2022": "https://2022.training.plone.org/"
"training-2023": "https://2023.training.plone.org/"
"training-2024": "https://2024.training.plone.org/"
"training-2025": "https://2025.training.plone.org/"
```

## Plone Sphinx theme

All Plone ecosystem documentation must use `plone-sphinx-theme`.
It wraps `sphinx-book-theme` (which wraps `pydata-sphinx-theme`), adding Plone branding, styling, and custom directives.

### Installation

```shell
pip install plone-sphinx-theme
```

Or in `pyproject.toml`:

```toml
[project.optional-dependencies]
docs = [
    "plone-sphinx-theme",
]
```

Install `sphinx-design` separately if you need cards, grids, tabs, dropdowns:

```shell
pip install sphinx-design
```

### Minimal conf.py

```python
extensions = [
    "myst_parser",
    "sphinx_copybutton",
    "sphinx_design",
]

html_theme = "plone_sphinx_theme"
```

That single `html_theme` line is the only required theme setting. Everything else is optional.

### Recommended conf.py options

```python
html_logo = "_static/logo.svg"
html_favicon = "_static/favicon.ico"

html_sidebars = {
    "**": [
        "navbar-logo",
        "search-button-field",
        "sbt-sidebar-nav",
    ]
}

html_theme_options = {
    "extra_footer": """<p>Your footer text.</p>""",
    "footer_content_items": [
        "author",
        "copyright",
        "last-updated",
        "extra-footer",
        "icon-links",
    ],
    "icon_links": [
        {
            "name": "GitHub",
            "url": "https://github.com/org/repo",
            "icon": "fa-brands fa-square-github",
            "type": "fontawesome",
        },
    ],
    "logo": {"text": "Project Name"},
    "navigation_with_keys": True,
    "path_to_docs": "docs",
    "repository_branch": "main",
    "repository_url": "https://github.com/org/repo",
    "search_bar_text": "Search",
    "show_toc_level": 2,
    "use_edit_page_button": True,
    "use_issues_button": True,
    "use_repository_button": True,
}

# For "Edit this page" links
html_context = {
    "edit_page_url_template": "https://github.com/org/repo/edit/main/docs/{{ file_name }}",
}
```

### Custom directive: versionremoved

The theme adds a `{versionremoved}` directive (not in stock Sphinx):

````markdown
```{versionremoved} 2.0
The `old_function` was removed. Use `new_function` instead.
```
````

Also available from stock Sphinx: `{versionadded}`, `{versionchanged}`, `{deprecated}`.

### Styling details

- **Pygments style:** `monokai` (dark code blocks).
- **External links:** automatically get an external-link icon appended.
- **`{guilabel}` and `{menuselection}`:** rendered as bordered badges with info-color background.
- **Inline images** (class `inline`): rendered at `1.2em` height.
- **Videos:** full-width by default.
- **Tippy tooltips:** themed for light and dark mode.

### sphinx-tippy configuration

```python
tippy_anchor_parent_selector = "article.bd-article"
tippy_enable_doitips = False
tippy_enable_wikitips = False
tippy_props = {
    "interactive": True,
    "placement": "auto-end",
}
```
