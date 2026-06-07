---
name: internal-comms
description: Write internal company communications using established formats — 3P updates (Progress, Plans, Problems), company newsletters, FAQ responses, status reports, leadership updates, project updates, and incident reports.
license: Complete terms in LICENSE.txt
---

# Internal Comms

Writes internal communications using the formats the company uses.

## Supported Communication Types

- **3P updates** — Progress, Plans, Problems (team status updates)
- **Company newsletters** — organization-wide updates
- **FAQ responses** — structured question/answer documents
- **Status reports** — project or initiative status
- **Leadership updates** — executive/management communications
- **Project updates** — milestone and progress reports
- **Incident reports** — post-mortem and incident documentation

## Workflow

1. Identify the communication type from the user's request
2. Load the corresponding guideline from `examples/`:
   - `examples/3p-updates.md` — team progress updates
   - `examples/company-newsletter.md` — organization newsletters
   - `examples/faq-answers.md` — FAQ responses
   - `examples/general-comms.md` — all other types
3. Ask for clarification if the communication type is ambiguous or not covered
4. Draft using the loaded guidelines and provided context

## 3P Update Format

**Progress** (what we completed):
- Bullet list of completed items with concrete outcomes
- Link to relevant artifacts or metrics where applicable

**Plans** (what we're working on next):
- Bullet list of upcoming work with owners and timelines
- Flag any dependencies on other teams

**Problems** (blockers and risks):
- Bullet list of current blockers with owners
- Proposed actions for each problem
- Escalations needed (flag clearly)

## General Principles

- Match tone to audience: peer-level for 3P updates, more polished for leadership
- Lead with the most important information
- Use concrete numbers over vague language ("shipped feature X" vs "made progress")
- Keep it scannable — bullets over paragraphs for status content
- Ask for more context rather than inventing details
