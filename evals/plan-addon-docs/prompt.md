---
tags: [planning]
runs: 1
max_turns: 40
timeout_seconds: 900
allowed_tools: [Read, Glob, Grep, Skill, Write, Edit]
expected_outcome: A documentation plan docs-plan.md with a Diataxis coverage audit, a document tree, page specifications, and a prioritized roadmap.
---

I maintain a Plone 6 add-on called collective.newsletter. It lets editors compose newsletters from existing content, manage subscriber lists with double opt-in, schedule sending, and it exposes a REST endpoint for subscriptions that Volto blocks use. Right now there is only a README. Please plan the documentation for it: what pages we need, how they split into tutorials, how-to guides, explanation and reference, what exists and what is missing, and in which order to write them. Write the plan to docs-plan.md in the current directory.
