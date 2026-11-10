---
tags: [writing, how-to]
runs: 1
max_turns: 40
timeout_seconds: 900
allowed_tools: [Read, Glob, Grep, Skill, Write, Edit]
expected_outcome: A MyST how-to page send-email-smtp.md that stays in the how-to quadrant and passes the Plone prose rules.
---

I need a page for our Plone 6 docs about sending email through an external SMTP server: the settings in the Mail control panel, how to set the same values from a GenericSetup profile or from environment variables in a container, and how to verify that mail actually leaves the site. Write it as a how-to guide in MyST Markdown and save it as send-email-smtp.md in the current directory. There are no existing docs to read; write from your knowledge of Plone 6.
