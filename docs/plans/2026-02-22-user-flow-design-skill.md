# Design: `user-flow-design` Skill

**Date:** 2026-02-22
**Type:** Interactive
**Status:** Approved

## Purpose

Guides a PM from a problem statement to an agent-buildable flow spec — a screen map with ASCII wireframes, state transitions, and scenario paths that a coding agent can implement directly. No Figma step required.

## Design Decisions

- **Primary consumer:** AI coding agent (builds screens directly from the spec)
- **Detail level:** ASCII wireframes per screen (spatial layout, not pixel-level)
- **Skill type:** Interactive (adaptive questions, then generates artifact)
- **Prerequisites:** Minimal — just a problem statement. Accepts richer inputs (story maps, personas, PRDs) if available.
- **Approach:** Hybrid of full discovery pipeline + iterative per-screen validation

## Output Structure: Three Layers

### Layer 1: Screen Registry

Deduplicated list of all screens. Each screen has an ID, appears once, and is referenced across multiple scenarios. Doubles as a task list / progress tracker for implementation.

```
| ID   | Screen Name           | Status | Scenarios  |
|------|-----------------------|--------|------------|
| S-01 | Login                 | [ ]    | all        |
| S-02 | Tenant Dashboard      | [ ]    | SC-1, SC-3 |
| S-03 | New Connection Wizard | [ ]    | SC-1, SC-2 |
| S-04 | Field Mapping Review  | [ ]    | SC-1, SC-2 |
```

### Layer 2: Scenario Flows

Named paths through the screen registry. Each flow shows the happy path plus key branch points.

```
### SC-1: External user onboards file connection
S-01 → S-02 → S-03 → S-04 → S-05 → S-02

### SC-2: Admin monitors all tenants
S-01 → S-07 → S-08 → S-05
```

### Layer 3: Screen Specs

One per screen in the registry. Each contains:

- **ASCII wireframe** — rough spatial layout
- **Element inventory** — fields, buttons, tables, indicators + data each element needs
- **States** — loading, empty, populated, error + what triggers each
- **Transitions** — what action leads to which screen

Example:

```
### S-02: Tenant Dashboard

┌─────────────────────────────────────────────┐
│  Logo          Tenant: Acme Health    [▼]   │
├──────────┬──────────────────────────────────┤
│ sidebar  │  Connections                     │
│          │  ┌───────────────────────────┐   │
│ Dashboard│  │ + New Connection          │   │
│ Settings │  ├───────┬────────┬──────────┤   │
│          │  │ Name  │ Status │ Last Run │   │
│          │  │ ───── │ ────── │ ──────── │   │
│          │  │ File1 │ Active │ 2h ago   │   │
│          │  │ API-2 │ Error  │ 1d ago   │   │
│          │  └───────┴────────┴──────────┘   │
└──────────┴──────────────────────────────────┘

**Elements:**
- Tenant selector (dropdown, top-right)
- Connections table (name, status, last run)
- "+ New Connection" button

**States:**
- Empty: no connections yet → show CTA "Create your first connection"
- Populated: table with rows
- Error: API failure → inline error banner

**Transitions:**
- [+ New Connection] → S-03
- [row click] → S-05 (Connection Detail)
- [sidebar: Settings] → S-06
```

## Interactive Discovery Phase

### Question Flow (3-5 adaptive questions)

**Q1: Product Context**
> "Describe what you're building in 2-3 sentences — what it does, who uses it, and what problem it solves. Or point me to a doc/PRD."

Accepts a file path or URL to ingest an existing brief.

**Q2: User Roles**
Based on Q1, identifies candidate roles and asks user to confirm/edit:
> "I see these user roles: [1] External customer, [2] Internal admin. Correct? Add or rename any."

**Q3: Key Scenarios**
For each role, proposes 3-5 high-level scenarios, asks user to prioritize:
> "For External Customer, here are the key scenarios I see:
> 1. Onboard a new file-based connection
> 2. Onboard a new API-based connection
> 3. Monitor an existing connection
> 4. Edit connection configuration
>
> Rank by priority, remove any, or add missing ones."

**Q4: Shared Patterns** (conditional — only if repeated UI patterns detected)
> "I notice several scenarios involve a wizard flow and a dashboard view. Should I treat these as reusable screen patterns, or design each scenario's screens independently?"

**Q5: Constraints** (optional — only asks if not already clear)
> "Any constraints I should know?
> - **Tech:** component library, framework, mobile support
> - **Design:** navigation pattern (sidebar, tabs, top-nav), layout conventions, branding guidelines
> - **Scope:** screens or flows explicitly out of scope for now"

After Q3 (or Q5 if asked), the skill generates the screen registry and scenario flows.

## Screen-by-Screen Walkthrough

Screens are walked through in scenario priority order (highest-priority scenario first). Screens already spec'd are skipped when they reappear in later scenarios.

For each screen, the skill generates the wireframe + spec, then offers:

> "Does this look right? You can:
> 1. **Approve** — move to the next screen
> 2. **Adjust** — tell me what to change and I'll regenerate
> 3. **Discuss** — let's talk through this screen before deciding
> 4. **Skip** — come back to this one later"

Option 3 (Discuss) opens freeform conversation about that screen — the user can think out loud, explore alternatives, ask "what if". The skill stays on that screen until the user explicitly approves or skips.

The screen registry updates status as screens get spec'd.

## Final Artifact

A single markdown document saved to the target project's docs:

```markdown
# User Flow Spec: [Product Name]

## Constraints
- Nav: sidebar
- Framework: React
- ...

## Screen Registry
| ID   | Screen Name           | Status | Scenarios  |
|------|-----------------------|--------|------------|
| S-01 | Login                 | [x]    | all        |
| S-02 | Tenant Dashboard      | [x]    | SC-1, SC-3 |

## Scenario Flows
### SC-1: External user onboards file connection
S-01 → S-02 → S-03 → S-04 → S-05 → S-02

## Screen Specs
### S-01: Login
[wireframe + elements + states + transitions]

### S-02: Tenant Dashboard
[wireframe + elements + states + transitions]
```

## Cross-References

**Upstream skills (inputs):**
- `problem-statement` — minimal required input
- `proto-persona` — enriches role definition if available
- `user-story-mapping` — activity backbone accelerates screen identification
- `storyboard` — scenario narratives seed the flow

**Downstream consumers:**
- Coding agents (primary) — implement directly from the spec
- `prd-development` — embed the flow spec as the solution section
- `epic-breakdown-advisor` — screen registry maps to epics

## Skill Metadata

```yaml
name: user-flow-design
description: Interactive guide from problem statement to agent-buildable screen specs with ASCII wireframes
type: interactive
```

## Placement

- Path: `skills/user-flow-design/SKILL.md`
- Category: Interactive Skills
