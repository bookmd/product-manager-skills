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

## Key Concepts

### The Three-Layer Model

Every user flow spec produced by this skill has three layers:

1. **Screen Registry** — The index. A deduplicated inventory of every unique screen with an ID (e.g., `S-01`, `S-02`), a name, and a status checkbox. It doubles as an implementation task list — check off screens as they're built.
2. **Scenario Flows** — Named paths through the screen registry. Each scenario (e.g., `SC-1: First-Time Setup`) is a sequence of screen IDs showing how a user moves through the product to accomplish a goal.
3. **Screen Specs** — The detail layer. For each screen: an ASCII wireframe, an element inventory, state definitions (Loading, Empty, Populated, Error), and a transition map showing where each action leads.

The registry is the source of truth. Flows reference it. Specs elaborate it. A coding agent reads the registry for scope, the flows for navigation logic, and the specs for implementation detail.

---

### Screens Are Entities, Flows Are Paths

The most common mistake in flow design: treating flows as linear sequences where the same screen gets described differently each time it appears.

**Wrong approach:** "In the onboarding flow, the dashboard shows a welcome banner. In the monitoring flow, the dashboard shows metrics." Now you have two conflicting specs for one screen.

**Right approach:** One screen = one entry in the registry = one spec = one component = one implementation task. The dashboard screen (S-02) has one spec that covers all its states and entry points. Flows simply reference `S-02` — they don't redefine it.

This deduplication matters because:
- Coding agents build **screens**, not flows. One spec per screen = one component per screen.
- The registry becomes a progress tracker. You can't track progress if the same screen appears three times with different descriptions.
- Contradictions disappear. There's one place to look for "what does this screen do?"

---

### ASCII Wireframes: Why and How

ASCII wireframes give coding agents **spatial context** without over-constraining implementation. They communicate:
- **Layout structure** — header, sidebar, main content, footer
- **Element placement** — where buttons, tables, forms, and labels sit relative to each other
- **Visual hierarchy** — what's prominent vs. secondary

They do **not** communicate:
- Colors, typography, or theming
- Pixel spacing or exact dimensions
- Component library specifics (that's the agent's job)

**Box-drawing characters to use:**

```
┌─┐  └─┘  ├─┤  ┬  ┴  │  ─
```

**Example:**

```
┌──────────────────────────────────────────┐
│  Logo          [Search...]    [Profile ▾]│
├──────────────────────────────────────────┤
│ ┌──────┐  ┌────────────────────────────┐ │
│ │ Nav  │  │  Page Title                │ │
│ │      │  │  ┌────────────────────────┐ │ │
│ │ Link │  │  │  Content Area          │ │ │
│ │ Link │  │  │                        │ │ │
│ │ Link │  │  └────────────────────────┘ │ │
│ └──────┘  │  [Primary Action]          │ │
│           └────────────────────────────┘ │
└──────────────────────────────────────────┘
```

Keep wireframes between 10-25 lines. Enough to show structure, not enough to bikeshed layout.

---

### Screen States

Every screen has states. At minimum, consider these four:

| State | Description | When it applies |
|-------|------------|-----------------|
| **Loading** | Skeleton or spinner while data fetches | Screen depends on async data |
| **Empty** | Zero-data state with call to action | First use, no records yet |
| **Populated** | Normal state with data | Happy path |
| **Error** | API failure, permission denied, timeout | Any data-dependent screen |

Skip states that genuinely don't apply (a static "About" page has no Loading state). But default to including them — coding agents who handle all four states ship more resilient UIs.

---

### When to Use This

**Use this when:**
- You have a problem statement or product brief and need to define the user experience at screen level
- You're handing off to a coding agent and need a shared reference for what to build
- You need a deduplicated screen inventory that doubles as an implementation tracker
- Multiple scenarios share screens and you need a single source of truth

**Don't use this when:**
- You're still exploring whether to build — use **[lean-ux-canvas](skills/lean-ux-canvas/SKILL.md)** first to validate assumptions
- You need pixel-perfect designs — use Figma after this skill to add visual polish
- You're building a single-screen tool with no navigation — just describe the screen directly

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

## Application

Use `template.md` for the full output artifact structure.

This interactive skill works in **three phases**: **Discovery** (3-5 adaptive questions to understand scope), **Walkthrough** (iterative screen-by-screen spec generation), and **Review & Export** (final artifact assembly). Discovery builds the registry and flows. Walkthrough fills in every screen spec. Review & Export produces the final document.

---

### Phase 1: Discovery

#### Step 0: Gather Context

**Agent asks:**

Before we design screens, I need to understand what we're building. Please share:

**Product Context:**
- Product description or problem statement
- Existing docs (PRD, brief, lean UX canvas, user story map)
- Design constraints (component library, framework, mobile/desktop, nav pattern)

**You can:**
- Paste a document or link to a file
- Point me to a file in the project (e.g., `docs/prd.md`)
- Describe the product briefly in your own words

I'll extract what I need and ask follow-up questions if anything is unclear.

---

#### Question 1: User Roles (Context Q1/5)

**Agent asks:**

Based on what you've shared, I see these user roles:

1. **[Role A]** — [brief description of permissions/goals/screen access]
2. **[Role B]** — [brief description of permissions/goals/screen access]
3. **Other** — Tell me about a role I missed

Do these look right? Edit, remove, or add roles.

**Agent validates:** Each role must have distinct permissions, goals, or screen access. If two roles see the same screens and do the same things, they're one role. If one role has admin powers the other doesn't, they're separate.

---

#### Question 2: Key Scenarios (Context Q2/5)

**Agent asks:**

For each role, here are the key scenarios I'd expect (verb + goal format):

**[Role A]:**
1. Configure new integration
2. Monitor sync status
3. Troubleshoot failed sync

**[Role B]:**
1. Review all tenant integrations
2. Manage user permissions
3. Override failed syncs

Rank these by priority (most important first), remove any that are out of scope, or add scenarios I missed.

**Agent validates:** Each scenario should represent a complete user goal, not a single click. "Click the save button" is an action. "Configure a new data integration" is a scenario. If a scenario can be completed in one click, it's too granular.

---

#### Question 3: Shared Patterns (Context Q3/5 — conditional)

> **Only ask this if the agent detects repeated UI patterns across scenarios** (e.g., multiple list/detail pairs, repeated wizard flows, shared navigation). Skip if no patterns are evident.

**Agent asks:**

I notice some repeating patterns across your scenarios:

1. **List → Detail** — Several scenarios follow a "browse list, click item, see detail" pattern
2. **Multi-step Wizard** — Configuration and setup scenarios follow a step-by-step flow
3. **Other** — Describe a pattern I missed

Should I standardize these as reusable screen patterns? This reduces the total screen count and keeps the UI consistent.

**Agent validates:** A shared pattern is worth extracting only if it genuinely reduces the screen count. Don't force patterns where they don't fit.

---

#### Question 4: Constraints (Context Q4/5 — optional)

> **Only ask this if constraints were not already provided in Step 0.** Skip if the user already specified tech stack, design system, or scope boundaries.

**Agent asks:**

Before I generate the screen registry, any constraints I should know about?

1. **Tech constraints** — Component library (e.g., shadcn, MUI), framework (React, Next.js), mobile-first vs. desktop
2. **Design constraints** — Navigation pattern (sidebar, top nav, tabs), layout conventions, branding requirements
3. **Scope constraints** — Anything explicitly out of scope for this iteration
4. **Other** — Tell me something else

Pick any that apply, or skip if nothing comes to mind.

---

#### Question 5: Generate Screen Registry and Scenario Flows (Context Q5/5)

> **This is not a question.** The agent generates the registry and flows from the gathered context, then presents them for validation.

**Agent generates:**

Based on your roles, scenarios, patterns, and constraints, here's the proposed screen registry and scenario flows:

**Screen Registry:**

| ID | Screen Name | Status | Scenarios |
|----|------------|--------|-----------|
| S-01 | Login | [ ] | SC-1, SC-2, SC-3, SC-4 |
| S-02 | Tenant Dashboard | [ ] | SC-1, SC-2, SC-3 |
| S-03 | New Integration Wizard — Step 1 | [ ] | SC-1 |
| S-04 | New Integration Wizard — Step 2 | [ ] | SC-1 |
| ... | ... | [ ] | ... |

**Scenario Flows:**

- **SC-1: Configure New Integration** — S-01 → S-02 → S-03 → S-04 → S-05 → S-06 → S-02
- **SC-2: Monitor Sync Status** — S-01 → S-02 → S-07 → S-08
- **SC-3: Troubleshoot Failed Sync** — S-01 → S-02 → S-07 → S-09
- **SC-4: Admin — Manage All Tenants** — S-01 → S-10 → S-02 → S-07

**Agent offers 4 options:**

1. **Approve** — Looks good, let's start the screen-by-screen walkthrough
2. **Adjust** — I need to add, remove, or rename screens/scenarios
3. **Discuss** — Let's talk through the structure before committing
4. **Other** — Tell me what you need

---

### Phase 2: Screen-by-Screen Walkthrough

Walk through screens in **scenario priority order** (SC-1 first, then SC-2, etc.). When a screen has already been spec'd in a previous scenario, skip it — the spec is already done.

#### For Each Screen

**Agent generates:**

**S-02: Tenant Dashboard** (Screen 2/10)

**ASCII Wireframe:**

```
┌──────────────────────────────────────────────────┐
│  Logo        [Search...]  [Notifications] [User ▾]│
├──────────────────────────────────────────────────┤
│ ┌──────┐  ┌──────────────────────────────────┐   │
│ │ Nav  │  │  Welcome, {user.name}            │   │
│ │      │  │                                  │   │
│ │ Dash │  │  ┌─────────┐ ┌─────────┐        │   │
│ │ Intg │  │  │ Active  │ │ Failed  │        │   │
│ │ Logs │  │  │  12     │ │   2     │        │   │
│ │ Help │  │  └─────────┘ └─────────┘        │   │
│ │      │  │                                  │   │
│ └──────┘  │  Integration List                │   │
│           │  ┌──────┬────────┬───────┬─────┐ │   │
│           │  │ Name │ Status │ Last  │ Act │ │   │
│           │  ├──────┼────────┼───────┼─────┤ │   │
│           │  │ ...  │ ...    │ ...   │ ... │ │   │
│           │  └──────┴────────┴───────┴─────┘ │   │
│           │  [+ New Integration]             │   │
│           └──────────────────────────────────┘   │
└──────────────────────────────────────────────────┘
```

**Elements:**

| Element | Type | Data Needed |
|---------|------|-------------|
| Welcome message | Text | `user.name` |
| Active integrations count | Stat card | `integrations.active.count` |
| Failed integrations count | Stat card | `integrations.failed.count` |
| Integration list | Table | `integrations[]` (name, status, lastSync) |
| New Integration button | Action | — |
| Navigation sidebar | Nav | Current route |

**States:**

| State | Behavior |
|-------|----------|
| **Loading** | Skeleton cards + table rows |
| **Empty** | "No integrations yet. Create your first integration." + [+ New Integration] button |
| **Populated** | Stat cards + integration table (shown above) |
| **Error** | "Unable to load integrations. Please try again." + [Retry] button |

**Transitions:**

| Action | Target |
|--------|--------|
| Click integration row | → S-07 (Integration Detail) |
| Click [+ New Integration] | → S-03 (Wizard Step 1) |
| Click [Notifications] | → S-08 (Notification Panel) |
| Click nav item | → corresponding screen |

---

#### After Each Screen

**Agent offers 4 options:**

1. **Approve** — Move to next screen
2. **Adjust** — Tell me what to change, I'll regenerate
3. **Discuss** — Let's talk through this screen before deciding
4. **Skip** — Come back to this screen later

Option 3 (Discuss) opens a freeform conversation about the screen. The agent stays on the current screen until the user approves or skips. No time limit — take as long as you need to think through edge cases, alternative layouts, or missing elements.

---

#### Progress Tracking

After each approval or skip, the agent shows progress:

```
Screen Registry: 3/12 spec'd [███░░░░░░░░░] 25%  Next: S-04 (Field Mapping Review)
```

This keeps the session oriented. You always know how many screens remain and which one is next.

---

#### Handling Skipped Screens

After completing all priority screens (those that appear in SC-1 first, then SC-2, etc.), the agent returns to skipped screens:

"We've completed all priority screens. You skipped 2 screens earlier:
- S-05 (Connection Settings)
- S-09 (Error Resolution)

Want to spec these now, or leave them for a later session?"

---

### Phase 3: Review and Export

After all screens are spec'd (or intentionally skipped), the agent presents the complete artifact.

**Agent presents:**

Here's your complete user flow specification:
- **Screen Registry:** N screens (M spec'd, K skipped)
- **Scenario Flows:** X scenarios
- **Screen Specs:** Full detail for each spec'd screen

**Agent offers next steps:**

1. **Export as file** — Save the complete spec to your project (e.g., `docs/user-flow-spec.md`)
2. **Refine a screen** — Go back and update a specific screen spec
3. **Add a scenario** — Define a new scenario and any new screens it requires
4. **Suggest related skills** — Get recommendations for what to do next with this spec

## Examples

### Example: Data Integration Portal (2 roles, 4 scenarios)

**Context provided by user:**

> "Self-service portal for onboarding data integrations. External customers configure file or API connections. Internal admins manage all tenants."

---

**Roles identified (Q1):**

1. **External Customer** — Configures and monitors their own integrations. No access to other tenants.
2. **Vim Admin** — Manages all tenant integrations, resolves escalations, overrides configurations.

---

**Scenarios prioritized (Q2):**

| Priority | ID | Role | Scenario |
|----------|----|------|----------|
| 1 | SC-1 | External Customer | Configure a new file-based integration |
| 2 | SC-2 | External Customer | Monitor sync status and troubleshoot errors |
| 3 | SC-3 | Vim Admin | Review and manage all tenant integrations |
| 4 | SC-4 | Vim Admin | Override a failed integration configuration |

---

**Screen Registry (Q5 output):**

| ID | Screen Name | Status | Scenarios |
|----|------------|--------|-----------|
| S-01 | Login | [x] | SC-1, SC-2, SC-3, SC-4 |
| S-02 | Tenant Dashboard | [x] | SC-1, SC-2 |
| S-03 | New Integration Wizard — Source Type | [x] | SC-1 |
| S-04 | New Integration Wizard — Field Mapping | [x] | SC-1 |
| S-05 | New Integration Wizard — Schedule & Review | [x] | SC-1 |
| S-06 | Integration Confirmation | [x] | SC-1 |
| S-07 | Integration Detail | [x] | SC-2, SC-4 |
| S-08 | Sync Log Viewer | [x] | SC-2 |
| S-09 | Admin Dashboard | [x] | SC-3, SC-4 |
| S-10 | Admin — Tenant Detail | [x] | SC-3, SC-4 |

---

**Scenario Flow (SC-1: Configure New File-Based Integration):**

```
SC-1: S-01 → S-02 → S-03 → S-04 → S-05 → S-06 → S-02
       Login   Dash   Source  Map    Review  Done   Dash
```

---

**Sample Screen Spec — S-02: Tenant Dashboard:**

**ASCII Wireframe:**

```
┌──────────────────────────────────────────────────┐
│  Logo        [Search...]  [Notifications] [User ▾]│
├──────────────────────────────────────────────────┤
│ ┌──────┐  ┌──────────────────────────────────┐   │
│ │ Nav  │  │  Welcome, {user.name}            │   │
│ │      │  │                                  │   │
│ │ Dash │  │  ┌─────────┐ ┌─────────┐        │   │
│ │ Intg │  │  │ Active  │ │ Failed  │        │   │
│ │ Logs │  │  │  12     │ │   2     │        │   │
│ │ Help │  │  └─────────┘ └─────────┘        │   │
│ │      │  │                                  │   │
│ └──────┘  │  Integration List                │   │
│           │  ┌──────┬────────┬───────┬─────┐ │   │
│           │  │ Name │ Status │ Last  │ Act │ │   │
│           │  ├──────┼────────┼───────┼─────┤ │   │
│           │  │ ...  │ ...    │ ...   │ ... │ │   │
│           │  └──────┴────────┴───────┴─────┘ │   │
│           │  [+ New Integration]             │   │
│           └──────────────────────────────────┘   │
└──────────────────────────────────────────────────┘
```

**Elements:**

| Element | Type | Data Needed |
|---------|------|-------------|
| Welcome message | Text | `user.name` |
| Active integrations count | Stat card | `integrations.active.count` |
| Failed integrations count | Stat card | `integrations.failed.count` |
| Integration list | Table | `integrations[]` (name, status, lastSync) |
| New Integration button | Action | — |
| Navigation sidebar | Nav | Current route |

**States:**

| State | Behavior |
|-------|----------|
| **Loading** | Skeleton cards + shimmer table rows |
| **Empty** | "No integrations yet. Create your first integration." with prominent [+ New Integration] button |
| **Populated** | Stat cards + sortable integration table |
| **Error** | "Unable to load integrations. Please try again." + [Retry] button |

**Transitions:**

| Action | Target |
|--------|--------|
| Click integration row | → S-07 (Integration Detail) |
| Click [+ New Integration] | → S-03 (Wizard — Source Type) |
| Click [Notifications] | → Notification panel (overlay) |
| Click nav item | → Corresponding screen |

---

### Example Conversation Flow (Discuss Mode)

This shows what happens when a user picks option 3 (Discuss) for a screen:

> **Agent:** Here's S-03: New Integration Wizard — Source Type.
>
> ```
> ┌──────────────────────────────────────┐
> │  ← Back to Dashboard                │
> ├──────────────────────────────────────┤
> │  New Integration                     │
> │                                      │
> │  Step 1 of 3: Select Source Type     │
> │  ─────────────────────────────       │
> │                                      │
> │  ┌──────────────┐ ┌──────────────┐  │
> │  │  📁 File     │ │  🔌 API      │  │
> │  │  Upload      │ │  Connection  │  │
> │  │  CSV, XLSX   │ │  REST, SFTP  │  │
> │  └──────────────┘ └──────────────┘  │
> │                                      │
> │  [Cancel]              [Next →]      │
> └──────────────────────────────────────┘
> ```
>
> **Options:** 1. Approve  2. Adjust  3. Discuss  4. Skip
>
> **User:** 3
>
> **Agent:** Sure, let's discuss S-03. What's on your mind?
>
> **User:** I'm not sure about the stepper. We have 3 steps now, but we might add more later. Should this be an accordion instead?
>
> **Agent:** Good question. Here's the tradeoff:
>
> - **Stepper** (current): Clear linear progression. Users see exactly where they are (step 1 of 3). Works well when steps must be completed in order and the step count is stable. Most wizard patterns use steppers.
> - **Accordion**: Users can see all sections at once and jump between them. Better when sections can be filled in any order or when users need to reference earlier sections while filling later ones.
>
> For an integration wizard, I'd recommend **stepper**. The steps are sequential (you can't map fields before selecting a source type), and the linear flow reduces cognitive load. If you add a 4th step later, the stepper pattern handles it fine — "Step 1 of 4" is just as clear.
>
> **User:** Makes sense. Let's keep the stepper. Approve it.
>
> **Agent:** Approved. Moving to S-04.
>
> ```
> Screen Registry: 4/10 spec'd [████░░░░░░] 40%  Next: S-04 (Field Mapping)
> ```

## Common Pitfalls

### 1. **Designing Flows, Not Screens**

**Failure Mode:** Describing the same screen differently in each scenario. "In the onboarding flow, the dashboard has a welcome banner. In the monitoring flow, the dashboard has a metrics table." Now you have two conflicting specs for one screen.

**Consequence:** Coding agents build duplicate components or pick one spec and ignore the other. Either way, the implementation diverges from the design.

**Fix:** One screen = one entry in the registry = one spec. The dashboard screen (S-02) has one spec that covers all its states and all entry points. Flows reference screen IDs — they don't redefine screen content.

---

### 2. **Wireframes Too Detailed or Too Vague**

**Failure Mode (too detailed):** Specifying pixel dimensions, font sizes, exact colors, or component library props in the wireframe. The wireframe becomes a design spec that over-constrains the coding agent.

**Failure Mode (too vague):** "There's a form" with no indication of field count, layout, or hierarchy. The wireframe communicates nothing the agent couldn't guess.

**Consequence:** Too detailed = brittle implementation that breaks on screen resize. Too vague = agent guesses wrong and you redo the screen.

**Fix:** Show spatial arrangement — where elements sit relative to each other, what's prominent vs. secondary. Let the component library handle sizing, spacing, and typography.

---

### 3. **Missing States**

**Failure Mode:** Only specifying the Populated state (the happy path with data). No Loading skeleton, no Empty state, no Error handling.

**Consequence:** Coding agents ship screens that show blank white pages during loading, no guidance when data is empty, and unhandled exceptions when APIs fail. Users see broken-looking UIs.

**Fix:** For every screen, ask: "What does this look like with zero data? While data loads? When the API fails?" Default to including all four states (Loading, Empty, Populated, Error) and skip only when a state genuinely doesn't apply.

---

### 4. **Scenarios That Are Too Granular**

**Failure Mode:** Creating a scenario for every click. "SC-1: Click login button. SC-2: Enter credentials. SC-3: Click submit." These are actions, not scenarios.

**Consequence:** Dozens of "scenarios" that each describe one interaction. The scenario list becomes useless as a navigation map — it's just a click-by-click screenplay.

**Fix:** Scenarios represent **user goals**, not individual actions. "Configure a new integration" is a scenario. "Click the save button" is a step within a scenario. If a scenario can be completed in one or two clicks, it's probably a step inside a larger scenario.

---

### 5. **Skipping the Discussion Step**

**Failure Mode:** Approving every screen without thinking. The agent generates a wireframe, user says "1" (Approve), repeat 15 times. The result looks complete but hasn't been interrogated.

**Consequence:** Edge cases, missing states, and awkward navigation surface during implementation — when they're expensive to fix.

**Fix:** Use option 3 (Discuss) for any screen where you're uncertain about layout, navigation, or states. The discussion is free — the implementation rework is not. Even a 30-second "does this stepper vs. accordion choice make sense?" saves hours of refactoring later.

## References

### Related Skills

- **[problem-statement](skills/problem-statement/SKILL.md)** (Component) — Minimal required input; frame the problem before designing screens
- **[proto-persona](skills/proto-persona/SKILL.md)** (Component) — Enriches role definitions with behavioral and demographic detail
- **[user-story-mapping](skills/user-story-mapping/SKILL.md)** (Component) — Activity backbone accelerates screen identification
- **[storyboard](skills/storyboard/SKILL.md)** (Component) — 6-frame narratives seed the scenario flows
- **[lean-ux-canvas](skills/lean-ux-canvas/SKILL.md)** (Interactive) — Use before this skill if still validating whether to build
- **[prd-development](skills/prd-development/SKILL.md)** (Workflow) — Embed the flow spec as the PRD solution section
- **[epic-breakdown-advisor](skills/epic-breakdown-advisor/SKILL.md)** (Interactive) — Turn the screen registry into implementation epics

### External Frameworks

- **Jeff Patton** — *User Story Mapping: Discover the Whole Story, Build the Right Product* (O'Reilly, 2014)
- **Ryan Singer** — *Shape Up: Stop Running in Circles and Ship Work that Matters* (Basecamp, 2019) — breadboarding technique
- **Steve Krug** — *Don't Make Me Think: A Common Sense Approach to Web Usability* (New Riders, 2000)
