# User Flow Design Skill — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Create an interactive skill that guides PMs from a problem statement to agent-buildable screen specs with ASCII wireframes, a screen registry (doubles as task list), and scenario flows.

**Architecture:** Single interactive skill at `skills/user-flow-design/SKILL.md` with a companion `template.md` for the output artifact. Follows the lean-ux-canvas pattern: adaptive questions → iterative screen walkthrough → exported artifact. The screen registry is the central data structure — screens are entities, flows are paths through them.

**Tech Stack:** Markdown skill files, YAML frontmatter, validated by `scripts/check-skill-metadata.py` and `scripts/test-a-skill.sh`.

**Design doc:** `docs/plans/2026-02-22-user-flow-design-skill.md`

---

### Task 1: Create skill directory and frontmatter + Purpose section

**Files:**
- Create: `skills/user-flow-design/SKILL.md`

**Step 1: Create the skill file with frontmatter and Purpose**

```markdown
---
name: user-flow-design
description: Guide product managers from a problem statement to agent-buildable screen specs with ASCII wireframes, a screen registry, and scenario flows.
type: interactive
---

## Purpose

Guide product managers from a **problem statement** to a complete **user flow specification** that a coding agent can implement directly — no Figma step required.

The skill produces three artifacts:
1. **Screen Registry** — deduplicated inventory of all screens with IDs, names, and status. Doubles as an implementation task list and progress tracker.
2. **Scenario Flows** — named paths through the screen registry showing how users move through the product.
3. **Screen Specs** — ASCII wireframes, element inventories, state definitions, and transition maps for each screen.

Use this when you know *what* you're building (even roughly) and need to define *how users will interact with it* at a screen level. The output goes straight to a coding agent for implementation.
```

**Step 2: Run metadata validation**

Run: `python3 scripts/check-skill-metadata.py skills/user-flow-design/SKILL.md`
Expected: Errors about missing sections (Key Concepts, Application, etc.) — that's fine, frontmatter should pass.

**Step 3: Commit**

```bash
git add skills/user-flow-design/SKILL.md
git commit -m "feat(user-flow-design): scaffold skill with frontmatter and Purpose"
```

---

### Task 2: Write Key Concepts section

**Files:**
- Modify: `skills/user-flow-design/SKILL.md`

**Step 1: Add Key Concepts after Purpose**

```markdown
## Key Concepts

### The Three-Layer Model

User flows are built from three layers that reference each other:

**Screen Registry (the index):**
Every screen exists once, identified by a stable ID (S-01, S-02, ...). The registry tracks which scenarios use each screen and whether it's been spec'd. This is the master reference — coding agents use it as a task list.

**Scenario Flows (the paths):**
A scenario is a named sequence of screens that accomplishes a user goal (e.g., "External user onboards a file-based connection"). Scenarios reference screen IDs, not screen names — so renaming a screen doesn't break flows.

**Screen Specs (the detail):**
Each screen gets an ASCII wireframe, element inventory, state definitions, and transition map. Screens are spec'd once even if they appear in multiple scenarios.

---

### Screens Are Entities, Flows Are Paths

A common mistake: designing flows as linear sequences where the same screen gets described differently each time it appears. Instead, treat screens as reusable entities. A dashboard screen is one screen — it appears in the onboarding flow, the monitoring flow, and the config editing flow. The flows just reference it.

This matters for coding agents: one screen = one component = one implementation task.

---

### ASCII Wireframes: Why and How

ASCII wireframes give coding agents spatial context without over-constraining layout. They communicate:
- **Layout structure** — sidebar vs. top-nav, content regions, form arrangements
- **Element placement** — where buttons, tables, and forms sit relative to each other
- **Visual hierarchy** — what's prominent vs. secondary

They don't communicate: colors, typography, pixel spacing, responsive breakpoints. The coding agent fills those in from the component library and design system.

**Box-drawing characters to use:**
```
┌─┐  └─┘  ├─┤  ┬  ┴  │  ─  ╔═╗  ╚═╝
```

---

### Screen States

Every screen has multiple states. Specify at minimum:
- **Loading** — what the user sees while data loads
- **Empty** — first-time or no-data state (often has a CTA)
- **Populated** — normal state with data
- **Error** — what happens when something fails

Skip states that don't apply (a static settings page has no "loading" state).

---

### When to Use This

Use this when:
- You have a problem statement or brief and need to define the UI
- You're handing off to a coding agent (Claude, Codex, etc.) for implementation
- You want a shared reference for screen inventory and user paths
- You need a progress tracker for screen-by-screen implementation

Don't use this when:
- You're still exploring whether to build (use `lean-ux-canvas` first)
- You need pixel-perfect mockups (use Figma after this)
- The product is a single-screen tool with no navigation

---

### Facilitation Source of Truth

Use [`workshop-facilitation`](../workshop-facilitation/SKILL.md) as the default interaction protocol for this skill.

It defines:
- session heads-up + entry mode (Guided, Context dump, Best guess)
- one-question turns with plain-language prompts
- progress labels (for example, Context Qx/5 and Screen Sx/N)
- interruption handling and pause/resume behavior
- numbered recommendations at decision points
- quick-select numbered response options for regular questions (include `Other (specify)` when useful)

This file defines the domain-specific assessment content. If there is a conflict, follow this file's domain logic.
```

**Step 2: Run metadata validation**

Run: `python3 scripts/check-skill-metadata.py skills/user-flow-design/SKILL.md`
Expected: Errors about missing sections (Application, Examples, etc.) — Key Concepts should now pass.

**Step 3: Commit**

```bash
git add skills/user-flow-design/SKILL.md
git commit -m "feat(user-flow-design): add Key Concepts section"
```

---

### Task 3: Write Application section — Discovery Phase (Questions 1-5)

**Files:**
- Modify: `skills/user-flow-design/SKILL.md`

**Step 1: Add Application section with discovery questions**

```markdown
## Application

Use `template.md` for the full output artifact structure.

This interactive skill works in two phases: **Discovery** (3-5 adaptive questions to identify screens and scenarios) and **Walkthrough** (iterative screen-by-screen spec generation with user validation). The discovery phase generates the screen registry and scenario flows; the walkthrough phase fills in the screen specs.

---

### Phase 1: Discovery

#### Step 0: Gather Context

**Agent asks:**

Before we design your user flows, let's gather context. Please share:

- **Product description** — What it does, who uses it, what problem it solves (2-3 sentences is fine)
- **Existing docs** — PRD, brief, discovery notes, or file path to any of these
- **Design constraints** — If you already know: nav pattern (sidebar, tabs, top-nav), component library, mobile/desktop, branding guidelines

You can paste a description, point to a file, or just describe it briefly.

---

#### Question 1: User Roles (Context Q1/5)

**Agent asks:**

Based on what you've shared, I see these user roles:

1. **[Role A]** — [one-line description]
2. **[Role B]** — [one-line description]
3. **Other (specify)**

Correct? Add, remove, or rename any.

**Agent validates:** Each role should be a distinct person with different permissions, goals, or screen access. Merge roles that see the same screens. Split roles that need different views of the same data.

---

#### Question 2: Key Scenarios (Context Q2/5)

**Agent asks:**

For each role, here are the key scenarios I see:

**[Role A]:**
1. [Scenario 1 — verb + goal]
2. [Scenario 2 — verb + goal]
3. [Scenario 3 — verb + goal]

**[Role B]:**
1. [Scenario 4 — verb + goal]
2. [Scenario 5 — verb + goal]

Rank by priority (highest first), remove any, or add missing ones.

**Agent validates:** Each scenario should be a complete user goal, not a single click. "Configure a new connection" is a scenario. "Click the save button" is not.

---

#### Question 3: Shared Patterns (Context Q3/5 — conditional)

**Only ask this if the agent detects repeated UI patterns across scenarios (e.g., multiple wizard flows, multiple dashboards, multiple detail views).**

**Agent asks:**

I notice these recurring patterns across your scenarios:

1. **[Pattern A]** — appears in [Scenario 1, 3, 5] (e.g., "wizard flow with sequential steps")
2. **[Pattern B]** — appears in [Scenario 2, 4] (e.g., "dashboard with data table + detail view")
3. **No shared patterns** — design each scenario's screens independently

Should I treat these as reusable screen templates, or keep each scenario's screens independent?

**Agent validates:** Reusable patterns reduce the screen count and make implementation more consistent. Independent screens give more flexibility per scenario. Default to reusable unless the user has a reason not to.

---

#### Question 4: Constraints (Context Q4/5 — optional)

**Only ask if constraints weren't provided in Step 0.**

**Agent asks:**

Any constraints I should factor into the wireframes?

- **Tech:** component library, framework, mobile support, accessibility requirements
- **Design:** navigation pattern (sidebar, tabs, top-nav), layout conventions, branding guidelines, max content width
- **Scope:** screens or flows explicitly out of scope for now

1. **I have constraints to share** — [describe them]
2. **No constraints — use sensible defaults** — [Agent uses: sidebar nav, desktop-first, standard form/table patterns]
3. **Other (specify)**

---

#### Question 5: Generate Screen Registry and Scenario Flows

**This is not a question — the agent generates the output.**

Based on the discovery answers, the agent:

1. **Generates the Screen Registry** — lists every screen needed across all scenarios, deduplicated, with IDs assigned sequentially (S-01, S-02, ...).
2. **Generates Scenario Flows** — maps each scenario as a path through screen IDs.
3. **Presents both for validation:**

**Screen Registry:**

| ID   | Screen Name              | Status | Scenarios       |
|------|--------------------------|--------|-----------------|
| S-01 | [Screen name]            | [ ]    | [SC-1, SC-2]    |
| S-02 | [Screen name]            | [ ]    | [SC-1]          |
| ...  |                          |        |                 |

**Scenario Flows:**

- **SC-1: [Scenario name]** — S-01 → S-02 → S-03 → S-04 → S-01
- **SC-2: [Scenario name]** — S-01 → S-05 → S-06 → S-01

Does this screen inventory and flow mapping look right?

1. **Approve** — move to screen-by-screen walkthrough
2. **Adjust** — add, remove, or rename screens / reorder flows
3. **Discuss** — let's talk through the structure before proceeding
4. **Other (specify)**
```

**Step 2: Commit**

```bash
git add skills/user-flow-design/SKILL.md
git commit -m "feat(user-flow-design): add Application discovery phase (Q1-Q5)"
```

---

### Task 4: Write Application section — Walkthrough Phase

**Files:**
- Modify: `skills/user-flow-design/SKILL.md`

**Step 1: Add Phase 2 (Walkthrough) after Phase 1 in Application**

```markdown
---

### Phase 2: Screen-by-Screen Walkthrough

Screens are walked through in **scenario priority order** — the highest-priority scenario's screens first. When a screen reappears in a later scenario, skip it (it's already spec'd).

#### For Each Screen

The agent generates the following spec:

**[S-XX]: [Screen Name]**

**ASCII Wireframe:**
```
┌─────────────────────────────────────────────┐
│  [header area]                              │
├──────────┬──────────────────────────────────┤
│ [nav]    │  [content area]                  │
│          │  [primary elements]              │
│          │  [data display / forms]          │
│          │                                  │
└──────────┴──────────────────────────────────┘
```

**Elements:**
- [Element name] — [type: button/field/table/indicator] — [data needed]
- [Element name] — [type] — [data needed]

**States:**
- **Loading:** [what user sees while data loads]
- **Empty:** [first-time / no-data state + CTA if applicable]
- **Populated:** [normal state with data]
- **Error:** [what happens when something fails]

**Transitions:**
- `[action]` → S-XX ([Screen Name])
- `[action]` → S-XX ([Screen Name])

---

#### After Each Screen

**Agent asks:**

Screen S-XX ([Screen Name]) — does this look right? You can:

1. **Approve** — move to the next screen
2. **Adjust** — tell me what to change and I'll regenerate
3. **Discuss** — let's talk through this screen before deciding
4. **Skip** — come back to this one later

**Option 3 (Discuss)** opens freeform conversation. The user can think out loud, ask "what if," explore alternatives, or rubber-duck their way to clarity. The agent stays on this screen until the user explicitly approves or skips.

**Progress tracking:** After each approval or skip, the agent shows the updated registry:

```
Screen Registry: 3/12 spec'd  [███░░░░░░░░░] 25%
Next: S-04 (Field Mapping Review)
```

---

#### Handling Skipped Screens

After completing all screens in priority order, the agent returns to skipped screens:

"You skipped these screens earlier:
- S-06 (Settings) — skipped during SC-1
- S-09 (Error Detail) — skipped during SC-2

Want to spec them now, or leave them for later?"

---

### Phase 3: Review and Export

**Agent presents the complete artifact:**

Here's your complete User Flow Spec:

[Full artifact using template.md structure — constraints, screen registry, scenario flows, all screen specs]

**Next steps:**

1. **Export as file** — save to your project's docs (e.g., `docs/plans/YYYY-MM-DD-user-flows.md`)
2. **Refine a screen** — revisit any screen spec for changes
3. **Add a scenario** — define a new flow through existing screens
4. **Suggest related skills** — what to do next (e.g., `epic-breakdown-advisor` to turn screens into epics)

**Agent saves:** The artifact to the target project's docs directory when the user selects option 1.
```

**Step 2: Commit**

```bash
git add skills/user-flow-design/SKILL.md
git commit -m "feat(user-flow-design): add Application walkthrough and export phases"
```

---

### Task 5: Write Examples section

**Files:**
- Modify: `skills/user-flow-design/SKILL.md`

**Step 1: Add Examples section**

```markdown
## Examples

### Example: Data Integration Portal (2 roles, 4 scenarios)

**Context provided:**
> "Self-service portal for onboarding data integrations. External customers configure file or API connections. Internal admins manage all tenants."

**Discovery output:**

**Roles:** External Customer, Vim Admin

**Scenarios (prioritized):**
1. SC-1: External customer onboards file-based connection
2. SC-2: External customer monitors existing connection
3. SC-3: Vim admin manages all tenants
4. SC-4: External customer onboards API-based connection

**Screen Registry (10 screens):**

| ID   | Screen Name               | Status | Scenarios       |
|------|---------------------------|--------|-----------------|
| S-01 | Login                     | [x]    | all             |
| S-02 | Tenant Dashboard          | [x]    | SC-1, SC-2, SC-4|
| S-03 | New Connection Wizard     | [x]    | SC-1, SC-4      |
| S-04 | Field Mapping Review      | [x]    | SC-1, SC-4      |
| S-05 | Value Mapping Config      | [x]    | SC-1, SC-4      |
| S-06 | Test & Activate           | [x]    | SC-1, SC-4      |
| S-07 | Connection Detail (File)  | [x]    | SC-2            |
| S-08 | Connection Detail (API)   | [x]    | SC-2            |
| S-09 | Admin: All Tenants        | [x]    | SC-3            |
| S-10 | Settings                  | [x]    | SC-1, SC-3      |

**Scenario Flow SC-1:**
S-01 → S-02 → S-03 → S-04 → S-05 → S-06 → S-02

**Sample Screen Spec — S-02: Tenant Dashboard:**

```
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
```

**Elements:**
- Tenant selector (dropdown, top-right) — current tenant name, list of user's tenants
- Connections table (name, type, status, last run) — data from connections API
- "+ New Connection" button — primary CTA
- Sidebar nav (Dashboard, Settings)

**States:**
- Empty: no connections → "Create your first connection" CTA with illustration
- Populated: table with connection rows, sortable by status
- Error: API failure → inline error banner above table

**Transitions:**
- `[+ New Connection]` → S-03 (New Connection Wizard)
- `[row click]` → S-07 or S-08 (Connection Detail, based on type)
- `[sidebar: Settings]` → S-10 (Settings)
- `[tenant selector]` → reload dashboard for selected tenant

---

### Example Conversation Flow (Discuss mode)

**Agent:** Screen S-03 (New Connection Wizard) — does this look right?
1. Approve  2. Adjust  3. Discuss  4. Skip

**User:** 3

**Agent:** Let's talk through it. What's on your mind about this screen?

**User:** I'm not sure if the wizard should be one long form or separate steps with a stepper. The file path has 5 config steps and the API path has 3.

**Agent:** Good question. Two options:

**Stepper with distinct pages:** Each config step is its own page. The stepper shows progress (Step 2 of 5). Pros: less overwhelming, easier to save partial progress. Cons: more navigation, user can't see everything at once.

**Accordion within a single page:** All steps visible as collapsible sections. Expand one at a time. Pros: user sees the full scope, faster for power users. Cons: long page, harder to track required vs. optional.

For a wizard with 5 steps where some steps depend on previous answers (like field mapping depends on file upload), the stepper pattern is usually better — it enforces sequence and keeps cognitive load low.

**User:** Stepper makes sense. Let's go with that. Can the steps be different for file vs. API?

**Agent:** Yes — the wizard shares S-03 as the entry point but branches after step 1 (choose connection type). I'll update the wireframe to show a stepper header and note the branching. Let me regenerate.

[Agent regenerates S-03 wireframe with stepper]
```

**Step 2: Commit**

```bash
git add skills/user-flow-design/SKILL.md
git commit -m "feat(user-flow-design): add Examples section with data portal walkthrough"
```

---

### Task 6: Write Common Pitfalls and References sections

**Files:**
- Modify: `skills/user-flow-design/SKILL.md`

**Step 1: Add Common Pitfalls**

```markdown
## Common Pitfalls

### 1. Designing Flows, Not Screens
**Failure Mode:** Creating a linear sequence where the same screen is described differently each time it appears (e.g., "Dashboard after login" vs. "Dashboard after saving").

**Consequence:** The coding agent builds multiple versions of the same screen, or builds one and the flow spec contradicts itself.

**Fix:** One screen = one entry in the registry = one spec. Flows reference screen IDs. If a screen looks different depending on context, that's a state — add it to the screen's States section.

---

### 2. Wireframes Too Detailed or Too Vague
**Failure Mode:** Either specifying pixel-level layout ("the button is 120px wide, 8px from the right edge") or being so abstract the agent can't infer layout ("there's a form and a table").

**Consequence:** Over-detailed wireframes fight the component library. Under-detailed wireframes produce random layouts.

**Fix:** Show spatial arrangement (sidebar left, table center, button top-right) using box-drawing characters. Let the component library handle sizing and spacing.

---

### 3. Missing States
**Failure Mode:** Only specifying the "populated" state. Forgetting empty, loading, and error.

**Consequence:** The agent builds the happy path and the first user who has no data sees a blank screen.

**Fix:** For every screen, ask: "What does this look like with zero data? While loading? When the API fails?" Spec all applicable states.

---

### 4. Scenarios That Are Too Granular
**Failure Mode:** Creating a scenario for every possible user action ("User clicks edit button," "User clicks delete button").

**Consequence:** The scenario list explodes, flows overlap heavily, and the spec becomes unreadable.

**Fix:** Scenarios should be user goals, not user actions. "Edit connection configuration" is a scenario. "Click the edit button" is a transition within a screen spec.

---

### 5. Skipping the Discussion Step
**Failure Mode:** Approving every screen without thinking it through, then discovering problems during implementation.

**Consequence:** Rework. The coding agent builds screens that don't make sense together.

**Fix:** Use "Discuss" (option 3) for any screen where you're not sure. Thinking out loud with the agent is faster than rebuilding after implementation.
```

**Step 2: Add References**

```markdown
## References

### Related Skills
- **[problem-statement](skills/problem-statement/SKILL.md)** (Component) — Minimal required input for this skill; frame the problem before designing screens
- **[proto-persona](skills/proto-persona/SKILL.md)** (Component) — Enriches role definitions with behavioral and motivational detail
- **[user-story-mapping](skills/user-story-mapping/SKILL.md)** (Component) — Activity backbone that accelerates screen identification
- **[storyboard](skills/storyboard/SKILL.md)** (Component) — 6-frame scenario narratives that seed the flow design
- **[lean-ux-canvas](skills/lean-ux-canvas/SKILL.md)** (Interactive) — Use before this skill if you're still validating whether to build
- **[prd-development](skills/prd-development/SKILL.md)** (Workflow) — Embed the flow spec as the solution section of a PRD
- **[epic-breakdown-advisor](skills/epic-breakdown-advisor/SKILL.md)** (Interactive) — Turn the screen registry into epics and user stories for implementation

### External Frameworks
- **Jeff Patton** — *User Story Mapping* (O'Reilly, 2014) — backbone-first approach to flow design
- **Ryan Singer** — *Shape Up* (Basecamp, 2019) — breadboarding technique for rough screen sketches
- **Steve Krug** — *Don't Make Me Think* (New Riders, 2000) — usability principles for screen design
```

**Step 3: Commit**

```bash
git add skills/user-flow-design/SKILL.md
git commit -m "feat(user-flow-design): add Common Pitfalls and References sections"
```

---

### Task 7: Create the output artifact template

**Files:**
- Create: `skills/user-flow-design/template.md`

**Step 1: Write the template**

```markdown
# User Flow Spec: [Product Name]

**Date:** [YYYY-MM-DD]
**Roles:** [Role 1, Role 2, ...]
**Scenarios:** [count] scenarios across [count] screens

---

## Constraints

- **Navigation:** [sidebar / tabs / top-nav / other]
- **Framework:** [React / Vue / other / none specified]
- **Target:** [desktop-first / mobile-first / responsive]
- **Component library:** [library name / none specified]
- **Design guidelines:** [any specific conventions]
- **Out of scope:** [screens or flows excluded]

---

## Screen Registry

| ID   | Screen Name | Status | Scenarios |
|------|-------------|--------|-----------|
| S-01 | [name]      | [ ]    | [SC-x]    |
| S-02 | [name]      | [ ]    | [SC-x]    |

**Progress:** 0/[N] screens spec'd

---

## Scenario Flows

### SC-1: [Scenario name — Role: verb + goal]

S-01 → S-02 → S-03 → S-01

**Branch points:**
- At S-03, if [condition] → S-04 (alternate path)

---

## Screen Specs

### S-01: [Screen Name]

**Wireframe:**

```
┌─────────────────────────────────────────────┐
│  [header]                                   │
├──────────┬──────────────────────────────────┤
│ [nav]    │  [content]                       │
│          │                                  │
└──────────┴──────────────────────────────────┘
```

**Elements:**
- [Element] — [type] — [data source]

**States:**
- **Loading:** [description]
- **Empty:** [description + CTA]
- **Populated:** [description]
- **Error:** [description]

**Transitions:**
- `[action]` → S-XX ([Screen Name])
```

**Step 2: Commit**

```bash
git add skills/user-flow-design/template.md
git commit -m "feat(user-flow-design): add output artifact template"
```

---

### Task 8: Run full validation

**Files:**
- Verify: `skills/user-flow-design/SKILL.md`

**Step 1: Run metadata check**

Run: `python3 scripts/check-skill-metadata.py skills/user-flow-design/SKILL.md`
Expected: All checks pass (frontmatter valid, all 6 sections present and in order, folder name matches).

**Step 2: Run test script**

Run: `bash scripts/test-a-skill.sh --skill user-flow-design`
Expected: PASS on conformance and linked skill paths.

**Step 3: Run smoke test**

Run: `bash scripts/test-a-skill.sh --skill user-flow-design --smoke`
Expected: PASS on non-empty sections, >= 3 numbered items in Application, >= 1 question mark.

**Step 4: Fix any failures, then re-run all three checks and commit**

```bash
git add skills/user-flow-design/
git commit -m "fix(user-flow-design): address validation findings"
```

---

### Task 9: Update README.md with new skill

**Files:**
- Modify: `README.md`

**Step 1: Add skill to the Interactive Skills table**

In the `### 🔄 Interactive Skills` table (around line 262), add the new skill in **alphabetical order** among the existing entries. It should go after `user-story-mapping-workshop` and before `workshop-facilitation`:

```markdown
| **[user-flow-design](skills/user-flow-design/SKILL.md)** | Guides you from a problem statement to agent-buildable screen specs with ASCII wireframes, screen registry, and scenario flows |
```

**Step 2: Update the skill count**

- Update the Interactive Skills count from `(18)` to `(19)` in the heading and architecture diagram
- Update the total count from `42` to `43` wherever it appears (heading, architecture text, etc.)

**Step 3: Commit**

```bash
git add README.md
git commit -m "docs: add user-flow-design to README skill catalog"
```

---

### Task 10: Update CLAUDE.md project status

**Files:**
- Modify: `CLAUDE.md`

**Step 1: Add user-flow-design to the project status**

In the project status section, add a note about the new skill under Phase 6 or as a standalone addition, depending on whether Dean considers this part of Phase 6 or a new phase.

**Step 2: Update skill counts**

Update the total skill count from 42 to 43, and update the Interactive Skills count from 18 to 19.

**Step 3: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: update CLAUDE.md with user-flow-design skill status"
```
