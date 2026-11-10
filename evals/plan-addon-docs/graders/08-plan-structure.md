---
type: llm
weight: 2
focus: { source: file, path: docs-plan.md }
---

The plan follows the Plone documentation planning method:
- It audits coverage per topic area across the four Diataxis quadrants (tutorial, how-to guide, explanation, reference) and marks each as existing, partial, missing, or not applicable.
- It proposes a document tree with filenames that use dashes and the .md extension, grouped by quadrant, with an index.md per directory.
- Each planned page has a quadrant, a one-line description, and a priority (must-have, should-have, or nice-to-have), and key pages have an opening sentence or section outline.
- It ends with a prioritized roadmap in dependency order.
- It does not organize pages by user role and does not plan single pages that mix a how-to with an explanation.
Fail if any of these points is clearly violated.
