---
name: qa:ui-verify
description: >
  Test actual UI implementation screenshots against Canva design mockups and write feedback.
  Triggers when: user says "ui test", "visual ui verification", "verify ui against canva", or types /qa:ui-verify.
---

# /qa:ui-verify
**Role**: QA  
**Purpose**: Compare Canva design mockups with actual UI screenshots and log layout/styling differences for Developers to fix.

---

## Instructions

1. Collect task ID, design mockup screenshot path, and actual UI capture path (or run the local server and use the browser subagent to capture actual UI).
2. Save the screenshots to `docs/tasks/[TASK-ID]/canva-design.png` and `docs/tasks/[TASK-ID]/actual-ui.png` respectively.
3. Spawn the `ui-comparator` subagent (model `sonnet` via `subagent_type: "oracle"`) to compare the two images.
4. Generate the report at `docs/tasks/[TASK-ID]/ui-feedback.md` using the `templates/ui-feedback.md` template.
5. Human Gate: Present findings summary and match score using `question()`.
6. Provide instructions for Developers to consume `ui-feedback.md` to fix layout issues.
