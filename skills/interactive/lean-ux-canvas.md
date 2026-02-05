# lean-ux-canvas.md

## Purpose
Guide product managers through creating a Lean UX Canvas (Jeff Gothelf, v2) by asking adaptive questions to frame work as a business problem (not a solution to implement), dissect core assumptions, develop testable hypotheses, and design experiments that drive measurable learning. Use this to align cross-functional teams on business outcomes, user benefits, and the riskiest assumptions to test—avoiding feature-factory syndrome and ensuring teams build the right thing, not just build things right.

This is not a roadmap—it's a hypothesis-driven planning tool that turns assumptions into experiments before committing to full development.

## Key Concepts

### What is the Lean UX Canvas?

The Lean UX Canvas (Jeff Gothelf, v2) is a facilitation tool for cross-functional teams that structures customer-centric conversations about product initiatives. It dissects the business problem into its core assumptions, which you then test through experiments—learning fast and adjusting course before building the wrong thing.

### Canvas Structure (8 Sections)

**Layout (3 columns × 3 rows):**

```
┌─────────────────────┬──────────────┬───────────────────────┐
│ 1. Business Problem │  5. Solutions│ 2. Business Outcomes  │
│                     │   (tall box  │                       │
├─────────────────────┤   spanning   ├───────────────────────┤
│ 3. Users            │   full       │ 4. User Outcomes      │
│                     │   height)    │    & Benefits         │
├─────────────────────┼──────────────┼───────────────────────┤
│ 6. Hypotheses       │ 7. What's    │ 8. What's the least   │
│                     │    most      │    work to learn      │
│                     │    important │    next?              │
│                     │    to learn? │                       │
└─────────────────────┴──────────────┴───────────────────────┘
```

**8 Sections:**
1. **Business Problem** — What challenge is the organization facing?
2. **Business Outcomes** — What measurable organizational goals must be achieved?
3. **Users** — Who are the target customer segments?
4. **User Outcomes & Benefits** — What actions/behaviors indicate success for users?
5. **Solutions** — What ideas might address the problem? (Center tall box)
6. **Hypotheses** — What assumptions are we making? (If/then/because format)
7. **What's the most important thing we need to learn first?** — Riskiest assumption to test
8. **What's the least amount of work we need to do to learn the next most important thing?** — Minimal experiment design

### Why This Works
- **Problem-first, not solution-first:** Starts with business problem, not "we should build X"
- **Assumption-driven:** Makes hypotheses explicit before building
- **Experiment-focused:** Tests assumptions before committing resources
- **Cross-functional alignment:** Shared canvas creates common language

### Anti-Patterns (What This Is NOT)
- **Not a feature list:** Solutions (box 5) are hypotheses, not commitments
- **Not a project plan:** Canvas frames learning, not delivery timelines
- **Not a replacement for strategy:** Canvas executes strategy; it doesn't create it

### When to Use This
- Starting a new product initiative or feature
- Reframing an existing project (suspect you're building wrong thing)
- Aligning cross-functional teams on assumptions and experiments
- Planning discovery sprints or MVPs

### When NOT to Use This
- When problem and solution are already validated (move to execution)
- For tactical bug fixes or technical debt (no learning needed)
- When stakeholders have already committed to a solution (address alignment first)

---

## Application

This interactive skill asks **up to 8 adaptive questions** (one per canvas section), offering **3-4 enumerated options** at each step.

---

### Step 0: Gather Context (Before Questions)

**Agent suggests:**

Before we fill out the Lean UX Canvas, let's gather context:

**Business Context:**
- Stakeholder request, product brief, or initiative description
- Business metrics (revenue, churn, growth targets)
- Strategic goals (OKRs, roadmap priorities)

**User Context:**
- Customer research, personas, JTBD insights
- User feedback, support tickets, churn reasons
- Competitor analysis, market trends

**You can paste this content directly, or describe the initiative briefly.**

---

### Question 1: Business Problem

**Agent asks:**
"What business problem are you trying to solve? (What challenge is the organization facing?)"

**Offer 4 enumerated options:**

1. **Revenue problem** — "We're not generating enough revenue or growth is stagnating" (e.g., "ARR growth dropped to 5% YoY")
2. **Retention problem** — "Customers are churning or not engaging" (e.g., "Churn rate increased 15% last quarter")
3. **Acquisition problem** — "Not enough customers discovering/signing up" (e.g., "Trial conversion rate below industry average")
4. **Efficiency problem** — "Internal costs too high or operations inefficient" (e.g., "Support tickets increasing 30%/month")

**Or describe your specific business problem.**

**User response:** [Selection or custom]

**Agent captures:**
- **Business Problem:** [Description]

---

### Question 2: Business Outcomes

**Agent asks:**
"What measurable business outcomes will indicate success? (How will you know the problem is solved?)"

**Offer 4 enumerated options:**

1. **Revenue outcome** — "Increase ARR, ARPU, or revenue per customer" (e.g., "Increase ARR from $5M to $8M in 12 months")
2. **Retention outcome** — "Reduce churn, increase engagement/activation" (e.g., "Reduce churn from 15% to 8%")
3. **Acquisition outcome** — "Increase signups, trial conversions, or new customers" (e.g., "Increase trial-to-paid conversion from 10% to 20%")
4. **Efficiency outcome** — "Reduce costs, support burden, or operational overhead" (e.g., "Reduce support tickets by 40%")

**Or describe your specific business outcome (must be measurable).**

**User response:** [Selection or custom]

**Agent captures:**
- **Business Outcomes:** [Measurable goals]

---

### Question 3: Users (Customer Segments)

**Agent asks:**
"Who are the target users or customer segments for this initiative?"

**Offer 4 enumerated options:**

1. **Primary persona** — "Main target customer (e.g., 'small business owners')" (Most common)
2. **Multiple personas** — "Several user segments with different needs (e.g., 'buyers' vs. 'sellers')" (Common for marketplaces)
3. **High-value segment** — "Subset of users driving most revenue/engagement (e.g., 'enterprise accounts')" (Good for expansion)
4. **Underserved segment** — "Users with unmet needs or high churn (e.g., 'mobile-first users')" (Good for retention)

**Or describe your specific user segments.**

**Adaptation:** Use personas from context (proto-personas, JTBD, customer research)

**User response:** [Selection or custom]

**Agent captures:**
- **Users:** [Target segments]

---

### Question 4: User Outcomes & Benefits

**Agent asks:**
"What user outcomes or benefits will indicate success? (What actions/behaviors show users are getting value?)"

**Offer 4 enumerated options:**

1. **Activation outcome** — "Users complete onboarding, reach 'aha moment'" (e.g., "Users complete first project within 24 hours")
2. **Engagement outcome** — "Users return regularly, increase usage" (e.g., "Users log in 3x/week, up from 1x/week")
3. **Satisfaction outcome** — "Users report higher satisfaction/NPS" (e.g., "NPS increases from 30 to 50")
4. **Expansion outcome** — "Users invite teammates, upgrade plans, or expand usage" (e.g., "Users invite 3+ teammates")

**Or describe your specific user outcomes (observable behaviors, not assumptions).**

**User response:** [Selection or custom]

**Agent captures:**
- **User Outcomes & Benefits:** [Observable behaviors]

---

### Question 5: Solutions (Initial Ideas)

**Agent asks:**
"What solution ideas might address the business problem? (These are hypotheses, not commitments.)"

**Agent generates 3-5 solution ideas** based on business problem (Q1) and user outcomes (Q4).

**Example (if Business Problem = Retention, User Outcome = Activation):**

```
Solution Ideas:

1. Guided onboarding checklist — Interactive checklist walks users through core workflows step-by-step
2. In-app tooltips — Contextual help appears when users encounter new features
3. Email drip campaign — Automated emails nudge users to complete activation steps
4. Human-assisted onboarding — 15-min onboarding call with CSM for high-value users
5. Empty state prompts — When users see empty dashboard, suggest "Create your first project"
```

**Agent asks:**
"Which solution ideas should we prioritize for testing?"

**User response:** [Selection or custom]

**Agent captures:**
- **Solutions:** [List of ideas to test]

---

### Question 6: Hypotheses (Assumptions)

**Agent asks:**
"What assumptions are you making? Let's turn them into testable hypotheses."

**Agent generates 3-5 hypotheses** using **"If/Then/Because"** format:

**Template:** "If [we do X], then [user outcome Y will happen], because [assumption Z]."

**Example (for Solution 1: Guided onboarding checklist):**

```
Hypothesis 1:
If we add a guided onboarding checklist, then activation rate will increase from 40% to 60%, because users are dropping off due to lack of guidance (not lack of features).

Hypothesis 2:
If we show step-by-step prompts, then users will complete onboarding faster (reduce time-to-value from 3 days to 1 day), because current onboarding is overwhelming and unclear.

Hypothesis 3:
If we prioritize onboarding over new features, then churn will decrease by 10%, because most churn happens in the first 30 days due to poor activation.
```

**Agent asks:**
"Do these hypotheses capture your key assumptions? Should we add or refine any?"

**User response:** [Approve or modify]

**Agent captures:**
- **Hypotheses:** [If/then/because statements]

---

### Question 7: What's the Most Important Thing to Learn First?

**Agent asks:**
"Which assumption is the riskiest? (What's the most important thing to validate before building?)"

**Agent ranks hypotheses from Q6 by risk:**

**Risk factors:**
- **High uncertainty:** Do we have data/evidence, or is this a guess?
- **High impact:** If this assumption is wrong, does the entire solution fail?
- **High cost:** Would building based on this assumption waste significant resources?

**Example ranking:**

```
Ranked Hypotheses (highest risk first):

1. **Hypothesis 1 (RISKIEST):** "Users drop off due to lack of guidance, not lack of features"
   - High uncertainty: We don't have data confirming this root cause
   - High impact: If wrong, onboarding checklist won't move activation
   - HIGH RISK — Test this first

2. **Hypothesis 2 (MEDIUM RISK):** "Users will complete onboarding faster with step-by-step prompts"
   - Medium uncertainty: Some qualitative feedback supports this
   - Medium impact: Time-to-value matters, but not as critical as activation rate
   - MEDIUM RISK — Test after Hypothesis 1

3. **Hypothesis 3 (LOWER RISK):** "Most churn happens in first 30 days"
   - Low uncertainty: We have churn data confirming this
   - Low impact: Already validated; no need to test
   - LOW RISK — Assume true
```

**Agent asks:**
"Do you agree with this ranking? Which hypothesis should we test first?"

**User response:** [Selection or custom]

**Agent captures:**
- **Most Important to Learn First:** [Riskiest hypothesis]

---

### Question 8: What's the Least Work to Learn Next?

**Agent asks:**
"What's the smallest experiment we can run to test the riskiest hypothesis?"

**Agent generates 3 experiment options** (ordered by effort: low → high):

**Example (for Hypothesis 1: "Users drop off due to lack of guidance"):**

```
Experiment Options (least work → most work):

1. **Concierge test (manual)** — Manually walk 10 users through onboarding via Zoom, observe where they get stuck
   - Effort: 1 day (10 x 30-min sessions)
   - Learning: Qualitative validation of root cause
   - Risk: Small sample, not scalable

2. **Prototype test (clickable mockup)** — Create Figma prototype of onboarding checklist, watch 10 users attempt it
   - Effort: 3 days (design + testing)
   - Learning: Validates if checklist concept resonates
   - Risk: Not real product, users may behave differently

3. **A/B test (live product)** — Build minimal onboarding checklist, show to 50% of new users for 2 weeks
   - Effort: 2 weeks (build + monitor)
   - Learning: Quantitative validation of activation lift
   - Risk: Higher effort if hypothesis is wrong
```

**Agent asks:**
"Which experiment should we run first?"

**User response:** [Selection or custom]

**Agent captures:**
- **Least Work to Learn Next:** [Minimal experiment design]

---

### Output: Lean UX Canvas + Experiment Plan

After completing the flow, the agent outputs:

```markdown
# Lean UX Canvas: [Initiative Name]

**Date:** [Today's date]
**Iteration:** 1

---

## 1. Business Problem
[From Q1]

## 2. Business Outcomes
[From Q2 - measurable goals]

## 3. Users (Customer Segments)
[From Q3 - target personas/segments]

## 4. User Outcomes & Benefits
[From Q4 - observable behaviors]

## 5. Solutions (Hypotheses to Test)
- [Solution 1 from Q5]
- [Solution 2]
- [Solution 3]
- [Solution 4]

## 6. Hypotheses (If/Then/Because)

### Hypothesis 1:
If [action], then [outcome], because [assumption].

### Hypothesis 2:
If [action], then [outcome], because [assumption].

### Hypothesis 3:
If [action], then [outcome], because [assumption].

---

## 7. What's the Most Important Thing to Learn First?

**Riskiest Hypothesis:** [From Q7]

**Why this is riskiest:**
- High uncertainty: [Explanation]
- High impact: [Consequence if wrong]

---

## 8. What's the Least Amount of Work to Learn the Next Most Important Thing?

**Experiment:** [From Q8]

**Effort:** [Time estimate]
**Success criteria:** [What validates/invalidates hypothesis]
**Timeline:** [Duration]

---

## Next Steps

1. **Run experiment:** [Specific action, e.g., "Recruit 10 users for concierge onboarding test"]
2. **Measure results:** [Metric to track, e.g., "Activation rate: control vs. test group"]
3. **Decide:**
   - If hypothesis validated → Build solution, iterate canvas
   - If hypothesis invalidated → Pivot, test next hypothesis
4. **Update canvas:** Iterate after each experiment (mark as "Iteration 2," etc.)

---

**Ready to run the experiment? Let me know if you'd like to refine hypotheses or design the test.**
```

---

## Examples

### Example 1: Good Lean UX Canvas (SaaS Onboarding)

**Q1 Response:** "Retention problem — Churn rate increased 15% last quarter"

**Q2 Response:** "Reduce churn from 15% to 8% within 6 months"

**Q3 Response:** "Primary persona — Small business owners (non-technical)"

**Q4 Response:** "Activation outcome — Users complete first project within 24 hours"

**Q5 - Solutions Generated:**
1. Guided onboarding checklist
2. In-app tooltips
3. Email drip campaign
4. Human-assisted onboarding

**Q6 - Hypotheses Generated:**
- **H1:** If we add guided checklist, then activation increases to 60%, because users drop off due to lack of guidance
- **H2:** If we show step-by-step prompts, then time-to-value decreases to 1 day, because current onboarding is overwhelming

**Q7 - Riskiest Hypothesis:** H1 (lack of guidance vs. lack of features)

**Q8 - Minimal Experiment:** Concierge test—manually walk 10 users through onboarding, observe pain points

**Why this works:**
- Clear business problem → measurable outcome
- Riskiest assumption identified before building
- Minimal experiment (1 day) before committing to full build

---

### Example 2: Bad Lean UX Canvas (Solution-First)

**Q1 Response:** "We need a mobile app"

**Why this fails:**
- Solution disguised as business problem
- No measurable business outcome
- No hypotheses to test

**Fix with canvas:**
- **Q1:** "Acquisition problem — Trial conversion rate below industry average (10% vs. 20%)"
- **Q2:** "Increase trial-to-paid conversion from 10% to 20%"
- **Q3:** "Mobile-first users (freelancers, field workers)"
- **Q4:** "Users complete core workflow on mobile device"
- **Q5:** Solutions = Mobile app, responsive web, PWA, SMS notifications
- **Q6:** Hypothesis = "If we enable mobile access, then trial conversion increases, because mobile-first users currently can't complete workflows on the go"
- **Q7:** Riskiest = "Mobile-first users abandon trials because they can't access product on mobile" (need to validate root cause)
- **Q8:** Experiment = Survey 50 churned trial users—ask if mobile access was a blocker

**Now canvas reveals:** Mobile app is one solution, but might not be the riskiest assumption to test first.

---

## Common Pitfalls

### Pitfall 1: Business Problem Is Actually a Solution
**Symptom:** "Business problem: We need better reporting"

**Consequence:** Jumped to solution before understanding root problem

**Fix:** Ask "why?"—"What business outcome is blocked by lack of reporting?"

---

### Pitfall 2: Business Outcomes Aren't Measurable
**Symptom:** "Improve user experience" or "Increase customer satisfaction"

**Consequence:** Can't validate if initiative succeeded

**Fix:** Make outcomes specific: "Increase NPS from 30 to 50" or "Reduce churn from 15% to 8%"

---

### Pitfall 3: Hypotheses Aren't Testable
**Symptom:** "We believe users want dark mode"

**Consequence:** Can't design an experiment to validate

**Fix:** Use If/Then/Because format: "If we add dark mode, then engagement increases by 10%, because users abandon due to eye strain at night"

---

### Pitfall 4: Testing Too Many Hypotheses at Once
**Symptom:** Trying to validate 10 assumptions simultaneously

**Consequence:** Can't isolate what worked or didn't

**Fix:** Test one hypothesis at a time, starting with riskiest

---

### Pitfall 5: Experiment Is Too Big
**Symptom:** "Let's build the full feature and A/B test it"

**Consequence:** Waste resources if hypothesis is wrong

**Fix:** Start with smallest experiment (concierge, prototype, landing page test)

---

## References

### Related Skills
- `problem-statement.md` — Converts business problem into structured problem statement
- `epic-hypothesis.md` — Turns validated hypotheses into epics
- `opportunity-solution-tree.md` — Generates solution options and POC experiments
- `proto-persona.md` — Defines user segments for canvas

### External Frameworks
- Jeff Gothelf, *Lean UX Canvas v2* (2020) — Origin of canvas framework
- Jeff Gothelf & Josh Seiden, *Lean UX* (2016) — Hypothesis-driven product development
- Eric Ries, *The Lean Startup* (2011) — Build-measure-learn cycle

### Dean's Work
- [If Dean has Lean UX resources, link here]

---

**Skill type:** Interactive
**Suggested filename:** `lean-ux-canvas.md`
**Suggested placement:** `/skills/interactive/`
**Dependencies:** Uses `problem-statement.md`, `proto-persona.md`, `epic-hypothesis.md`
