# epic-hypothesis.md

## Purpose
Frame epics as testable hypotheses using an if/then structure that articulates the action or solution, the target beneficiary, the expected outcome, and how you'll validate success. Use this to manage uncertainty in product development by making assumptions explicit, defining lightweight experiments ("tiny acts of discovery"), and establishing measurable success criteria before committing to full build-out.

This is not a requirements spec—it's a hypothesis you're testing, not a feature you're committed to shipping.

## Key Concepts

### The Epic Hypothesis Framework
Inspired by Tim Herbig's Lean UX hypothesis format, the structure is:

**If/Then Hypothesis:**
- **If we** [action or solution on behalf of target persona]
- **for** [target persona]
- **Then we will** [attain or achieve a desirable outcome or job-to-be-done]

**Tiny Acts of Discovery Experiments:**
- **We will test our assumption by:**
  - [Experiment 1]
  - [Experiment 2]
  - [Add more as necessary]

**Validation Measures:**
- **We know our hypothesis is valid if within** [timeframe]
- **we observe:**
  - [Quantitative measurable outcome]
  - [Qualitative measurable outcome]
  - [Add more as necessary]

### Why This Structure Works
- **Hypothesis-driven:** Forces you to state what you believe (and could be wrong about)
- **Outcome-focused:** "Then we will" emphasizes user benefit, not feature output
- **Experiment-first:** Encourages lightweight validation before full build
- **Falsifiable:** Clear success criteria make it possible to kill bad ideas early
- **Risk management:** Treats epics as bets, not commitments

### Anti-Patterns (What This Is NOT)
- **Not a feature spec:** "Build a dashboard with 5 charts" is a feature, not a hypothesis
- **Not a guaranteed commitment:** Hypotheses can (and should) be invalidated
- **Not output-focused:** "Ship feature X by Q2" misses the point—did it achieve the outcome?
- **Not experiment-free:** If you skip experiments and go straight to build, you're not testing a hypothesis

### When to Use This
- Early-stage feature exploration (before committing to full roadmap)
- Validating product-market fit for new capabilities
- Prioritizing backlog (epics with validated hypotheses get higher priority)
- Managing stakeholder expectations (frame work as experiments, not promises)

### When NOT to Use This
- For well-validated features (if you've already proven demand, skip straight to user stories)
- For trivial features (don't over-engineer small tweaks)
- When experiments aren't feasible (rare, but sometimes you must commit before testing)

---

## Application

### Step 1: Gather Context
Before drafting an epic hypothesis, ensure you have:
- **Problem understanding:** What user problem does this address? (reference `problem-statement.md`)
- **Target persona:** Who benefits? (reference `proto-persona.md`)
- **Jobs-to-be-Done:** What outcome are they trying to achieve? (reference `jobs-to-be-done.md`)
- **Current alternatives:** What do users do today? (competitors, workarounds, doing nothing)

**If missing context:** Run discovery interviews or problem validation work first.

---

### Step 2: Draft the If/Then Hypothesis

Fill in the template:

```markdown
### If/Then Hypothesis

**If we** [action or solution on behalf of the target persona]
**for** [target persona]
**Then we will** [attain or achieve a desirable outcome or job-to-be-done for the persona]
```

**Quality checks:**
- **"If we" is specific:** Not "improve the product" but "add one-click Slack notifications when tasks are assigned"
- **"For" is a clear persona:** Not "users" but "remote project managers juggling 3+ distributed teams" (reference `proto-persona.md`)
- **"Then we will" is an outcome:** Not "users will have notifications" but "users will respond to task assignments 50% faster"

**Examples:**
- ✅ "If we add one-click Google Calendar integration for trial users, then we will increase activation rates by 20% within 30 days"
- ✅ "If we provide bulk delete functionality for power users managing 1000+ items, then we will reduce time spent on cleanup tasks by 70%"
- ❌ "If we build a dashboard, then users will use it" (vague, not measurable)

---

### Step 3: Design Tiny Acts of Discovery Experiments

Before building the full epic, define lightweight experiments to test the hypothesis:

```markdown
### Tiny Acts of Discovery Experiments

**We will test our assumption by:**
- [Experiment 1: low-cost, fast test]
- [Experiment 2: another low-cost, fast test]
- [Add more as necessary]
```

**Experiment types:**
- **Prototype + user testing:** Fake the feature with a clickable prototype, test with 5-10 users
- **Concierge test:** Manually perform the feature for a few users, see if they value it
- **Landing page test:** Describe the feature, measure sign-ups or interest
- **Wizard of Oz test:** Present the feature as if it's automated, but do it manually behind the scenes
- **A/B test (if feasible):** Test a lightweight version vs. control

**Quality checks:**
- **Fast:** Experiments should take days/weeks, not months
- **Cheap:** Avoid full engineering builds—use prototypes, manual processes, or existing tools
- **Falsifiable:** Design experiments that could prove you *wrong*

**Examples:**
- "Create a Figma prototype of the bulk delete flow and test with 5 power users"
- "Manually send Slack notifications to 10 trial users and track response time"
- "Add a 'Request this feature' button to the UI and measure click-through rate"

---

### Step 4: Define Validation Measures

Specify what success looks like and the timeframe for evaluation:

```markdown
### Validation Measures

**We know our hypothesis is valid if within** [timeframe in days or weeks]
**we observe:**
- [Desirable quantitative, measurable outcome]
- [Desirable qualitative, measurable outcome]
- [Add more as necessary]
```

**Quality checks:**
- **Timeframe is realistic:** Not "within 6 months" (too slow) or "within 3 days" (too fast)
- **Quantitative measures are specific:** Not "more users" but "20% increase in activation rate"
- **Qualitative measures are observable:** Not "users like it" but "8 out of 10 users say they'd pay for this feature"

**Examples:**
- ✅ "Within 4 weeks, we observe:"
  - "Activation rate increases from 40% to 50% (quantitative)"
  - "75% of surveyed trial users say the integration saved them time (qualitative)"
- ❌ "Within 1 year, we observe:"
  - "Revenue goes up" (too vague, too long)

---

### Step 5: Run Experiments and Evaluate

- **Execute experiments:** Build prototypes, run tests, gather data
- **Measure results:** Did you hit the validation measures?
- **Decision point:**
  - ✅ **Hypothesis validated:** Proceed to building user stories and adding to roadmap
  - ❌ **Hypothesis invalidated:** Kill the epic or pivot to a different hypothesis
  - ⚠️ **Inconclusive:** Run additional experiments or tighten validation measures

---

### Step 6: Convert to User Stories (If Validated)

Once the hypothesis is validated, break the epic into user stories:

```markdown
### Epic: [Epic Name]

**Stories:**
1. [User Story 1 - reference `user-story.md`]
2. [User Story 2]
3. [User Story 3]
```

---

## Examples

### Example 1: Good Epic Hypothesis

```markdown
### Epic Hypothesis: Google Calendar Integration for Trial Users

#### If/Then Hypothesis

**If we** provide one-click Google Calendar integration during onboarding
**for** trial users who manage multiple meetings and tasks daily
**Then we will** increase activation rate (defined as completing setup + creating first task) from 40% to 50%

#### Tiny Acts of Discovery Experiments

**We will test our assumption by:**
1. Creating a clickable Figma prototype of the integration flow and testing with 10 trial users
2. Adding a "Connect Google Calendar" CTA to the onboarding flow (but it's non-functional) and measuring click-through rate
3. Manually syncing Google Calendar for 5 trial users and surveying them after 1 week on perceived value

#### Validation Measures

**We know our hypothesis is valid if within 4 weeks we observe:**
- Click-through rate on the CTA is > 60% (quantitative)
- 8 out of 10 prototype testers say they'd use this feature regularly (qualitative)
- Manually synced users report saving 10+ minutes per day on task entry (qualitative)
```

**Why this works:**
- Hypothesis is specific and measurable ("40% to 50% activation")
- Experiments are lightweight (prototype, CTA test, manual sync)
- Validation measures are clear and falsifiable
- Persona is specific ("trial users managing multiple meetings")

---

### Example 2: Bad Epic Hypothesis (Vague)

```markdown
### Epic Hypothesis: Improve Dashboard

#### If/Then Hypothesis

**If we** improve the dashboard
**for** users
**Then we will** make the product better

#### Tiny Acts of Discovery Experiments

**We will test our assumption by:**
1. Building the dashboard

#### Validation Measures

**We know our hypothesis is valid if we observe:**
- Users like it
```

**Why this fails:**
- "Improve the dashboard" is not specific (improve how?)
- "Users" is not a persona (which users? all users?)
- "Make the product better" is not measurable
- Experiment is "build it" (not a lightweight test)
- Validation is subjective ("users like it" = not falsifiable)

**How to fix it:**
- Specify the hypothesis: "If we add real-time task status updates to the dashboard for project managers, then we will reduce time spent checking task progress from 20 min/day to 5 min/day"
- Define persona: "for project managers managing 10+ team members"
- Design experiments: "Prototype the dashboard, test with 5 PMs, measure time savings"
- Specify validation: "8 out of 10 PMs report saving 10+ min/day"

---

### Example 3: Invalidated Hypothesis (Good Process)

```markdown
### Epic Hypothesis: Slack Integration for Notifications

#### If/Then Hypothesis

**If we** send Slack notifications when tasks are assigned
**for** remote project managers
**Then we will** reduce task response time from 4 hours to 1 hour

#### Tiny Acts of Discovery Experiments

**We will test our assumption by:**
1. Manually send Slack notifications to 10 project managers for 2 weeks
2. Measure response time before/after
3. Survey users on perceived value

#### Validation Measures

**We know our hypothesis is valid if within 2 weeks we observe:**
- Average response time drops from 4 hours to 1 hour (quantitative)
- 8 out of 10 users say Slack notifications helped them respond faster (qualitative)

---

**Results after 2 weeks:**
- Average response time: 3.5 hours (minimal improvement)
- User feedback: "I already get too many Slack notifications. I ignore most of them."
- **Decision: Hypothesis INVALIDATED. Users don't want more Slack noise. Pivot to in-app notifications or email digests.**
```

**Why this is good:**
- Hypothesis was tested (not just built)
- Experiments were lightweight (manual Slack messages, not full integration)
- Results showed the hypothesis was wrong
- Team killed the epic before wasting engineering time

---

## Common Pitfalls

### Pitfall 1: Hypothesis is a Feature, Not an Outcome
**Symptom:** "If we build a dashboard, then we will have a dashboard"

**Consequence:** You're describing output, not outcome. This doesn't test anything.

**Fix:** Focus on the user outcome: "If we build a dashboard showing real-time task status, then PMs will spend 50% less time asking for status updates."

---

### Pitfall 2: Skipping Experiments
**Symptom:** "We'll test our assumption by building the full feature"

**Consequence:** You've committed to building before validating. Not a hypothesis—it's a feature commitment.

**Fix:** Design lightweight experiments (prototypes, concierge tests, landing pages) that take days/weeks, not months.

---

### Pitfall 3: Vague Validation Measures
**Symptom:** "We know it's valid if users are happy"

**Consequence:** Success criteria are subjective and unmeasurable.

**Fix:** Define specific, falsifiable metrics: "80% of surveyed users rate the feature 4+ out of 5" or "Response time drops by 50%."

---

### Pitfall 4: Unrealistic Timeframes
**Symptom:** "We know it's valid if within 6 months revenue increases"

**Consequence:** Too slow to inform decisions. By then, you've already built it.

**Fix:** Aim for 2-4 week validation cycles. If you can't measure in that timeframe, choose a leading indicator (e.g., activation rate, not annual revenue).

---

### Pitfall 5: Treating Epics as Commitments
**Symptom:** "We already told the CEO we're shipping this, so we have to validate it"

**Consequence:** Experiments are theater—you're going to build it regardless of results.

**Fix:** Frame epics as hypotheses *before* making commitments. If stakeholders need certainty, explain the risk of building unvalidated features.

---

## References

### Related Skills
- `problem-statement.md` — Hypothesis should address a validated problem
- `proto-persona.md` — Defines the "for [persona]" section
- `jobs-to-be-done.md` — Informs the "then we will" outcome
- `user-story.md` — Validated epics decompose into user stories
- `user-story-splitting.md` — How to break validated epics into stories

### External Frameworks
- Tim Herbig, *Lean UX Hypothesis Statement* — Origin of if/then hypothesis format
- Jeff Gothelf & Josh Seiden, *Lean UX* (2013) — Hypothesis-driven product development
- Alberto Savoia, *Pretotype It* (2011) — Lightweight experiments to validate ideas
- Eric Ries, *The Lean Startup* (2011) — Build-Measure-Learn cycle

### Dean's Work
- Backlog Epic Hypothesis Prompt (inspired by Tim Herbig's framework)

---

**Skill type:** Component
**Suggested filename:** `epic-hypothesis.md`
**Suggested placement:** `/skills/components/`
**Dependencies:** References `problem-statement.md`, `proto-persona.md`, `jobs-to-be-done.md`
**Used by:** `user-story.md`, `user-story-splitting.md`
