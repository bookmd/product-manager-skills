# tam-sam-som-calculator.md

## Purpose
Guide product managers through calculating Total Addressable Market (TAM), Serviceable Available Market (SAM), and Serviceable Obtainable Market (SOM) for a product idea by asking adaptive, contextually relevant questions. Use this to build defensible market size estimates backed by real-world citations, economic projections, and population data—essential for pitching to investors, securing budget, or validating product-market fit.

This is not a back-of-napkin guess—it's a structured, citation-backed analysis that withstands scrutiny.

## Key Concepts

### TAM/SAM/SOM Framework
The three-tier market sizing model:

**Total Addressable Market (TAM):**
- The total market demand for a product or service
- "If we captured 100% of the market, what's the revenue?"
- Broadest possible market (no constraints)

**Serviceable Available Market (SAM):**
- The segment of TAM your company can realistically target
- Narrowed by geography, firmographics, demographics, or product constraints
- "Who can we actually reach with our product?"

**Serviceable Obtainable Market (SOM):**
- The portion of SAM you can realistically capture
- Accounts for competition, market constraints, go-to-market capacity
- "What can we capture in the next 1-3 years?"

### Why This Works
- **Top-down validation:** TAM → SAM → SOM ensures estimates are grounded in reality
- **Investor-friendly:** Standard framework VCs and execs understand
- **Citation-backed:** Real data sources (Census, Statista, World Bank) add credibility
- **Adaptive:** Questions adjust based on context (B2B vs. B2C, US vs. global, etc.)

### Anti-Patterns (What This Is NOT)
- **Not a single-number guess:** "The market is $10B" without supporting data
- **Not static:** Markets evolve—reassess annually
- **Not a substitute for customer validation:** Market size ≠ product-market fit

### When to Use This
- Pitching to investors or execs (need market size in deck)
- Validating product ideas (is the market big enough?)
- Prioritizing product lines (which has bigger opportunity?)
- Setting growth targets (what's realistic to capture?)

### When NOT to Use This
- For internal tools with captive users (no external market)
- Before defining the problem (market sizing requires clear problem space)
- As the only validation (pair with customer research)

---

## Application

This interactive skill asks **up to 4 adaptive questions**, offering **enumerated context-aware options** at each step. The agent adapts questions based on previous responses.

---

### Step 0: Gather Context (Before Questions)

**Agent suggests:**

Before we begin, it's helpful to have product context. If available, please share:

**For Your Own Product:**
- Website copy (homepage, product pages, value prop statements)
- Marketing emails or landing pages
- Product descriptions or positioning statements
- Case studies or customer testimonials
- Sales deck or pitch materials

**If You Don't Have a Product Yet:**
- Find a similar or adjacent product (competitor or analog)
- Copy their website homepage, product description, or landing page
- We'll use this as a reference point for market sizing

**You can paste this content directly, or we can proceed with a brief description.**

**Why this helps:**
- Marketing materials already contain target audience, pain points, and value props
- Analyzing real content (yours or competitors') grounds the analysis in reality
- You can benchmark against similar products' market positioning

---

### Question 1: Problem Space

**Agent asks:**
"Based on the context you've provided (or will describe), what problem space are you exploring for market sizing?"

**Offer 4 enumerated examples (user can select by number or write custom):**

1. **B2B SaaS productivity** — E.g., "Workflow automation for small business operations" (like Zapier, Integromat)
2. **Consumer fintech** — E.g., "Personal budgeting app for Gen Z users" (like Mint, YNAB)
3. **Healthcare/telehealth** — E.g., "Mental health support for remote workers" (like BetterHelp, Talkspace)
4. **E-commerce enablement** — E.g., "Payment processing for online sellers" (like Stripe, Square)

**Or write your own problem space description based on the marketing materials you shared.**

**Tip:** If you provided website copy or marketing materials, the agent can extract the problem space from phrases like:
- "We help [target] solve [problem]"
- "The #1 solution for [use case]"
- Customer pain points in testimonials or case studies

**User response:** [Selection or custom description]

---

### Question 2: Geographic Region

**Agent asks:**
"What geographic region are you targeting?"

**Offer 4 enumerated options (adapted based on problem space):**

1. **United States** — Best for detailed Census Bureau data, BLS stats, robust industry reports
2. **European Union** — Use Eurostat, local statistical agencies; note GDPR/compliance considerations
3. **Global** — World Bank, IMF data; broader but less granular
4. **Specific country/region** — E.g., "Canada," "Southeast Asia," "Latin America"

**Or specify your own region.**

**User response:** [Selection or custom]

**Adaptation logic:**
- If user selected B2B SaaS (Question 1, Option 1) → Emphasize US/EU markets (mature SaaS adoption)
- If user selected Consumer fintech (Question 1, Option 2) → Mention emerging markets (higher mobile adoption)

---

### Question 3: Industry/Market Segments

**Agent asks:**
"What specific industry or market segments does this problem space relate to?"

**Offer 4 enumerated options (adapted based on problem space + geography):**

**Example (if Question 1 = B2B SaaS, Question 2 = US):**
1. **SMB services sector** — 5.4M businesses, $1.2T revenue (US Census, 2023)
2. **Professional services (legal, accounting)** — 1.1M firms, $850B revenue (IBISWorld, 2023)
3. **Healthcare providers** — 900K practices, $4T industry (BLS, 2023)
4. **Tech/software companies** — 500K firms, $1.8T revenue (Statista, 2023)

**Or describe your own industry segment.**

**User response:** [Selection or custom]

**Adaptation logic:**
- If Question 1 = Consumer fintech, offer consumer segments (e.g., "Gen Z 18-25," "Millennials 25-40")
- If Question 1 = Healthcare, offer segments (e.g., "Primary care physicians," "Therapists/counselors")

---

### Question 4: Potential Customers (Demographics/Firmographics)

**Agent asks:**
"Who are the potential customers affected by this problem?"

**Offer 4 enumerated options (adapted based on previous answers):**

**Example (if Question 1 = B2B SaaS, Question 3 = SMB services sector):**
1. **SMBs with 10-50 employees** — 1.2M businesses, $400B revenue (Census Bureau, 2023)
2. **SMBs with 50-250 employees** — 600K businesses, $800B revenue (Census Bureau, 2023)
3. **Solo entrepreneurs/freelancers** — 3.5M self-employed, $200B revenue (BLS, 2023)
4. **Service businesses with online presence** — 2M businesses, $600B e-commerce (Statista, 2023)

**Or describe your own customer segment (firmographics, demographics, income, etc.).**

**User response:** [Selection or custom]

---

### Output: Generate TAM/SAM/SOM Analysis

After collecting responses, the agent generates a structured analysis:

```markdown
# TAM/SAM/SOM Analysis

**Problem Space:** [User's input from Question 1]
**Geographic Region:** [User's input from Question 2]
**Industry/Market Segments:** [User's input from Question 3]
**Potential Customers:** [User's input from Question 4]

---

## Total Addressable Market (TAM)

**Definition:** The total market demand if you captured 100% of potential customers in the problem space.

**Population Estimate:** [Calculated from data sources]
- **Source:** [Citation, e.g., "US Census Bureau, 2023"]
- **Calculation:** [Show math, e.g., "5.4M SMBs × $1.2T revenue = $1.2T TAM"]

**Market Size Estimate:** $[X] billion/million
- **Source:** [Industry report citation]
- **URL:** [Clickable link to source]

---

## Serviceable Available Market (SAM)

**Definition:** The segment of TAM you can realistically target with your product (narrowed by geography, firmographics, product fit).

**Segment of TAM:** [User's narrowed segment from Question 4]

**Population Estimate:** [Calculated]
- **Source:** [Citation]
- **Calculation:** [Show math, e.g., "1.2M SMBs with 10-50 employees"]

**Market Size Estimate:** $[X] billion/million
- **Source:** [Citation]
- **URL:** [Link]

**Assumptions:**
- [List key assumptions, e.g., "Assumes 50% of SMBs have budget for automation tools"]

---

## Serviceable Obtainable Market (SOM)

**Definition:** The portion of SAM you can realistically capture in the next 1-3 years, accounting for competition and market constraints.

**Realistically Capturable Market:** [Agent's estimation based on market maturity, competition]

**Population Estimate:** [Calculated]
- **Source:** [Citation]
- **Calculation:** [Show math, e.g., "1.2M SMBs × 5% market share (Year 1) = 60K customers"]

**Market Size Estimate:** $[X] million
- **Assumptions:**
  - [Competition assumption, e.g., "5 major competitors, market leader has 15% share"]
  - [GTM assumption, e.g., "Sales capacity: 50 customers/month in Year 1"]
  - [Conversion assumption, e.g., "10% trial-to-paid conversion"]

**Year 1-3 Projections:**
- **Year 1:** [X]K customers, $[X]M revenue (5% of SAM)
- **Year 2:** [X]K customers, $[X]M revenue (10% of SAM)
- **Year 3:** [X]K customers, $[X]M revenue (15% of SAM)

---

## Data Sources & Citations

- [Source 1: e.g., "US Census Bureau (2023). County Business Patterns. URL: census.gov"]
- [Source 2: e.g., "IBISWorld (2023). Professional Services Industry Report. URL: ibisworld.com"]
- [Source 3: e.g., "Statista (2023). SMB Software Market Size. URL: statista.com"]
- [Add all sources used]

---

## Validation Questions

1. **Does TAM align with industry reports?** [Compare to 3rd-party market research]
2. **Is SAM realistically serviceable?** [Can your GTM motion reach this segment?]
3. **Is SOM achievable given competition?** [Is 5-15% market share realistic in 3 years?]

---

## Next Steps

1. **Validate with customer interviews:** Does the problem resonate with target segment?
2. **Benchmark against competitors:** What market share do incumbents have?
3. **Refine SOM based on GTM capacity:** Can sales/marketing support this growth?
4. **Update annually:** Markets shift—reassess TAM/SAM/SOM yearly

---

**Would you like to refine any assumptions or explore a different segment?**
```

---

## Examples

### Example 1: Good TAM/SAM/SOM Analysis (B2B SaaS Workflow Automation)

**Step 0 - Context Provided:**
User shares Zapier's homepage copy:
> "Zapier connects your apps and automates workflows. Easy automation for busy people. Move info between your web apps automatically, so you can focus on your most important work."

**Question 1 Response:** "B2B SaaS productivity — Workflow automation for small business operations" (extracted from "automates workflows" and "busy people")
**Question 2 Response:** "United States"
**Question 3 Response:** "SMB services sector"
**Question 4 Response:** "SMBs with 10-50 employees"

---

**Generated Analysis:**

```markdown
# TAM/SAM/SOM Analysis: Workflow Automation for SMBs

**Problem Space:** Workflow automation for small business operations
**Geographic Region:** United States
**Industry/Market Segments:** SMB services sector
**Potential Customers:** SMBs with 10-50 employees

---

## Total Addressable Market (TAM)

**Definition:** Total US market for workflow automation tools across all business sizes.

**Population Estimate:** 33.2M businesses (US Census Bureau, 2023)

**Market Size Estimate:** $50B
- **Source:** Gartner, "Business Process Automation Market, 2023"
- **URL:** [gartner.com/business-automation-report]
- **Breakdown:** $30B (large enterprise), $15B (mid-market), $5B (SMB)

---

## Serviceable Available Market (SAM)

**Definition:** US SMBs (10-50 employees) in services sector that could use workflow automation.

**Segment of TAM:** SMBs with 10-50 employees in services sector

**Population Estimate:** 1.2M businesses
- **Source:** US Census Bureau, "County Business Patterns, 2023"
- **URL:** [census.gov/cbp]
- **Calculation:** 5.4M total SMBs × 22% (10-50 employee size) = 1.2M

**Market Size Estimate:** $3.6B
- **Source:** IBISWorld, "SMB Software Market, 2023"
- **Calculation:** 1.2M businesses × $3,000 avg spend/year = $3.6B
- **URL:** [ibisworld.com/smb-software]

**Assumptions:**
- 50% of SMBs have budget for automation tools ($1.8B addressable)
- Avg $3,000/year spend on software (Statista, 2023)

---

## Serviceable Obtainable Market (SOM)

**Definition:** Market share we can realistically capture in next 3 years.

**Realistically Capturable Market:** 5-15% of SAM over 3 years

**Year 1 Population Estimate:** 12K customers (1% of SAM)
- **Calculation:** 1.2M businesses × 1% = 12K
- **Revenue:** $36M (12K × $3,000 ARPU)

**Year 3 Population Estimate:** 180K customers (15% of SAM)
- **Calculation:** 1.2M businesses × 15% = 180K
- **Revenue:** $540M (180K × $3,000 ARPU)

**Assumptions:**
- **Competition:** 5 major players (Zapier 20% share, Integromat 10%, others <5%)
- **GTM Capacity:** PLG motion, 1K trial signups/month in Year 1, scaling to 15K/month by Year 3
- **Conversion:** 10% trial-to-paid conversion
- **Churn:** 15% annual churn (industry standard for SMB SaaS)

**Year 1-3 Projections:**
- **Year 1:** 12K customers, $36M revenue (1% of SAM)
- **Year 2:** 60K customers, $180M revenue (5% of SAM)
- **Year 3:** 180K customers, $540M revenue (15% of SAM)

---

## Data Sources & Citations

- US Census Bureau (2023). County Business Patterns. [census.gov/cbp]
- Gartner (2023). Business Process Automation Market Report. [gartner.com]
- IBISWorld (2023). SMB Software Market Analysis. [ibisworld.com]
- Statista (2023). SMB Software Spending. [statista.com]

---

## Validation Questions

1. **Does TAM align with industry reports?** ✅ Yes—Gartner estimates $50B total BPA market
2. **Is SAM realistically serviceable?** ✅ Yes—PLG motion can reach 1.2M SMBs via digital marketing
3. **Is SOM achievable given competition?** ⚠️ Stretch goal—Zapier has 20% share; 15% in Year 3 requires strong differentiation

---

## Next Steps

1. **Validate with 20 customer interviews:** Confirm $3K/year budget exists
2. **Benchmark against Zapier/Integromat:** Study their GTM, pricing, churn
3. **Refine SOM based on pilot:** Run 6-month pilot, measure actual conversion/churn
4. **Reassess annually:** SMB market growing 5%/year—update TAM/SAM annually
```

**Why this works:**
- Citations for every data point (Census, Gartner, IBISWorld, Statista)
- Shows math and assumptions transparently
- Realistic SOM (1% → 5% → 15% over 3 years)
- Identifies validation gaps ("⚠️ Stretch goal")

---

### Example 2: Bad TAM/SAM/SOM Analysis (No Citations, Vague)

```markdown
# TAM/SAM/SOM Analysis: Productivity Tool

**TAM:** The productivity market is huge, probably $100 billion.

**SAM:** We're targeting small businesses, so maybe $10 billion.

**SOM:** We think we can get 1% in the first year, so $100 million.
```

**Why this fails:**
- No citations (where did "$100B" come from?)
- Vague segments ("small businesses" = how many? what size?)
- No assumptions documented (1% of SAM—why?)
- No population estimates (how many customers?)
- No validation questions or next steps

---

## Common Pitfalls

### Pitfall 1: TAM Without Citations
**Symptom:** "The market is $50B" (no source)

**Consequence:** Can't defend the number to investors or execs.

**Fix:** Cite industry reports (Gartner, IBISWorld, Statista) with URLs.

---

### Pitfall 2: SOM Equals SAM
**Symptom:** "SAM is $5B, SOM is $5B" (assuming 100% capture)

**Consequence:** Unrealistic projection—no market has zero competition.

**Fix:** SOM should be 1-20% of SAM in Year 1-3, accounting for competition.

---

### Pitfall 3: No Population Estimates
**Symptom:** Only dollar amounts, no customer counts

**Consequence:** Can't build sales/marketing plans without knowing customer volume.

**Fix:** Always include population (e.g., "1.2M businesses" or "60K customers in Year 1").

---

### Pitfall 4: Static Assumptions
**Symptom:** TAM/SAM/SOM calculated once, never updated

**Consequence:** Stale data as markets shift.

**Fix:** Reassess annually. Markets grow/shrink, competition changes, new data emerges.

---

### Pitfall 5: Ignoring GTM Constraints
**Symptom:** "SOM is 50% of SAM in Year 1" (but no sales team)

**Consequence:** SOM isn't realistic given GTM capacity.

**Fix:** Ground SOM in GTM constraints (sales capacity, marketing budget, conversion rates).

---

## References

### Related Skills
- `positioning-statement.md` — TAM/SAM/SOM informs "For [target]" segment size
- `problem-statement.md` — Problem space defines the market
- `recommendation-canvas.md` — Market sizing informs business outcome projections

### External Frameworks
- Steve Blank, *The Four Steps to the Epiphany* (2005) — Market sizing for startups
- Lean Startup methodology — Validate market size with experiments, not just desk research

### Data Sources (For Citations)
- **US:** US Census Bureau, Bureau of Labor Statistics, IBISWorld, Statista
- **Europe:** Eurostat, local statistical agencies
- **Global:** World Bank, IMF, Gartner, Forrester

### Dean's Work
- TAM/SAM/SOM Prompt Generator (multi-turn adaptive market sizing)

---

**Skill type:** Interactive
**Suggested filename:** `tam-sam-som-calculator.md`
**Suggested placement:** `/skills/interactive/`
**Dependencies:** None (standalone interactive skill)
