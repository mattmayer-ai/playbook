# Part 1: Discovery and Synthesis

**Purpose**: Validate problems and synthesize insights before writing PRD.

**Time**: 4-7 hours total

**Output**: Discovery Insights Report (assumptions, hypothesis, insights, problem reframe, recommended direction)

**What's included**: Copy-paste prompts for each step—just fill in your specifics and paste into any AI tool (Claude, ChatGPT, Perplexity, etc.).

***

### Why Discovery and Synthesis

You need evidence-backed direction before writing a PRD. Not full validation—that comes after MVP. Just enough to avoid building something obviously wrong.

**Without this**: "Build a productivity app" → No direction, just assumptions\
**With this**: "Contractors lose bids due to slow estimation (15/15 interviews confirmed), not pricing errors. Build speed-first tool targeting <2 hour estimates vs. 8 hour baseline."

The difference is 4-7 hours of focused discovery with AI assistance.

***

### The Process

Four steps, 4-7 hours total:

1. **AI-Assisted Market Research** (30-60 min) - ALWAYS start here
2. **Pick Your Validation Method** (30 min) - Choose based on what market research revealed
3. **Execute Discovery** (2-4 hours) - Follow your chosen method
4. **Synthesis & Insights** (1-2 hours) - Transform raw data into direction

**Critical**: Step 3 is where product thinking happens. Raw research without synthesis is just data collection.

***

### Step 0: AI-Assisted Market Research (30-60 min)

**START HERE EVERY TIME.** Before you pick a validation method, get AI to map the landscape.

Use Claude with web search, ChatGPT with browsing, or Perplexity.

#### What You're Learning

* Who are the existing players?
* What do they cost?
* What are users complaining about?
* What gaps exist?
* Are there regulatory constraints?

#### Copy-Paste Prompt

```
I have an idea for: [YOUR IDEA - 1-2 sentences]

Help me research the market:

1. **Existing solutions**: Who are the top 5-7 competitors/alternatives? 
   - Use web search to find them
   - Include both direct competitors and adjacent solutions

2. **Pricing landscape**: What do these solutions cost?
   - Find pricing pages
   - Note free tiers, entry-level plans, enterprise pricing

3. **User complaints**: What are people saying is broken?
   - Search Reddit, G2, Capterra for "[competitor name] review"
   - Look for patterns in negative reviews
   - Find forum discussions about problems in this space

4. **Market gaps**: What's missing?
   - Features users are asking for
   - Use cases not being served
   - Underserved user segments

5. **Regulatory landscape**: Are there compliance requirements?
   - HIPAA, GDPR, industry-specific regulations
   - Data handling requirements
   - Certification or licensing needs

Synthesize findings into:
- Competitive landscape table
- Common user complaints
- Identified gaps
- Regulatory constraints (if any)
- Pricing benchmarks

Format as markdown with clear sections.
```

#### Decision Point

Based on market research:

* **Competitors exist but users complain** → Proceed to Step 1
* **Market saturated, users happy** → Consider different idea
* **No competitors exist** → Validate the problem is real

***

### Step 1: Pick Your Validation Method (30 min)

Choose ONE based on what you're uncertain about.

#### Option A: User Interviews

**Use when**: You have a problem hypothesis but don't know if it's painful enough

**What to do**:

* Find 3-5 people who have the problem
* 30-minute calls each
* Ask: What's your current workflow? Where does it break? How much time/money does that cost?

**Time**: 3-4 hours (includes recruitment, calls, synthesis)

**Copy-Paste Prompt**:

```
I'm building [YOUR PRODUCT IDEA - 1-2 sentences].

Target users: [WHO - e.g., "elementary teachers", "construction contractors"]
Problem I think they have: [PROBLEM]

Create an interview script for 30-minute calls. Generate 10-12 open-ended questions that:

1. Understand current workflow (3-4 questions)
2. Identify pain points (3-4 questions)
3. Quantify impact (2-3 questions)
4. Test solution fit (2-3 questions)

Avoid leading questions. Don't describe my solution—focus on their problem.
Format as numbered list with follow-up probes.
```

#### Option B: Deep Problem Research

**Use when**: Market research shows complaints exist, but you need deeper understanding

**What to do**:

* Use AI to search forums, Reddit, Twitter for actual user complaints
* Analyze language patterns
* Identify specific user segments
* Quantify severity

**Time**: 1-2 hours (AI-assisted research)

**Copy-Paste Prompt**:

```
Based on this market research: [PASTE YOUR MARKET RESEARCH FROM STEP 0]

Now find the user voice. Search for:

1. Reddit discussions in relevant subreddits
2. Forum discussions with problem keywords
3. Twitter/X conversations

Focus on finding:
- WHO specifically has this problem
- HOW they describe it (their words, not industry jargon)
- WHAT they've tried (existing solutions, workarounds, why they failed)
- HOW SEVERE (quantifiable impact: hours wasted, money lost)

Organize findings by:
- User segment
- Pain point themes (with frequency count)
- Verbatim quotes
- Quantified impact

Format as markdown with clear sections and quote attribution.
```

#### Option C: Quick Technical Experiment

**Use when**: You're unsure if the technical approach will work

**What to do**:

* Build smallest possible test (1-3 hours of coding)
* Example: If building AI tool, test prompt quality with 5-10 examples
* Example: If building integration, test API with sample data

**Time**: 2-4 hours (includes coding, testing, analysis)

**Copy-Paste Prompt**:

```
I want to build [YOUR PRODUCT] using [AI MODEL/API].

Help me design a quick test to validate feasibility:

1. Generate 10 test cases representing typical use
2. For each test case, write:
   - Input (what user would provide)
   - Expected output (what constitutes "success")
   - Acceptance criteria (how to judge if it's good enough)

3. Provide code template to run the test

Target language: [Python/JavaScript/etc.]
API/Model: [Anthropic Claude/OpenAI/etc.]
```

***

### Step 2: Execute Discovery (2-4 hours)

#### If You Chose User Interviews

After conducting 3-5 interviews, synthesize findings.

**Copy-Paste Synthesis Prompt**:

```
I conducted [NUMBER] user interviews about [PROBLEM AREA].

Here are my raw notes from each interview:

**Interview 1**: [PASTE NOTES]
**Interview 2**: [PASTE NOTES]
[Continue for all interviews]

Synthesize these findings:

1. **Current workflow patterns**
2. **Pain point themes** (ranked by frequency, include verbatim quotes)
3. **Quantified impact** (time wasted, money lost, consequences)
4. **Current workarounds** (what they do now, why it doesn't work)
5. **Willingness to change** (motivation, what would make them try new solution)
6. **Decision**: Build / Don't build / Need more data (with reasoning)

Format as markdown with clear sections.
```

#### If You Chose Deep Problem Research

Use AI to analyze forum/Reddit posts.

**Copy-Paste Synthesis Prompt**:

```
Based on the user voice research you did, organize findings:

1. **User segments** (who has this problem? Which segment most underserved?)
2. **Pain point themes** (ranked by frequency with vivid quotes)
3. **Quantified impact** (from user posts)
4. **Why current solutions fail** (with quotes)
5. **Our opportunity** (gap we can fill, segment to target, minimum viable solution)

**Decision**: Build / Don't build / Need more data (with reasoning)

Format as markdown.
```

#### If You Chose Quick Technical Experiment

After running test code, analyze results.

**Example Analysis**:

```markdown
## Technical Validation: [What You Tested]

**Test date**: [Date]
**Test cases**: [Number and types]
**Model/API tested**: [Technology]

**Results**:
- Acceptable quality: X/Y (Z%)
- Issues found: [List]
- Performance: [Metrics]

**Workarounds identified**: [Solutions to issues]

**Decision**: Proceed / Improve approach / Different technology
**Reasoning**: [Based on test results]
```

***

### Step 3: Synthesis & Insights (1-2 hours)

**This is where product thinking happens.** Transform raw research into actionable direction.

You now have market research and discovery data. Before writing a PRD, synthesize findings into:

* **Assumptions Matrix** (validated vs. needs testing)
* **Hypothesis** (testable statement about solution)
* **Key Insights** (evidence-backed learnings)
* **Problem Reframe** (shift from assumptions to evidence)
* **Recommended Direction** (which solution to build and why)

#### Component 1: Assumptions Matrix

**Copy-Paste Prompt**:

```
Based on my discovery work:

[PASTE MARKET RESEARCH FROM STEP 0]
[PASTE DISCOVERY FINDINGS FROM STEP 2]

Create an Assumptions Matrix with 8-12 assumptions:

For each assumption:
1. Assumption statement (specific, testable)
2. Confidence level: HIGH (multiple sources confirm) or TO VALIDATE (needs confirmation)
3. Evidence (what supports this)
4. Risk if wrong (what breaks)

Format as table:

| # | Assumption | Confidence | Evidence | Risk if Wrong |
|---|------------|------------|----------|---------------|
| 1 | [Statement] | HIGH / TO VALIDATE | [Source] | [Impact] |

Group by: High Confidence vs. To Validate
```

**Example Output**:

```markdown
## Assumptions Matrix

### High Confidence

| # | Assumption | Evidence | Risk if Wrong |
|---|------------|----------|---------------|
| 1 | Sites use paper/spreadsheets for pre-screening | Industry surveys | Solving wrong bottleneck |
| 2 | Funnel breaks early - 56% fail before connection | Tufts CSDD study | Optimizing wrong part |

### To Validate

| # | Assumption | Logical Basis | Risk if Wrong |
|---|------------|---------------|---------------|
| 7 | Our users have similar pain points | Industry patterns apply | Solution doesn't fit workflow |
```

#### Component 2: Hypothesis Formation

**Structure**:

```
We believe that [problem statement] because [evidence].

A solution that [approach] will [outcome] without [constraint].

Validation status: [Supported/Partial/Invalidated] based on [evidence].
```

**Copy-Paste Prompt**:

```
Based on discovery work and assumptions matrix:

[PASTE MARKET RESEARCH]
[PASTE ASSUMPTIONS MATRIX]

Create testable hypothesis:

**Initial Hypothesis**:
We believe that [WHO] struggles with [PROBLEM] because [ROOT CAUSE backed by evidence].

A solution that [APPROACH] will [MEASURABLE OUTCOME] without [CONSTRAINTS].

**Validation Status**: SUPPORTED / PARTIAL / INVALIDATED

Based on [EVIDENCE]:
☑ [Supporting evidence 1]
☑ [Supporting evidence 2]

**Success Criteria**:
- [Metric 1]: [Target]
- [Metric 2]: [Target]

**Failure Criteria**:
- [Metric]: [Threshold for pivot]
```

#### Component 3: Key Insights

**Purpose**: Extract the "so what?" from research data.

**Copy-Paste Prompt**:

```
Based on research, identify 5-7 KEY INSIGHTS:

[PASTE MARKET RESEARCH]
[PASTE DISCOVERY FINDINGS]

For each insight:
1. Title: Short, punchy statement
2. Evidence: 3-5 specific data points
3. Implication: What this means for solution design

Insights should challenge assumptions and reveal patterns.

Format as:

## Insight 1: [Title]

**Evidence**:
• [Data point with source]
• [Data point with source]

**Implication**: [What this means]
```

**Example Output**:

```markdown
## Insight 1: Problem is Access, Not Willingness

**Evidence**:
• 56% of failures occur because no one connected patient to trial
• Only 2-8% participate, but climbs when friction reduced
• Decentralized trials show 96% retention vs. 70%

**Implication**: Focus on surfacing eligible patients and reducing friction, not "convincing" patients.
```

#### Component 4: Problem Reframe

**Purpose**: Show how evidence changed your understanding.

**Copy-Paste Prompt**:

```
Create PROBLEM REFRAME showing how evidence changed understanding:

[PASTE INITIAL IDEA/ASSUMPTION]
[PASTE KEY INSIGHTS]

**What We Thought**:
[Initial problem assumption]

**What Research Revealed**:
[Evidence-backed actual problem]

**Core Reframe**:
[New problem statement - specific, evidence-backed]
```

**Example Output**:

```markdown
**What We Thought**: Patients aren't participating because they fear trials

**What Research Revealed**: 56% never connected to trials—problem is access, not fear

**Core Reframe**: Eligible patients exist but aren't being connected to the right trial at the right moment. This is an access problem, not a willingness problem.
```

#### Component 5: Recommended Direction

**Copy-Paste Prompt**:

```
Recommend which solution to build:

[PASTE PROBLEM REFRAME]
[PASTE KEY INSIGHTS]
[PASTE ASSUMPTIONS MATRIX]

## Options Considered

Create 3 solution options with:
- Description
- Problems addressed
- Pros/cons

## Recommended: Option [X]

**Why This Option**: [Evidence-based reasoning]

**Core Capabilities** (MVP):
1. [Capability]: [Why essential]
2. [Capability]: [Why essential]

**Out of Scope** (V2+):
- [Feature]: [Why deferring]

**Validation Plan**:
1. [First assumption to test]
```

#### Compile Discovery Insights Report

**Copy-Paste Prompt**:

```
Compile all components into Discovery Insights Report:

[PASTE ASSUMPTIONS MATRIX]
[PASTE HYPOTHESIS]
[PASTE KEY INSIGHTS]
[PASTE PROBLEM REFRAME]
[PASTE RECOMMENDED DIRECTION]

Create structured report with sections:
- Executive Summary (reframe + recommendation)
- Hypothesis
- Methodology
- Assumptions Matrix
- Key Insights
- Problem Reframe
- Recommended Direction
- What to Validate Next

Format as professional markdown.
```

***

### Summary: Discovery and Synthesis (4-7 hours)

**What you produce**: 0. Market research (30-60 min): Competitive landscape, user complaints, gaps

1. Validation method choice (30 min): Pick ONE based on market research
2. Discovery execution (2-4 hours): User interviews OR problem research OR technical experiment
3. Synthesis & insights (1-2 hours): Assumptions, hypothesis, insights, reframe, direction

**Total time**: 4-7 hours

**Tools**: Any conversational AI (Claude, ChatGPT, Perplexity) with web search

**Output**: Discovery Insights Report with evidence-backed direction

#### When to invest more time

* **Regulated industry** (healthcare, finance) - add 2-4 hours for compliance research
* **Unfamiliar domain** - add 2-3 hours for deeper market research
* **High technical risk** - add 2-4 hours for extensive proof-of-concept
* **Enterprise sales** - add 3-4 hours for buyer persona research

#### Red flags: don't build

* Market research shows no complaints
* Users can't quantify the problem
* Technical experiment shows fundamental blockers
* Regulatory requirements prohibitively complex
* Saturated market with happy users

#### Green lights: proceed to PRD

* 3+ users articulate same pain point
* Quantified impact (time/money) is significant
* Technical feasibility validated
* Clear gap in competitive landscape
* Users express willingness to pay

***

**Next**: Part 2: PRD Development
