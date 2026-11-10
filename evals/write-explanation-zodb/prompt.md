---
tags: [writing, explanation]
runs: 1
max_turns: 40
timeout_seconds: 900
allowed_tools: [Read, Glob, Grep, Skill, Write, Edit]
expected_outcome: A MyST explanation page why-zodb.md on the ZODB, its trade-offs, and consequences for backups and scaling.
---

For the docs of our Plone 6 project I want a page that explains why Plone stores content in the ZODB rather than in a relational database: what the ZODB is, why an object database suits a CMS, the trade-offs, and what it means for backups, deployment and scaling with ZEO or RelStorage. Please write it in MyST Markdown following the Plone docs conventions and save it as why-zodb.md in the current directory. No existing docs to read.
