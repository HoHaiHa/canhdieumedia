---
name: ba:canva-spec
description: >
  Read Canva design mockups and raw requirements to generate detailed UI and business specs.
  Triggers when: user says "read canva", "spec from canva", "canva spec", or types /ba:canva-spec.
---

# /ba:canva-spec
**Role**: Business Analyst  
**Purpose**: Parse Canva designs and raw requirements to generate structured UI/UX specifications.

---

## Instructions

1. Gather raw requirements and Canva design screenshots or public Canva links.
2. If a public link is provided, use the **Browser subagent** to take a screenshot and save it to `docs/tasks/[TASK-ID]/canva-design.png`.
3. Spawn the `canva-reader` subagent (model `sonnet` via `subagent_type: "oracle"`) to parse the design.
4. Human Gate: Present preliminary findings and ask clarifying questions using `question()`.
5. Create the specification document `docs/tasks/[TASK-ID]/requirements.md` using the `templates/task-doc-canva-requirements.md` template.
6. Final Human Gate: Review and confirm specification details using `question()`.
