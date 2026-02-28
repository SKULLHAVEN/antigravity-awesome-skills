---
name: superdesign
description: "Frontend UI/UX design agent that generates and iterates design drafts on an infinite canvas. Requires @superdesign/cli installed and authenticated."
source: superdesigndev/superdesign-skill (see repo)
risk: safe
---

# SuperDesign

A design agent specialized in frontend UI/UX work. Generates and iterates design drafts on an infinite canvas, helps configure design systems, and improves existing UI — invoked via `/superdesign`.

## When to Use

Use this skill when the user wants to:
- Design a new feature, page, or user flow
- Generate multiple design variations to explore options
- Set up or refine a design system for a project
- Improve or iterate on existing UI components
- Export designs as HTML for handoff

## Prerequisites

The SuperDesign CLI must be installed and authenticated before any design commands run:

```bash
npm install -g @superdesign/cli@latest
superdesign login
```

## Core Workflow

**Step 1 — Initialize**: Create `.superdesign/init/` and analyze the repo structure (components, layouts, routes, theme, pages). This happens automatically before any design task.

**Step 2 — Design System**: Read `.superdesign/design-system.md` for brand/style context. If it doesn't exist, help the user configure one.

**Step 3 — Create or Iterate**:
- New design: `superdesign create-project --title "X"` → `superdesign create-design-draft`
- Variations: `superdesign iterate-design-draft`
- Multi-page flow: `superdesign execute-flow-pages`

**Step 4 — Export**: Export final designs as HTML for implementation handoff.

## Key Commands

| Command | Purpose |
|---|---|
| `superdesign create-project --title "X"` | Start a new design project |
| `superdesign create-design-draft` | Generate initial design drafts |
| `superdesign iterate-design-draft` | Create design variations |
| `superdesign execute-flow-pages` | Extend designs across multiple pages |

## Critical Rules

- Always pass `--json` flag for machine-parseable output
- Read all mandatory init files before starting any design task
- HTML templates should reflect existing UI only — not proposed designs
- Use `askQuestion` to clarify requirements before generating
- Design system file lives at `.superdesign/design-system.md`

## Invocation

```
/superdesign help me design X
```
