# Planning mode

Read this when the user asks to plan, structure, audit, or outline documentation. It holds the coverage matrix and the plan template.

## Contents

- Planning process
- Diataxis coverage matrix
- Output: documentation plan
- Planning anti-patterns
- Adapting to non-Plone projects

Use this mode when the user wants to plan, structure, audit, or outline documentation for a project, package, feature, or entire site.

## Planning process

1. **Understand scope.** What is being documented? A single package? A feature area? An entire project? Ask if unclear.
2. **Inventory existing content.** Read existing docs, README files, docstrings, and changelog to understand what already exists.
3. **Identify the audience(s).** Who will read this? Beginners, integrators, developers, admins? This drives Diataxis balance.
4. **Apply the Diataxis grid.** For every topic area, ask: what does the reader need?

## Diataxis coverage matrix

For each topic area, fill in this grid to find gaps:

```
Topic area: [e.g., "Content types"]
┌─────────────────────┬─────────────────────┐
│ TUTORIAL             │ HOW-TO GUIDE         │
│ "Learn content       │ "How to create a     │
│  types by building   │  custom content      │
│  one from scratch"   │  type with behavior" │
│ Status: [missing]    │ Status: [exists]     │
├─────────────────────┼─────────────────────┤
│ EXPLANATION          │ REFERENCE            │
│ "About content       │ "Content type        │
│  types: FTI, schema, │  schema fields       │
│  behaviors, and why" │  and directives"     │
│ Status: [partial]    │ Status: [exists]     │
└─────────────────────┴─────────────────────┘
```

Produce one grid per topic area. Mark each cell:
- **exists**: page exists and is adequate.
- **partial**: page exists but incomplete or mixes quadrants.
- **missing**: no page covers this need.
- **n/a**: this quadrant genuinely does not apply (rare).

## Output: documentation plan

Deliver the plan as a structured document with these sections:

### I. Overview

- Project/package name and purpose (1-2 sentences).
- Target audiences.
- Scope boundaries (what is and is not covered).

### II. Diataxis coverage audit

The coverage matrix (see "Diataxis coverage matrix" above) for every identified topic area.
Highlight gaps and mixed-quadrant pages that need splitting.

### III. Document tree (TOC)

A proposed file/folder structure. Use Plone conventions:

```
docs/
├── index.md                          # Landing page with grid cards
├── tutorials/
│   ├── index.md
│   ├── first-content-type.md         # Tutorial
│   └── first-viewlet.md              # Tutorial
├── how-to/
│   ├── index.md
│   ├── create-custom-content-type.md # How-to
│   └── configure-caching.md          # How-to
├── explanation/
│   ├── index.md
│   ├── content-types.md              # Explanation
│   └── caching-architecture.md       # Explanation
└── reference/
    ├── index.md
    ├── schema-fields.md              # Reference
    └── configuration-options.md      # Reference
```

Each entry states:
- Filename (dashes, `.md`).
- Diataxis quadrant.
- One-line description of content.
- Priority: **must-have**, **should-have**, or **nice-to-have**.
- Dependencies (pages that should exist first).

### IV. Page specifications

For each planned page, provide:

```
Page: how-to/create-custom-content-type.md
Quadrant: How-to guide
Title: "How to create a custom content type"
Opening: "This guide shows you how to create a custom content type with a schema and a behavior."
Audience: Developers with basic Plone knowledge
Prerequisites: Working Plone installation
Sections (estimated):
  1. Define the schema
  2. Register the FTI
  3. Add a behavior
  4. Verify in the control panel
Estimated length: ~120 lines
Cross-references: {ref}`content-type-explanation`, {ref}`schema-fields-reference`
```

### V. Prioritized roadmap

Order pages by priority and dependency:

1. **Phase 1 (must-have):** Pages without which the docs are incomplete.
2. **Phase 2 (should-have):** Pages that fill important gaps.
3. **Phase 3 (nice-to-have):** Pages that round out coverage.

Within each phase, list pages in dependency order (prerequisite pages first).

### VI. Style and consistency notes

- Naming conventions specific to this project.
- Glossary terms to define.
- Cross-reference strategy (how pages link to each other).
- Any deviations from standard Plone docs conventions (with justification).

## Planning anti-patterns

- **Do not plan pages that mix quadrants.** If a topic needs both a how-to and an explanation, plan two separate pages.
- **Do not plan encyclopedic coverage.** Prioritize what readers actually need. Practical usability beats exhaustive completeness.
- **Do not plan around user roles.** Organize by what the reader wants to achieve. Whether they are a "developer" or an "admin" is irrelevant.
- **Do not front-load all tutorials.** A balanced docs set needs all four quadrants. Reference and explanation are not afterthoughts.
- **Do not create deep nesting.** Two levels of folders is usually sufficient. Three is the maximum.

## Adapting to non-Plone projects

This planning framework works for any Sphinx/MyST documentation project.
When planning docs outside the Plone core documentation repository:

- The MyST markup rules, Diataxis framework, and style conventions still apply.
- Adjust the directory structure to match the project's conventions.
- If the project uses a different Sphinx theme, note any markup differences.
- The `html_meta` frontmatter is Plone-specific. Other projects may use different metadata.
- Vale and linkcheck are recommended but may not be configured. Note this in the plan.
