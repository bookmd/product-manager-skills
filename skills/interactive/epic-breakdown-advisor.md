# epic-breakdown-advisor.md

## Purpose
Guide product managers through breaking down epics into user stories by systematically applying Richard Lawrence's 8 splitting patterns **in sequence**. Use this to identify which pattern applies to your epic, split it accordingly, and validate that each story delivers user value while maintaining independence. This ensures you're not guessing at how to split—you're following a proven, methodical approach.

This is not a story-writing automation—it's a systematic discovery process that walks you through the splitting decision tree until you find the right pattern.

## Key Concepts

### Richard Lawrence's Sequential Splitting Approach
The key insight: **Apply splitting patterns in order like a checklist.** Don't jump to a pattern—work through them sequentially until you find one that fits.

**The 8 Patterns (in order):**
1. **Workflow steps** — Sequential steps in user journey
2. **Business rule variations** — Different scenarios/rules (permissions, discounts, etc.)
3. **Data variations** — Different data types or inputs
4. **Acceptance criteria complexity** — Multiple "When" or "Then" statements
5. **Major effort** — Large technical work that can be phased
6. **External dependencies** — Third-party APIs, other teams, approvals
7. **DevOps steps** — Infrastructure or deployment phases
8. **Tiny Acts of Discovery (TADs)** — Experiments to unpack unknowns (when none of the above apply)

### Why This Systematic Approach Works
- **Prevents arbitrary splitting:** You're not guessing—you're following a checklist
- **Preserves user value:** Each pattern ensures stories deliver independently
- **Catches edge cases:** Working sequentially means you don't miss applicable patterns
- **Repeatable:** Can be applied to any epic, consistently

### Anti-Patterns (What This Is NOT)
- **Not "pick your favorite pattern":** Follow the sequence
- **Not task decomposition:** Stories aren't tasks
- **Not horizontal slicing:** Each story includes front-end + back-end work

### When to Use This
- Epic is too large for a single sprint
- Multiple "When/Then" statements in acceptance criteria
- Stakeholders can't agree on epic scope
- You're unsure how to split an epic

### When NOT to Use This
- Story is already small and well-scoped
- Epic is a technical task (use engineering breakdown)
- Splitting would create blocking dependencies

---

## Application

This interactive skill **walks through the 8 splitting patterns sequentially**, asking yes/no questions for each pattern until you find one that applies.

---

### Step 0: Provide Epic Context

**Agent asks:**

Before we begin the splitting process, please share your epic:

**Epic Information:**
- Epic title or ID
- Epic description or hypothesis (if using `epic-hypothesis.md` format)
- Acceptance criteria (especially important if multiple "When/Then" statements)
- Target persona (reference `proto-persona.md`)
- Rough estimate (person-weeks or story points)

**You can paste:**
- Epic from Jira, Linear, or backlog tool
- Epic hypothesis ("If we / for / Then we will")
- User story with complex acceptance criteria
- Feature description or PRD section

**Or describe the epic briefly.**

---

### Pattern 1: Workflow Steps

**Agent asks:**
"Does your epic contain multiple sequential steps in a user's workflow or journey?"

**Examples of workflow step patterns:**
- Sign up → verify email → complete onboarding → activate
- Search → filter results → select item → add to cart → checkout
- Create account → import data → configure settings → invite team

**Offer 3 options:**

1. **Yes, it has sequential workflow steps** — "I can identify 2+ steps users complete in order"
2. **No, it's a single step** — "Users do one thing, not a sequence"
3. **Not sure** — "Let me describe the epic and you tell me"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by workflow steps. List the sequential steps, and we'll create one story per step."
→ Skip to Output (generate stories split by workflow)

**If NO or NOT SURE:**
→ Continue to Pattern 2

---

### Pattern 2: Business Rule Variations

**Agent asks:**
"Does your epic have different rules for different scenarios (e.g., permissions, discount tiers, user types)?"

**Examples of business rule patterns:**
- Different discount rules (member 10%, VIP 20%, first-time 5%)
- Permission levels (admin, editor, viewer)
- Calculation variations (tax by region, pricing by tier)

**Offer 3 options:**

1. **Yes, different rules for different scenarios** — "The logic changes based on user type, region, or context"
2. **No, same rules for everyone** — "Everyone gets the same treatment"
3. **Not sure** — "Let me describe it"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by business rules. We'll create one story per rule variation."
→ Skip to Output (generate stories split by business rules)

**If NO or NOT SURE:**
→ Continue to Pattern 3

---

### Pattern 3: Data Variations

**Agent asks:**
"Does your epic handle different types of data or inputs (e.g., file types, data formats, input methods)?"

**Examples of data variation patterns:**
- Upload different file types (images, PDFs, videos)
- Import from different sources (CSV, Google Sheets, API)
- Handle different input methods (keyboard, voice, touch)

**Offer 3 options:**

1. **Yes, different data types or inputs** — "The epic handles multiple formats or sources"
2. **No, single data type** — "Only one format or input method"
3. **Not sure** — "Let me describe it"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by data type. We'll create one story per data variation."
→ Skip to Output (generate stories split by data type)

**If NO or NOT SURE:**
→ Continue to Pattern 4

---

### Pattern 4: Acceptance Criteria Complexity

**Agent asks:**
"Does your epic have multiple 'When' or 'Then' statements in the acceptance criteria?"

**Examples:**
- When I add item → Then it appears
- When I remove item → Then it disappears
- When I update quantity → Then total updates

**If your epic has 2+ "When/Then" pairs, that's a sign it should be split.**

**Offer 3 options:**

1. **Yes, multiple When/Then pairs** — "I count 2 or more distinct When/Then statements"
2. **No, single When/Then** — "Just one action and one outcome"
3. **Not sure / no acceptance criteria yet** — "Let me share what I have"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by acceptance criteria. Each When/Then pair becomes a story."
→ Skip to Output (generate stories, one per When/Then pair)

**If NO or NOT SURE:**
→ Continue to Pattern 5

---

### Pattern 5: Major Effort

**Agent asks:**
"Is your epic large (e.g., 3+ weeks of work) but can be delivered incrementally in phases?"

**Examples:**
- Build real-time collaboration (Phase 1: presence indicators, Phase 2: live cursors, Phase 3: real-time edits)
- Add advanced search (Phase 1: basic keyword search, Phase 2: filters, Phase 3: fuzzy matching)

**Offer 3 options:**

1. **Yes, large effort with phases** — "It's 3+ weeks but can be delivered in increments"
2. **No, it's small** — "1-2 weeks of work, no need to phase"
3. **Not sure** — "Let me describe the scope"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by effort phases. We'll deliver a basic version first, then enhancements."
→ Skip to Output (generate stories by MVP → Phase 2 → Phase 3)

**If NO or NOT SURE:**
→ Continue to Pattern 6

---

### Pattern 6: External Dependencies

**Agent asks:**
"Does your epic depend on external systems (third-party APIs, other teams, legal approval)?"

**Examples:**
- Integration with Stripe API (can build without API first, add integration later)
- Requires legal approval (build core feature, add compliance layer after approval)
- Depends on Platform Team's authentication service

**Offer 3 options:**

1. **Yes, external dependencies** — "It requires third-party APIs, other teams, or approvals"
2. **No, self-contained** — "We can build this entirely within our team"
3. **Not sure** — "Let me describe dependencies"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by dependencies. Story 1 works without dependencies, Story 2 adds integration."
→ Skip to Output (generate stories: standalone version → add dependencies)

**If NO or NOT SURE:**
→ Continue to Pattern 7

---

### Pattern 7: DevOps Steps

**Agent asks:**
"Does your epic require significant infrastructure, deployment, or DevOps work that can be separated?"

**Examples:**
- Set up Kubernetes cluster (Story 1) → Deploy app to cluster (Story 2)
- Implement caching layer (Story 1) → Migrate to cached version (Story 2)

**Offer 3 options:**

1. **Yes, significant DevOps steps** — "Infrastructure or deployment work can be split out"
2. **No, minimal DevOps** — "Standard deployment, no special infrastructure"
3. **Not sure** — "Let me describe technical requirements"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by DevOps steps. We'll separate infrastructure from feature work."
→ Skip to Output (generate stories by DevOps phases)

**If NO or NOT SURE:**
→ Continue to Pattern 8

---

### Pattern 8: Tiny Acts of Discovery (TADs)

**Agent says:**
"None of the standard splitting patterns seem to apply. This suggests the epic has **high uncertainty or unknowns**."

**Richard Lawrence's recommendation:** Use **Tiny Acts of Discovery (TADs)** to reduce uncertainty before committing to a full build.

**TADs are small experiments (not stories) that answer questions:**
- Prototype with 5 users → Learn if the approach works
- Spike: Research technical feasibility → Learn if it's possible with current stack
- A/B test a landing page → Validate demand before building

**Agent asks:**
"What are the biggest unknowns or assumptions in this epic?"

**Offer 3 options:**

1. **Uncertain if users want this** — "Haven't validated demand"
2. **Uncertain if it's technically feasible** — "Don't know if we can build it with current stack"
3. **Uncertain about the right approach** — "Multiple ways to solve it, unclear which is best"

**User response:** [Selection or description]

**Agent recommends TADs:**
→ Agent says: "Let's design 2-3 small experiments (TADs) to reduce uncertainty. Once we learn from TADs, we can write stories with confidence."
→ Skip to Output (generate TAD experiments, not stories yet)

---

### Output: Generate Story Breakdown (Based on Pattern)

After identifying which pattern applies, the agent generates story outlines:

```markdown
# Epic Breakdown Plan

**Epic:** [Original epic title/description]
**Splitting Pattern Applied:** [Pattern name from above]
**Rationale:** [Why this pattern fits]

---

## Story Breakdown

### Story 1: [Story Title]

**Summary:** [Brief, user-value-focused title]

**Use Case:**
- **As a** [persona]
- **I want to** [specific action]
- **so that** [desired outcome]

**Acceptance Criteria:**
- **Scenario:** [Brief description]
- **Given:** [Preconditions]
- **When:** [Action]
- **Then:** [Outcome]

**User Value:** [Why this story matters independently]
**Estimated Effort:** [Rough days/story points]

---

### Story 2: [Story Title]

[Repeat for each story...]

---

## Validation Checklist (INVEST Criteria)

✅ **Independent:** Can stories be developed in any order?
✅ **Negotiable:** Can stories be refined during sprint planning?
✅ **Valuable:** Does each story deliver user value?
✅ **Estimable:** Can engineering estimate effort?
✅ **Small:** Can each story fit in a sprint (1-5 days)?
✅ **Testable:** Can QA write test cases from acceptance criteria?

---

## Next Steps

1. **Review stories with team:** Do PM, design, engineering agree on this split?
2. **Check for further splitting:** Are any stories still too large? If yes, repeat this process (start at Pattern 1 again).
3. **Prioritize:** Which story delivers the most value first?
4. **Add to backlog:** Ready to groom and pull into sprint.

---

**If stories are still too large, we can apply the splitting patterns again to individual stories.**
```

---

## Examples

### Example 1: Pattern 1 Applied (Workflow Steps)

**Epic:** "User onboarding flow — New users sign up, verify email, complete profile, create first project"

**Agent walks through patterns:**
- **Pattern 1 (Workflow):** "Does this have sequential steps?" → **YES** ✅

**Generated Breakdown:**

### Story 1: Sign Up with Email/Password
- **As a** new user, **I want to** sign up with email/password, **so that** I can create an account
- **Effort:** 2 days

### Story 2: Verify Email
- **As a** new user, **I want to** verify my email via confirmation link, **so that** I can prove I own the email
- **Effort:** 1 day

### Story 3: Complete Profile
- **As a** verified user, **I want to** answer 3 onboarding questions, **so that** the app personalizes my experience
- **Effort:** 2 days

### Story 4: Create First Project
- **As an** onboarded user, **I want to** create my first project, **so that** I can start using the app
- **Effort:** 3 days

---

### Example 2: Multiple Patterns Applied (Workflow + Business Rules)

**Epic:** "Checkout flow with discounts — Users add items, apply discounts (member, VIP, first-time), and complete payment"

**Agent walks through patterns:**
- **Pattern 1 (Workflow):** "Does this have sequential steps?" → **YES** ✅

**First Split (by workflow):**
1. Add items to cart
2. Apply discount
3. Complete payment

**Agent checks Story 2 ("Apply discount"):**
- Still too large (3 days)
- Restart pattern sequence for Story 2:
  - **Pattern 2 (Business Rules):** "Different discount rules?" → **YES** ✅

**Second Split (Story 2 by business rules):**
1. Apply member discount (10%)
2. Apply VIP discount (20%)
3. Apply first-time buyer discount (5%)

**Final Breakdown:**
1. Add items to cart
2. Apply member discount
3. Apply VIP discount
4. Apply first-time buyer discount
5. Complete payment

---

## Common Pitfalls

### Pitfall 1: Skipping Patterns (Jumping to Gut Feel)
**Symptom:** "I think we should split by X" without checking patterns 1-7 first

**Consequence:** Miss a better splitting approach

**Fix:** Follow the sequence. Don't skip patterns.

---

### Pitfall 2: Stopping After One Split When Stories Are Still Large
**Symptom:** Split epic into 3 stories, but each story is still 5+ days

**Consequence:** Stories are still too large for sprint

**Fix:** Re-apply the pattern sequence to each large story until all stories are 1-5 days.

---

### Pitfall 3: Forcing a Pattern That Doesn't Fit
**Symptom:** "We'll split by workflow even though there's no sequence"

**Consequence:** Arbitrary, meaningless split

**Fix:** If a pattern doesn't apply, say "NO" and move to the next pattern.

---

### Pitfall 4: Giving Up at Pattern 8 (TADs)
**Symptom:** "None of the patterns fit, so we can't split"

**Consequence:** Build a large epic with high uncertainty

**Fix:** Pattern 8 (TADs) is for high-uncertainty epics. Run experiments before writing stories.

---

## References

### Related Skills
- `user-story-splitting.md` — The 8 patterns in detail
- `user-story.md` — Format for writing split stories
- `epic-hypothesis.md` — Original epic format

### External Frameworks
- Richard Lawrence & Peter Green, *Humanizing Work Guide to Splitting User Stories* — The flowchart/checklist approach
- Bill Wake, *INVEST in Good Stories* (2003) — Story quality criteria

### Dean's Work
- User Story Splitting Prompt Template

---

**Skill type:** Interactive
**Suggested filename:** `epic-breakdown-advisor.md`
**Suggested placement:** `/skills/interactive/`
**Dependencies:** Uses `user-story-splitting.md`, `user-story.md`, `epic-hypothesis.md`

## Purpose
Guide product managers through breaking down epics into user stories by asking adaptive questions about epic scope, complexity, personas, and delivery constraints. Use this to avoid epics that are too large to ship, stories that lack user value, or arbitrary slicing that creates dependencies. Outputs a recommended breakdown approach with splitting patterns, story outlines, and validation criteria.

This is not a story-writing automation—it's a strategic breakdown process that ensures each story delivers user value while maintaining technical feasibility.

## Key Concepts

### The Epic Breakdown Flow
An interactive process that:
1. Analyzes the epic (reads hypothesis, acceptance criteria, or description)
2. Identifies complexity drivers (workflow steps, business rules, data variations, effort)
3. Recommends splitting pattern (from `user-story-splitting.md`)
4. Generates story outlines with user value preserved
5. Validates that splits are independent, testable, and deliverable

### Why This Works
- **Value-preserving:** Each story delivers user value (not "front-end" + "back-end" splits)
- **Pattern-based:** Uses proven splitting patterns (workflow, business rules, data, etc.)
- **Context-aware:** Adapts to epic type (feature, infrastructure, experiment)
- **Validation-focused:** Ensures stories pass INVEST criteria

### Anti-Patterns (What This Is NOT)
- **Not task decomposition:** Stories aren't tasks ("Set up database," "Write API")
- **Not arbitrary slicing:** Don't split "Add user management" into "Add user" + "Management"
- **Not horizontal slicing:** Each story should include front-end + back-end work

### When to Use This
- Epic is too large for a single sprint (>5 days of work)
- Multiple "When/Then" statements in acceptance criteria (sign of bundled stories)
- Stakeholders can't agree on epic scope (need to split for phased delivery)
- Epic has complex acceptance criteria or dependencies

### When NOT to Use This
- Story is already small and well-scoped (don't over-split)
- Epic is a technical task (use engineering task breakdown instead)
- Splitting would create hard dependencies that block delivery

---

## Application

This interactive skill asks **up to 4 adaptive questions**, offering **3-4 enumerated options** at each step.

---

### Step 0: Provide Epic Context

**Agent asks:**

Before we break down your epic, please share:

**Epic Information:**
- Epic title or ID (if available)
- Epic hypothesis (if using `epic-hypothesis.md` format)
- Acceptance criteria or description
- Target persona (reference `proto-persona.md` if available)
- Estimated effort (rough person-weeks or story points)

**You can paste:**
- Epic from Jira, Linear, or backlog tool
- Epic hypothesis with "If we / for / Then we will" format
- Feature description or PRD section
- User story with complex acceptance criteria (multiple When/Then statements)

**Or describe the epic briefly.**

---

### Question 1: Epic Complexity Type

**Agent asks:**
"What makes this epic complex? (What's driving the size?)"

**Offer 4 enumerated options:**

1. **Multiple workflow steps** — E.g., "Sign up → verify email → complete onboarding → activate" (sequential steps that could be split)
2. **Business rule variations** — E.g., "Different discount rules for members, VIPs, first-time buyers" (different scenarios/rules)
3. **Data or input variations** — E.g., "Upload images, PDFs, videos" (different data types)
4. **Major effort or complexity** — E.g., "Requires 6 weeks of engineering; can be delivered incrementally" (phased delivery possible)

**Or describe what makes this epic large/complex.**

**Adaptation tip:** If user provided acceptance criteria with multiple "When/Then" statements, suggest "Multiple workflow steps" or "Business rule variations."

**User response:** [Selection or custom]

---

### Question 2: Personas Involved

**Agent asks:**
"Does this epic serve multiple user personas or roles?"

**Offer 3 enumerated options:**

1. **Single persona** — E.g., "Only serves small business owners" (can split by workflow/rules/data, not persona)
2. **Multiple personas** — E.g., "Serves both admins and end-users" (can split by persona first, then by workflow)
3. **Not sure / no clear persona** — "Epic is feature-focused, not persona-focused" (need to reframe as user story first)

**Or describe the personas involved.**

**Adaptation tip:** If user provided epic with "As a [persona]," extract persona from there.

**User response:** [Selection or custom]

---

### Question 3: Delivery Constraints

**Agent asks:**
"What are your delivery constraints for this epic?"

**Offer 3 enumerated options:**

1. **Must ship all at once** — E.g., "Can't deliver partial functionality; confuses users" (need to validate if this is true, or find ways to phase)
2. **Can ship incrementally** — E.g., "Okay to ship basic version first, add advanced features later" (phased delivery = split by value tiers)
3. **External dependencies** — E.g., "Depends on third-party API, legal approval, or other team's work" (split by dependency boundaries)

**Or describe your constraints (timeline, dependencies, team capacity).**

**User response:** [Selection or custom]

---

### Question 4: Splitting Pattern Recommendation

**Agent asks:**
"Based on your epic ([complexity from Q1], [personas from Q2], [constraints from Q3]), here are recommended splitting patterns:"

**Offer 3-4 enumerated options (context-aware based on Q1-Q3):**

**Example (if Q1 = Multiple workflow steps, Q2 = Single persona, Q3 = Can ship incrementally):**

1. **Split by workflow steps** — Break epic into sequential stories (e.g., Story 1: "Sign up with email/password," Story 2: "Verify email via link," Story 3: "Complete onboarding profile"). Each story delivers user value independently. (Best for: Multi-step workflows that users complete sequentially)

2. **Split by MVP vs. enhancements** — Deliver bare-minimum version first, add polish later (e.g., Story 1: "Upload images (basic validation)," Story 2: "Add image cropping/filters"). (Best for: When you can ship "good enough" first, iterate based on feedback)

3. **Split by user journey phase** — Break by where users are in their journey (e.g., Story 1: "Onboarding: First-time user setup," Story 2: "Activation: Create first project," Story 3: "Retention: Return user flow"). (Best for: Epics that span multiple journey stages)

4. **Split by acceptance criteria** — Each "When/Then" pair becomes a story (e.g., Story 1: "When user adds item to cart, Then it appears," Story 2: "When user removes item, Then it disappears"). (Best for: Epics with multiple When/Then statements)

**Choose a number, or describe your own splitting approach.**

**Adaptation examples:**
- If Q1 = Business rule variations → Prioritize "Split by business rules" (e.g., Story 1: "Member discount," Story 2: "VIP discount")
- If Q1 = Data variations → Prioritize "Split by data type" (e.g., Story 1: "Upload images," Story 2: "Upload PDFs")
- If Q2 = Multiple personas → Prioritize "Split by persona" first (e.g., Story 1: "Admin permissions," Story 2: "End-user permissions")
- If Q3 = External dependencies → Prioritize "Split by dependency" (e.g., Story 1: "Works without API," Story 2: "Add API integration")

**User response:** [Selection or custom]

---

### Output: Generate Story Breakdown

After collecting responses, the agent generates story outlines:

```markdown
# Epic Breakdown Plan

**Epic:** [Original epic title/description]
**Complexity:** [From Q1]
**Personas:** [From Q2]
**Constraints:** [From Q3]
**Splitting Pattern:** [From Q4]

---

## Recommended Story Breakdown

### Story 1: [Story Title]

**Summary:** [Brief, user-value-focused title]

**Use Case:**
- **As a** [persona from Q2]
- **I want to** [specific action]
- **so that** [desired outcome]

**Acceptance Criteria:**
- **Scenario:** [Brief description]
- **Given:** [Preconditions]
- **When:** [Action]
- **Then:** [Outcome]

**User Value:** [Why this story matters independently]
**Estimated Effort:** [Rough days/story points]

---

### Story 2: [Story Title]

**Summary:** [Brief, user-value-focused title]

**Use Case:**
- **As a** [persona]
- **I want to** [action]
- **so that** [outcome]

**Acceptance Criteria:**
- **Scenario:** [Description]
- **Given:** [Preconditions]
- **When:** [Action]
- **Then:** [Outcome]

**User Value:** [Why this matters]
**Estimated Effort:** [Rough estimate]

---

### Story 3: [Story Title]

[Repeat for each story...]

---

## Validation Checklist (INVEST Criteria)

Review each story against INVEST:

✅ **Independent:** Can stories be developed in any order without blocking each other?
- [ ] Story 1 doesn't block Story 2
- [ ] Story 2 doesn't block Story 3
- [ ] If dependencies exist, document them

✅ **Negotiable:** Can stories be refined during sprint planning?
- [ ] Stories aren't overly detailed (leave room for design/eng input)
- [ ] Focus on "what" and "why," not "how"

✅ **Valuable:** Does each story deliver user value?
- [ ] Each story has clear "so that" outcome
- [ ] No "front-end story" + "back-end story" splits
- [ ] User can see/use the feature after each story

✅ **Estimable:** Can engineering estimate effort?
- [ ] Stories are clear enough to size
- [ ] If not, flag for refinement session

✅ **Small:** Can each story fit in a sprint?
- [ ] Stories are 1-5 days of work
- [ ] If larger, consider further splitting

✅ **Testable:** Can QA write test cases?
- [ ] Acceptance criteria are clear and measurable
- [ ] "Then" statements are verifiable

---

## Delivery Sequence (Recommended Order)

1. **[Story 1]** — Delivers core value, validates demand
2. **[Story 2]** — Builds on Story 1, adds next-most-important feature
3. **[Story 3]** — Enhancement or polish (can defer if needed)

**Rationale:** [Explain why this order maximizes early value delivery and learning]

---

## Alternative Splitting Approach

**If the recommended split doesn't work, consider:** [Alternative pattern]

**Why this might work:**
- [Rationale]

**Tradeoffs:**
- [What you gain vs. lose]

---

**Ready to add these stories to your backlog? Let me know if you'd like to refine any story.**
```

---

## Examples

### Example 1: Good Epic Breakdown (Workflow Steps)

**Step 0 - Epic Context:**
```
Epic: User Onboarding Flow
Description: New users should sign up, verify email, complete profile, and create their first project.
Estimated effort: 3 weeks
```

**Q1 Response:** "Multiple workflow steps — Sign up → verify email → complete profile → create first project"

**Q2 Response:** "Single persona — New trial users"

**Q3 Response:** "Can ship incrementally — Okay to deliver basic signup first, add profile/project creation later"

**Q4 Response:** "Split by workflow steps — Each step becomes a story"

---

**Generated Breakdown:**

### Story 1: Sign Up with Email/Password

**Summary:** New user creates account with email and password

**Use Case:**
- **As a** new trial user
- **I want to** sign up with email and password
- **so that** I can access the app

**Acceptance Criteria:**
- **Given:** I am on the signup page
- **When:** I enter valid email/password and click "Sign Up"
- **Then:** My account is created and I receive a "Check your email" message

**User Value:** Users can create accounts and start exploring the app (even without email verification)
**Estimated Effort:** 2 days

---

### Story 2: Verify Email

**Summary:** User verifies email address via confirmation link

**Use Case:**
- **As a** new user
- **I want to** verify my email via a confirmation link
- **so that** I can prove I own the email address

**Acceptance Criteria:**
- **Given:** I have signed up and received a confirmation email
- **When:** I click the verification link in the email
- **Then:** My email is verified and I'm redirected to the app

**User Value:** Prevents fake accounts, enables password reset
**Estimated Effort:** 1 day

---

### Story 3: Complete Onboarding Profile

**Summary:** User answers 3 profile questions to personalize experience

**Use Case:**
- **As a** verified user
- **I want to** answer 3 onboarding questions (role, team size, use case)
- **so that** the app can personalize my experience

**Acceptance Criteria:**
- **Given:** I have verified my email
- **When:** I answer 3 onboarding questions and click "Continue"
- **Then:** My profile is saved and I proceed to dashboard

**User Value:** Personalized onboarding improves activation
**Estimated Effort:** 2 days

---

**Validation:** ✅ Independent, ✅ Valuable, ✅ Small, ✅ Testable

**Delivery Sequence:**
1. Story 1 (core signup)
2. Story 2 (email verification)
3. Story 3 (profile questions)

**Why this order:** Users can sign up immediately (Story 1). Email verification (Story 2) reduces fake accounts. Profile questions (Story 3) improve activation but aren't blocking.

---

## Common Pitfalls

### Pitfall 1: Horizontal Slicing (Technical Layers)
**Symptom:** "Story 1: Build API. Story 2: Build UI."

**Consequence:** Neither story delivers user value independently.

**Fix:** Split vertically—each story includes front-end + back-end work to deliver a user-facing feature.

---

### Pitfall 2: Arbitrary Slicing
**Symptom:** "Story 1: First half of feature. Story 2: Second half."

**Consequence:** No clear rationale for split; creates confusion.

**Fix:** Use a splitting pattern (workflow, business rules, data, etc.).

---

### Pitfall 3: Creating Hard Dependencies
**Symptom:** "Story 2 can't start until Story 1 is 100% done, tested, and deployed."

**Consequence:** No parallelization, slows delivery.

**Fix:** Split so stories are independent. If dependencies are unavoidable, prioritize Story 1.

---

### Pitfall 4: Stories Without User Value
**Symptom:** "Story: Set up database schema"

**Consequence:** Engineering task, not user story.

**Fix:** Reframe as user value: "Story: User can save preferences (includes database setup)."

---

### Pitfall 5: Over-Splitting
**Symptom:** "Story 1: Add button. Story 2: Wire button. Story 3: Display result."

**Consequence:** Unnecessary overhead, too many dependencies.

**Fix:** Only split when story is too large. A 2-day story doesn't need splitting.

---

## References

### Related Skills
- `user-story-splitting.md` — The 8 splitting patterns this advisor uses
- `user-story.md` — Format for writing the split stories
- `epic-hypothesis.md` — Original epic format with hypothesis structure

### External Frameworks
- Richard Lawrence & Peter Green, *Humanizing Work Story Splitting Guide* — 8 splitting patterns
- Bill Wake, *INVEST in Good Stories* (2003) — Story quality criteria

### Dean's Work
- User Story Splitting Prompt Template

---

**Skill type:** Interactive
**Suggested filename:** `epic-breakdown-advisor.md

## Purpose
Guide product managers through breaking down epics into user stories by systematically applying Richard Lawrence's 8 splitting patterns **in sequence**. Use this to identify which pattern applies to your epic, split it accordingly, and validate that each story delivers user value while maintaining independence. This ensures you're not guessing at how to split—you're following a proven, methodical approach.

This is not a story-writing automation—it's a systematic discovery process that walks you through the splitting decision tree until you find the right pattern.

## Key Concepts

### Richard Lawrence's Sequential Splitting Approach
The key insight: **Apply splitting patterns in order like a checklist.** Don't jump to a pattern—work through them sequentially until you find one that fits.

**The 8 Patterns (in order):**
1. **Workflow steps** — Sequential steps in user journey
2. **Business rule variations** — Different scenarios/rules (permissions, discounts, etc.)
3. **Data variations** — Different data types or inputs
4. **Acceptance criteria complexity** — Multiple "When" or "Then" statements
5. **Major effort** — Large technical work that can be phased
6. **External dependencies** — Third-party APIs, other teams, approvals
7. **DevOps steps** — Infrastructure or deployment phases
8. **Tiny Acts of Discovery (TADs)** — Experiments to unpack unknowns (when none of the above apply)

### Why This Systematic Approach Works
- **Prevents arbitrary splitting:** You're not guessing—you're following a checklist
- **Preserves user value:** Each pattern ensures stories deliver independently
- **Catches edge cases:** Working sequentially means you don't miss applicable patterns
- **Repeatable:** Can be applied to any epic, consistently

### Anti-Patterns (What This Is NOT)
- **Not "pick your favorite pattern":** Follow the sequence
- **Not task decomposition:** Stories aren't tasks
- **Not horizontal slicing:** Each story includes front-end + back-end work

### When to Use This
- Epic is too large for a single sprint
- Multiple "When/Then" statements in acceptance criteria
- Stakeholders can't agree on epic scope
- You're unsure how to split an epic

### When NOT to Use This
- Story is already small and well-scoped
- Epic is a technical task (use engineering breakdown)
- Splitting would create blocking dependencies

---

## Application

This interactive skill **walks through the 8 splitting patterns sequentially**, asking yes/no questions for each pattern until you find one that applies.

---

### Step 0: Provide Epic Context

**Agent asks:**

Before we begin the splitting process, please share your epic:

**Epic Information:**
- Epic title or ID
- Epic description or hypothesis (if using `epic-hypothesis.md` format)
- Acceptance criteria (especially important if multiple "When/Then" statements)
- Target persona (reference `proto-persona.md`)
- Rough estimate (person-weeks or story points)

**You can paste:**
- Epic from Jira, Linear, or backlog tool
- Epic hypothesis ("If we / for / Then we will")
- User story with complex acceptance criteria
- Feature description or PRD section

**Or describe the epic briefly.**

---

### Pattern 1: Workflow Steps

**Agent asks:**
"Does your epic contain multiple sequential steps in a user's workflow or journey?"

**Examples of workflow step patterns:**
- Sign up → verify email → complete onboarding → activate
- Search → filter results → select item → add to cart → checkout
- Create account → import data → configure settings → invite team

**Offer 3 options:**

1. **Yes, it has sequential workflow steps** — "I can identify 2+ steps users complete in order"
2. **No, it's a single step** — "Users do one thing, not a sequence"
3. **Not sure** — "Let me describe the epic and you tell me"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by workflow steps. List the sequential steps, and we'll create one story per step."
→ Skip to Output (generate stories split by workflow)

**If NO or NOT SURE:**
→ Continue to Pattern 2

---

### Pattern 2: Business Rule Variations

**Agent asks:**
"Does your epic have different rules for different scenarios (e.g., permissions, discount tiers, user types)?"

**Examples of business rule patterns:**
- Different discount rules (member 10%, VIP 20%, first-time 5%)
- Permission levels (admin, editor, viewer)
- Calculation variations (tax by region, pricing by tier)

**Offer 3 options:**

1. **Yes, different rules for different scenarios** — "The logic changes based on user type, region, or context"
2. **No, same rules for everyone** — "Everyone gets the same treatment"
3. **Not sure** — "Let me describe it"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by business rules. We'll create one story per rule variation."
→ Skip to Output (generate stories split by business rules)

**If NO or NOT SURE:**
→ Continue to Pattern 3

---

### Pattern 3: Data Variations

**Agent asks:**
"Does your epic handle different types of data or inputs (e.g., file types, data formats, input methods)?"

**Examples of data variation patterns:**
- Upload different file types (images, PDFs, videos)
- Import from different sources (CSV, Google Sheets, API)
- Handle different input methods (keyboard, voice, touch)

**Offer 3 options:**

1. **Yes, different data types or inputs** — "The epic handles multiple formats or sources"
2. **No, single data type** — "Only one format or input method"
3. **Not sure** — "Let me describe it"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by data type. We'll create one story per data variation."
→ Skip to Output (generate stories split by data type)

**If NO or NOT SURE:**
→ Continue to Pattern 4

---

### Pattern 4: Acceptance Criteria Complexity

**Agent asks:**
"Does your epic have multiple 'When' or 'Then' statements in the acceptance criteria?"

**Examples:**
- When I add item → Then it appears
- When I remove item → Then it disappears
- When I update quantity → Then total updates

**If your epic has 2+ "When/Then" pairs, that's a sign it should be split.**

**Offer 3 options:**

1. **Yes, multiple When/Then pairs** — "I count 2 or more distinct When/Then statements"
2. **No, single When/Then** — "Just one action and one outcome"
3. **Not sure / no acceptance criteria yet** — "Let me share what I have"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by acceptance criteria. Each When/Then pair becomes a story."
→ Skip to Output (generate stories, one per When/Then pair)

**If NO or NOT SURE:**
→ Continue to Pattern 5

---

### Pattern 5: Major Effort

**Agent asks:**
"Is your epic large (e.g., 3+ weeks of work) but can be delivered incrementally in phases?"

**Examples:**
- Build real-time collaboration (Phase 1: presence indicators, Phase 2: live cursors, Phase 3: real-time edits)
- Add advanced search (Phase 1: basic keyword search, Phase 2: filters, Phase 3: fuzzy matching)

**Offer 3 options:**

1. **Yes, large effort with phases** — "It's 3+ weeks but can be delivered in increments"
2. **No, it's small** — "1-2 weeks of work, no need to phase"
3. **Not sure** — "Let me describe the scope"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by effort phases. We'll deliver a basic version first, then enhancements."
→ Skip to Output (generate stories by MVP → Phase 2 → Phase 3)

**If NO or NOT SURE:**
→ Continue to Pattern 6

---

### Pattern 6: External Dependencies

**Agent asks:**
"Does your epic depend on external systems (third-party APIs, other teams, legal approval)?"

**Examples:**
- Integration with Stripe API (can build without API first, add integration later)
- Requires legal approval (build core feature, add compliance layer after approval)
- Depends on Platform Team's authentication service

**Offer 3 options:**

1. **Yes, external dependencies** — "It requires third-party APIs, other teams, or approvals"
2. **No, self-contained** — "We can build this entirely within our team"
3. **Not sure** — "Let me describe dependencies"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by dependencies. Story 1 works without dependencies, Story 2 adds integration."
→ Skip to Output (generate stories: standalone version → add dependencies)

**If NO or NOT SURE:**
→ Continue to Pattern 7

---

### Pattern 7: DevOps Steps

**Agent asks:**
"Does your epic require significant infrastructure, deployment, or DevOps work that can be separated?"

**Examples:**
- Set up Kubernetes cluster (Story 1) → Deploy app to cluster (Story 2)
- Implement caching layer (Story 1) → Migrate to cached version (Story 2)

**Offer 3 options:**

1. **Yes, significant DevOps steps** — "Infrastructure or deployment work can be split out"
2. **No, minimal DevOps** — "Standard deployment, no special infrastructure"
3. **Not sure** — "Let me describe technical requirements"

**User response:** [Selection or description]

**If YES:**
→ Agent says: "Great! Let's split by DevOps steps. We'll separate infrastructure from feature work."
→ Skip to Output (generate stories by DevOps phases)

**If NO or NOT SURE:**
→ Continue to Pattern 8

---

### Pattern 8: Tiny Acts of Discovery (TADs)

**Agent says:**
"None of the standard splitting patterns seem to apply. This suggests the epic has **high uncertainty or unknowns**."

**Richard Lawrence's recommendation:** Use **Tiny Acts of Discovery (TADs)** to reduce uncertainty before committing to a full build.

**TADs are small experiments (not stories) that answer questions:**
- Prototype with 5 users → Learn if the approach works
- Spike: Research technical feasibility → Learn if it's possible with current stack
- A/B test a landing page → Validate demand before building

**Agent asks:**
"What are the biggest unknowns or assumptions in this epic?"

**Offer 3 options:**

1. **Uncertain if users want this** — "Haven't validated demand"
2. **Uncertain if it's technically feasible** — "Don't know if we can build it with current stack"
3. **Uncertain about the right approach** — "Multiple ways to solve it, unclear which is best"

**User response:** [Selection or description]

**Agent recommends TADs:**
→ Agent says: "Let's design 2-3 small experiments (TADs) to reduce uncertainty. Once we learn from TADs, we can write stories with confidence."
→ Skip to Output (generate TAD experiments, not stories yet)

---

### Output: Generate Story Breakdown (Based on Pattern)

After identifying which pattern applies, the agent generates story outlines:

```markdown
# Epic Breakdown Plan

**Epic:** [Original epic title/description]
**Splitting Pattern Applied:** [Pattern name from above]
**Rationale:** [Why this pattern fits]

---

## Story Breakdown

### Story 1: [Story Title]

**Summary:** [Brief, user-value-focused title]

**Use Case:**
- **As a** [persona]
- **I want to** [specific action]
- **so that** [desired outcome]

**Acceptance Criteria:**
- **Scenario:** [Brief description]
- **Given:** [Preconditions]
- **When:** [Action]
- **Then:** [Outcome]

**User Value:** [Why this story matters independently]
**Estimated Effort:** [Rough days/story points]

---

### Story 2: [Story Title]

[Repeat for each story...]

---

## Validation Checklist (INVEST Criteria)

✅ **Independent:** Can stories be developed in any order?
✅ **Negotiable:** Can stories be refined during sprint planning?
✅ **Valuable:** Does each story deliver user value?
✅ **Estimable:** Can engineering estimate effort?
✅ **Small:** Can each story fit in a sprint (1-5 days)?
✅ **Testable:** Can QA write test cases from acceptance criteria?

---

## Next Steps

1. **Review stories with team:** Do PM, design, engineering agree on this split?
2. **Check for further splitting:** Are any stories still too large? If yes, repeat this process (start at Pattern 1 again).
3. **Prioritize:** Which story delivers the most value first?
4. **Add to backlog:** Ready to groom and pull into sprint.

---

**If stories are still too large, we can apply the splitting patterns again to individual stories.**
```

---

## Examples

### Example 1: Pattern 1 Applied (Workflow Steps)

**Epic:** "User onboarding flow — New users sign up, verify email, complete profile, create first project"

**Agent walks through patterns:**
- **Pattern 1 (Workflow):** "Does this have sequential steps?" → **YES** ✅

**Generated Breakdown:**

### Story 1: Sign Up with Email/Password
- **As a** new user, **I want to** sign up with email/password, **so that** I can create an account
- **Effort:** 2 days

### Story 2: Verify Email
- **As a** new user, **I want to** verify my email via confirmation link, **so that** I can prove I own the email
- **Effort:** 1 day

### Story 3: Complete Profile
- **As a** verified user, **I want to** answer 3 onboarding questions, **so that** the app personalizes my experience
- **Effort:** 2 days

### Story 4: Create First Project
- **As an** onboarded user, **I want to** create my first project, **so that** I can start using the app
- **Effort:** 3 days

---

### Example 2: Multiple Patterns Applied (Workflow + Business Rules)

**Epic:** "Checkout flow with discounts — Users add items, apply discounts (member, VIP, first-time), and complete payment"

**Agent walks through patterns:**
- **Pattern 1 (Workflow):** "Does this have sequential steps?" → **YES** ✅

**First Split (by workflow):**
1. Add items to cart
2. Apply discount
3. Complete payment

**Agent checks Story 2 ("Apply discount"):**
- Still too large (3 days)
- Restart pattern sequence for Story 2:
  - **Pattern 2 (Business Rules):** "Different discount rules?" → **YES** ✅

**Second Split (Story 2 by business rules):**
1. Apply member discount (10%)
2. Apply VIP discount (20%)
3. Apply first-time buyer discount (5%)

**Final Breakdown:**
1. Add items to cart
2. Apply member discount
3. Apply VIP discount
4. Apply first-time buyer discount
5. Complete payment

---

## Common Pitfalls

### Pitfall 1: Skipping Patterns (Jumping to Gut Feel)
**Symptom:** "I think we should split by X" without checking patterns 1-7 first

**Consequence:** Miss a better splitting approach

**Fix:** Follow the sequence. Don't skip patterns.

---

### Pitfall 2: Stopping After One Split When Stories Are Still Large
**Symptom:** Split epic into 3 stories, but each story is still 5+ days

**Consequence:** Stories are still too large for sprint

**Fix:** Re-apply the pattern sequence to each large story until all stories are 1-5 days.

---

### Pitfall 3: Forcing a Pattern That Doesn't Fit
**Symptom:** "We'll split by workflow even though there's no sequence"

**Consequence:** Arbitrary, meaningless split

**Fix:** If a pattern doesn't apply, say "NO" and move to the next pattern.

---

### Pitfall 4: Giving Up at Pattern 8 (TADs)
**Symptom:** "None of the patterns fit, so we can't split"

**Consequence:** Build a large epic with high uncertainty

**Fix:** Pattern 8 (TADs) is for high-uncertainty epics. Run experiments before writing stories.

---

## References

### Related Skills
- `user-story-splitting.md` — The 8 patterns in detail
- `user-story.md` — Format for writing split stories
- `epic-hypothesis.md` — Original epic format

### External Frameworks
- Richard Lawrence & Peter Green, *Humanizing Work Guide to Splitting User Stories* — The flowchart/checklist approach
- Bill Wake, *INVEST in Good Stories* (2003) — Story quality criteria

### Dean's Work
- User Story Splitting Prompt Template

---

**Skill type:** Interactive
**Suggested filename:** `epic-breakdown-advisor.md`
**Suggested placement:** `/skills/interactive/`
**Dependencies:** Uses `user-story-splitting.md`, `user-story.md`, `epic-hypothesis.md``
**Suggested placement:** `/skills/interactive/`
**Dependencies:** Uses `user-story-splitting.md`, `user-story.md`, `epic-hypothesis.md`
