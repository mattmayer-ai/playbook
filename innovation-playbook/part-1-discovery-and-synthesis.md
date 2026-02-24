# Part 1: Discovery and Synthesis

### Overview

Discovery is the intellectual work before building. Most projects fail not because of bad execution, but because they solve the wrong problem.

This section covers:

* **Step 0:** Problem Interrogation — Question the brief, research what exists, identify the real gap
* **Step 1:** Assumption Cataloguing — List what must be true, rank by risk
* **Step 2:** Hypothesis Development — Formulate testable hypothesis, evolve through versions
* **Step 3:** Validation Method Selection — Pick the right approach
* **Step 4:** Execute Discovery — Gather evidence
* **Step 5:** Synthesis & Insights — Transform raw data into direction

**Total time:** 4-8 hours (not weeks)

**Output:** Discovery Insights Report with evidence-backed direction

***

### Step 0: Problem Interrogation (1-2 hours)

Before validating, ensure you're solving the right problem. The brief is often wrong.

#### Question the Brief

Every brief contains embedded assumptions. Surface them before accepting them.

<table><thead><tr><th width="330">Question</th><th>What You're Looking For</th></tr></thead><tbody><tr><td>What's the stated problem?</td><td>The surface-level issue as presented</td></tr><tr><td>What assumptions are embedded?</td><td>What the brief takes for granted</td></tr><tr><td>Who defined this problem?</td><td>Perspective and potential blind spots</td></tr><tr><td>What would success look like?</td><td>Implicit definition of "solved"</td></tr><tr><td>What's NOT being said?</td><td>Gaps, constraints, politics</td></tr></tbody></table>

**Red flags in briefs:**

* Solution embedded in problem statement ("We need an AI to...")
* Vague user definition ("users struggle with...")
* No quantified impact ("costs are high...")
* Assumed causation ("because of X, Y happens...")

**Output:** List of embedded assumptions to investigate.

***

#### Research What Exists

Before proposing solutions, understand the landscape. This step prevents building what already exists.

<table><thead><tr><th width="281">Research Area</th><th>Questions</th></tr></thead><tbody><tr><td><strong>Existing solutions</strong></td><td>What's already been built? What's in market?</td></tr><tr><td><strong>Previous attempts</strong></td><td>What's been tried internally? Why did it fail/succeed?</td></tr><tr><td><strong>Adjacent solutions</strong></td><td>What solves similar problems in other domains?</td></tr><tr><td><strong>Emerging capabilities</strong></td><td>What's newly possible that wasn't before?</td></tr><tr><td><strong>Partnerships available</strong></td><td>Can we partner instead of build?</td></tr></tbody></table>

**Copy-Paste Prompt:**

```
I'm exploring a problem: [PROBLEM STATEMENT]

Help me research what exists:

1. **Existing solutions**: Who are the top 5-7 competitors/alternatives?
   - Direct competitors
   - Adjacent solutions
   - Enterprise vs. consumer options

2. **What's working**: What do existing solutions do well?
   - Features users praise
   - Problems they've solved

3. **What's failing**: What are users complaining about?
   - Search Reddit, G2, forums for complaints
   - Patterns in negative reviews

4. **Recent developments**: What's changed in the last 12 months?
   - New entrants
   - Technology shifts
   - Regulatory changes

5. **Gaps identified**: What's missing?
   - Features users request
   - Use cases not served
   - User segments ignored

Format as markdown with clear sections.
```

**Output:** Landscape summary — what exists, what works, what gaps remain.

***

#### Identify the Real Gap

The stated problem is often a symptom. Find the root cause.

<table><thead><tr><th width="254">Technique</th><th>Application</th></tr></thead><tbody><tr><td><strong>"Why" chain</strong></td><td>Ask "why" 3-5 times to move from symptom to cause</td></tr><tr><td><strong>Funnel analysis</strong></td><td>Where are users/customers actually lost?</td></tr><tr><td><strong>Constraint mapping</strong></td><td>What's actually blocking progress?</td></tr><tr><td><strong>Reframing</strong></td><td>What if the opposite of the stated problem is true?</td></tr></tbody></table>

**Reframing Template:**

| Old Framing       | Evidence Against          | New Framing         |
| ----------------- | ------------------------- | ------------------- |
| \[Stated problem] | \[What research revealed] | \[Reframed problem] |

**Output:** Reframed problem statement that addresses root cause, not symptoms.

***

#### Step 0 Summary

<table><thead><tr><th width="261">Activity</th><th width="188">Time</th><th>Output</th></tr></thead><tbody><tr><td>Question the brief</td><td>15 min</td><td>Embedded assumptions list</td></tr><tr><td>Research what exists</td><td>30-45 min</td><td>Landscape summary</td></tr><tr><td>Identify the real gap</td><td>15-30 min</td><td>Reframed problem statement</td></tr></tbody></table>

**Total Step 0:** 1-2 hours

**Why this matters:** This prevents building what already exists, solving symptoms instead of root causes, and validating solutions before validating problems.

***

### Step 1: Assumption Cataloguing (30-45 min)

List what must be true for your solution to work. Be explicit. Implicit assumptions are the ones that kill projects.

#### Assumption Categories

<table><thead><tr><th width="157">Category</th><th width="238">Question</th><th>Examples</th></tr></thead><tbody><tr><td><strong>Desirability</strong></td><td>Do users want this?</td><td>Users will adopt new workflow; Users will pay for this</td></tr><tr><td><strong>Feasibility</strong></td><td>Can we build it?</td><td>API provides needed data; AI accuracy is sufficient</td></tr><tr><td><strong>Viability</strong></td><td>Does the business work?</td><td>ROI justifies investment; We can scale support</td></tr></tbody></table>

#### Assumption Template

For each assumption:

<table><thead><tr><th width="196">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>ID</strong></td><td>A1, A2, A3...</td></tr><tr><td><strong>Assumption</strong></td><td>What we believe to be true</td></tr><tr><td><strong>Category</strong></td><td>Desirability / Feasibility / Viability</td></tr><tr><td><strong>Importance</strong></td><td>How critical is this? (1-10)</td></tr><tr><td><strong>Evidence</strong></td><td>What do we know? (High / Medium / Low)</td></tr><tr><td><strong>Risk</strong></td><td>What happens if we're wrong?</td></tr></tbody></table>

#### Example Assumption Matrix

<table><thead><tr><th width="73">ID</th><th>Assumption</th><th>Category</th><th width="115">Importance</th><th width="105">Evidence</th><th>Risk if Wrong</th></tr></thead><tbody><tr><td>A1</td><td>Users want a unified platform</td><td>Desirability</td><td>9/10</td><td>Low</td><td>Build something nobody uses</td></tr><tr><td>A2</td><td>Existing tools can be integrated</td><td>Feasibility</td><td>7/10</td><td>Medium</td><td>Technical blocker</td></tr><tr><td>A3</td><td>Users will adopt new workflows</td><td>Desirability</td><td>8/10</td><td>Low</td><td>Adoption fails</td></tr><tr><td>A4</td><td>ROI justifies 12-month investment</td><td>Viability</td><td>7/10</td><td>Low</td><td>No budget for scale</td></tr></tbody></table>

#### Prioritization

**Test first:** High importance + Low evidence

**Defer:** Low importance OR High evidence (already validated)

**Copy-Paste Prompt:**

```
Based on this problem and landscape research:

[PASTE PROBLEM STATEMENT]
[PASTE LANDSCAPE RESEARCH]

Help me catalogue assumptions:

1. List 8-12 assumptions that must be true for a solution to work
2. Categorize each as: Desirability / Feasibility / Viability
3. Rate importance (1-10)
4. Rate current evidence level (High / Medium / Low)
5. Describe risk if assumption is wrong

Format as table:

| ID | Assumption | Category | Importance | Evidence | Risk if Wrong |
|----|------------|----------|------------|----------|---------------|

Then identify:
- Top 3 assumptions to test first (high importance, low evidence)
- Assumptions we can defer (low importance or already validated)
```

**Output:** Ranked list of 8-12 assumptions with testing priority.

***

### Step 2: Hypothesis Development (30-45 min)

A hypothesis connects intervention to outcome with a mechanism. It's what you're betting on.

#### Hypothesis Structure

> "If we \[intervention], then \[outcome], because \[mechanism]."

**Components:**

<table><thead><tr><th width="187">Component</th><th width="236">Description</th><th>Example</th></tr></thead><tbody><tr><td><strong>Intervention</strong></td><td>What we're doing</td><td>"provide unified workflow tools"</td></tr><tr><td><strong>Outcome</strong></td><td>Measurable result</td><td>"conversion rates improve 20%"</td></tr><tr><td><strong>Mechanism</strong></td><td>Why it works</td><td>"reduced cognitive load enables focus"</td></tr></tbody></table>

#### Characteristics of a Good Hypothesis

<table><thead><tr><th width="211">Characteristic</th><th>Description</th><th>Test</th></tr></thead><tbody><tr><td><strong>Testable</strong></td><td>Can be validated with an experiment</td><td>Can you design an experiment?</td></tr><tr><td><strong>Falsifiable</strong></td><td>Clear criteria for being wrong</td><td>What would disprove it?</td></tr><tr><td><strong>Specific</strong></td><td>Not vague or unmeasurable</td><td>Are metrics defined?</td></tr><tr><td><strong>Mechanism-driven</strong></td><td>Explains why it would work</td><td>Can you explain the causal chain?</td></tr></tbody></table>

#### Hypothesis Evolution

First attempts are usually too narrow or too broad. Expect to iterate.

<table><thead><tr><th width="109">Version</th><th>Common Problem</th><th>Fix</th></tr></thead><tbody><tr><td>V1</td><td>Too narrow — focuses on feature, not outcome</td><td>Zoom out to user outcome</td></tr><tr><td>V2</td><td>Too broad — hard to measure</td><td>Add specific metrics and mechanism</td></tr><tr><td>V3</td><td>Right level — testable, falsifiable, specific</td><td>Ready to validate</td></tr></tbody></table>

**Example Evolution:**

**V1 (Too narrow):**

> "If we reduce matching time from 2 hours to 5 minutes, contacts increase."

_Problem: Focuses on time, not user outcome._

**V2 (Too broad):**

> "A unified platform will improve conversion at each funnel stage."

_Problem: Hard to measure, no mechanism._

**V3 (Right level):**

> "If we empower coordinators with the right information at the right moment, conversion rates improve—because confident coordinators have better conversations, and better conversations maintain engagement."

_Why this works: Testable (confidence, resource usage), falsifiable (if confidence doesn't improve, hypothesis fails), mechanism explains the causal chain._

#### Causal Chain

Map how your intervention leads to outcomes:

```
[Intervention]
    ↓
[Immediate effect]
    ↓
[Behavioral change]
    ↓
[Measurable outcome]
```

**Output:** Single testable hypothesis with clear mechanism.

***

### Step 3: Define What We're NOT Building (15-20 min)

Explicit scope boundaries prevent drift. If you can't say what's out of scope, you don't understand the problem well enough.

#### Out of Scope Categories

<table><thead><tr><th width="281">Category</th><th>Reason to Exclude</th></tr></thead><tbody><tr><td><strong>Already solved</strong></td><td>Existing tools/partnerships handle this</td></tr><tr><td><strong>Outside control</strong></td><td>Regulatory, organizational, political constraints</td></tr><tr><td><strong>Dependent</strong></td><td>Must validate core hypothesis first</td></tr><tr><td><strong>Low priority</strong></td><td>Nice-to-have, not must-have</td></tr><tr><td><strong>Too complex</strong></td><td>Risk outweighs value for initial validation</td></tr></tbody></table>

#### Template

| Out of Scope        | Reason           | When to Revisit                |
| ------------------- | ---------------- | ------------------------------ |
| \[Solution/Feature] | \[Why excluding] | \[Condition for reconsidering] |

**Example:**

| Out of Scope         | Reason                      | When to Revisit                 |
| -------------------- | --------------------------- | ------------------------------- |
| Custom AI model      | Partnership exists (Tempus) | If partnership doesn't deliver  |
| Decentralized trials | Regulatory complexity       | After core hypothesis validated |
| Financial incentives | Outside product scope       | If adoption is the bottleneck   |

**Output:** Explicit scope boundaries with rationale.

***

### Step 4: Validation Method Selection (30 min)

Now that you have a hypothesis and assumptions, pick the right validation method.

#### Choose Based on What You're Uncertain About

<table><thead><tr><th width="401">If you need to understand...</th><th>Use</th></tr></thead><tbody><tr><td>User pain points and workflows</td><td>User Interviews</td></tr><tr><td>Market landscape and competition</td><td>Industry Research</td></tr><tr><td>Technical feasibility</td><td>Quick Experiment</td></tr><tr><td>Problem space from scratch</td><td>Problem Research</td></tr></tbody></table>

#### Validation Methods

**User Interviews**

**When:** You need to understand pain points, workflows, or adoption likelihood.

**Scope:**

* 3-5 users (more if high variance)
* 30 minutes each
* Semi-structured (have questions, but follow threads)

**Key Questions:**

* "Walk me through the last time you \[relevant task]..."
* "What's the hardest part about \[problem area]?"
* "What tools do you currently use? What's frustrating about them?"
* "If you could wave a magic wand, what would change?"

**Copy-Paste Prompt:**

```
I'm validating this hypothesis: [YOUR HYPOTHESIS]

Target users: [WHO]
Problem area: [PROBLEM]

Create an interview script for 30-minute calls:

1. Current workflow questions (3-4) - How they do this today
2. Pain point questions (3-4) - Where it breaks down
3. Impact questions (2-3) - Time/money/consequence
4. Solution fit questions (2-3) - Reaction to approach

Avoid leading questions. Focus on their problem, not my solution.
Format as numbered list with follow-up probes.
```

**Output:** Pain points validated, workflow understood, language captured.

***

**Industry Research**

**When:** You need market context, competitive landscape, or regulatory understanding.

**Scope:**

* 2-4 hours of focused research
* AI-assisted for speed
* Primary sources over summaries

**Research Areas:**

* Competitive solutions (what exists, what's missing)
* Industry reports (market size, trends)
* Regulatory landscape (constraints, upcoming changes)
* Case studies (what's worked, what's failed)

**Output:** Landscape summary, competitive positioning, regulatory constraints.

***

**Quick Experiment**

**When:** You need to test technical feasibility or validate a specific assumption.

**Scope:**

* 2-4 hours
* Minimal viable test
* Clear success criteria

**Types:**

* Technical spike (can we build it?)
* Prototype test (do users understand it?)
* Data validation (does the data exist and work?)

**Output:** Feasibility validated, technical constraints identified.

***

**Problem Research**

**When:** You're starting from scratch and need to understand the problem space.

**Scope:**

* 4-8 hours
* AI-assisted synthesis
* Multiple source types

**Activities:**

* Define problem boundaries
* Identify stakeholders
* Map existing solutions
* Surface root causes

**Output:** Problem definition, stakeholder map, initial assumptions.

***

### Step 5: Execute Discovery (2-4 hours)

Run your chosen validation method. Document as you go.

#### During Discovery

<table><thead><tr><th width="274">Activity</th><th>Purpose</th></tr></thead><tbody><tr><td>Take raw notes</td><td>Capture exact language, not interpretations</td></tr><tr><td>Note surprises</td><td>What contradicts your assumptions?</td></tr><tr><td>Track patterns</td><td>What themes emerge across sources?</td></tr><tr><td>Flag unknowns</td><td>What questions remain unanswered?</td></tr></tbody></table>

#### After Discovery

<table><thead><tr><th width="270">Activity</th><th>Purpose</th></tr></thead><tbody><tr><td>Synthesize findings</td><td>What did you learn?</td></tr><tr><td>Update assumptions</td><td>Which are validated? Invalidated? Still unknown?</td></tr><tr><td>Refine hypothesis</td><td>Does it still hold? Need adjustment?</td></tr><tr><td>Identify gaps</td><td>What do you still need to learn?</td></tr></tbody></table>

**Output:** Discovery summary with validated/invalidated assumptions.

***

### Step 6: Synthesis & Insights (1-2 hours)

Transform raw research into actionable direction. This is where product thinking happens.

#### Component 1: Key Insights

Extract the "so what?" from research data.

**Copy-Paste Prompt:**

```
Based on this research:

[PASTE DISCOVERY FINDINGS]

Identify 5-7 KEY INSIGHTS:

For each insight:
1. Title: Short, punchy statement
2. Evidence: 3-5 specific data points
3. Implication: What this means for solution design

Format as:

## Insight 1: [Title]

**Evidence:**
• [Data point with source]
• [Data point with source]

**Implication:** [What this means]
```

***

#### Component 2: Problem Reframe

Show how evidence changed your understanding.

| What We Thought       | What Research Revealed | Reframed Problem     |
| --------------------- | ---------------------- | -------------------- |
| \[Initial assumption] | \[Evidence]            | \[New understanding] |

***

#### Component 3: Updated Assumptions

| ID | Assumption   | Status                                   | Evidence           |
| -- | ------------ | ---------------------------------------- | ------------------ |
| A1 | \[Statement] | ✅ Validated / ❌ Invalidated / ⚠️ Partial | \[What we learned] |

***

#### Component 4: Recommended Direction

Based on evidence, what should we do?

| Option   | Description | Pros        | Cons     |
| -------- | ----------- | ----------- | -------- |
| Option A | \[Approach] | \[Benefits] | \[Risks] |
| Option B | \[Approach] | \[Benefits] | \[Risks] |

**Recommended:** \[Option] because \[evidence-based reasoning]

***

#### Component 5: Compile Discovery Insights Report

**Copy-Paste Prompt:**

```
Compile all components into Discovery Insights Report:

[PASTE KEY INSIGHTS]
[PASTE PROBLEM REFRAME]
[PASTE UPDATED ASSUMPTIONS]
[PASTE RECOMMENDED DIRECTION]

Create structured report:

# Discovery Insights Report

## Executive Summary
[Reframe + recommendation in 2-3 sentences]

## Hypothesis
[Final hypothesis statement]

## Key Insights
[Numbered list with evidence]

## Problem Reframe
[Old → New understanding]

## Assumptions Matrix
[Updated with validation status]

## Recommended Direction
[What to build, what not to build, why]

## What to Validate Next
[Remaining unknowns for Phase 2]

Format as professional markdown.
```

***

### Discovery Summary

<table><thead><tr><th width="334">Step</th><th width="154">Time</th><th>Output</th></tr></thead><tbody><tr><td>Step 0: Problem Interrogation</td><td>1-2 hrs</td><td>Assumptions list, landscape, reframed problem</td></tr><tr><td>Step 1: Assumption Cataloguing</td><td>30-45 min</td><td>Ranked assumption matrix</td></tr><tr><td>Step 2: Hypothesis Development</td><td>30-45 min</td><td>Testable hypothesis</td></tr><tr><td>Step 3: Define What We're NOT Building</td><td>15-20 min</td><td>Explicit scope boundaries</td></tr><tr><td>Step 4: Validation Method Selection</td><td>30 min</td><td>Method selected</td></tr><tr><td>Step 5: Execute Discovery</td><td>2-4 hrs</td><td>Evidence gathered</td></tr><tr><td>Step 6: Synthesis &#x26; Insights</td><td>1-2 hrs</td><td>Discovery Insights Report</td></tr></tbody></table>

**Total: 4-8 hours**

***

### Common Mistakes

| Mistake                        | Consequence                                      | Prevention                                |
| ------------------------------ | ------------------------------------------------ | ----------------------------------------- |
| Skipping problem interrogation | Build what already exists or solve wrong problem | Always question the brief first           |
| Implicit assumptions           | Unvalidated beliefs drive decisions              | Write assumptions down explicitly         |
| Solution before problem        | Validate solution nobody wants                   | Validate problem before solution          |
| No "out of scope" definition   | Scope creep, unfocused effort                    | Explicitly define boundaries              |
| Too much research              | Analysis paralysis                               | Timebox discovery, move to validation     |
| Too little research            | Build on false assumptions                       | Do Step 0 even when you "know" the answer |
| Hypothesis without mechanism   | Can't diagnose why it fails                      | Always include "because"                  |

***

### Transition to Part 2

With discovery complete, you have:

* ✅ Reframed problem statement
* ✅ Explicit assumptions (validated and unvalidated)
* ✅ Testable hypothesis with mechanism
* ✅ Scope boundaries (what we're NOT building)
* ✅ Discovery Insights Report with direction

**Next: Part 2: PRD Development** — Transform insights into implementation-ready specification.
