# Discovery Prompts - Quick Reference

Copy-paste these prompts into Claude, ChatGPT, Perplexity, or any AI tool. Just fill in the [BRACKETED] sections with your specifics.

---

## Step 0: Market Research (30-60 min)

**Use in**: Claude with web search, ChatGPT with browsing, or Perplexity

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

---

## Step 1A: User Interview Script

**Use in**: Any AI tool

```
I'm building [YOUR PRODUCT IDEA - 1-2 sentences].

Target users: [WHO - e.g., "elementary teachers", "construction contractors"]

Problem I think they have: [PROBLEM - e.g., "spend too much time on lesson planning"]

Create an interview script for 30-minute calls. Generate 10-12 open-ended questions that:

1. Understand current workflow (3-4 questions)
   - How they do this task today
   - Tools they currently use
   - Time it takes

2. Identify pain points (3-4 questions)
   - Where current process breaks down
   - Most frustrating parts
   - Impact on their work

3. Quantify impact (2-3 questions)
   - Time wasted per week/month
   - Money lost due to this problem
   - What happens if problem isn't solved

4. Test solution fit (2-3 questions)
   - Willingness to try new solution
   - What would make them NOT use it
   - Price sensitivity

Avoid leading questions. Don't describe my solution—focus on their problem.
Format as numbered list with follow-up probes for each question.
```

---

## Step 1B: Deep Problem Research

**Use in**: Claude with web search, ChatGPT with browsing, or Perplexity

```
Based on this market research: [PASTE YOUR MARKET RESEARCH FROM STEP 0]

Now find the user voice. Search for:

1. Reddit discussions
   - Search r/[relevant subreddits] for posts about [problem area]
   - Find threads where users complain about current solutions
   - Extract verbatim quotes about pain points

2. Forum discussions
   - Search [relevant forums] for [problem keywords]
   - Find specific examples of users describing the problem
   - Note how they quantify impact (time, money, frustration)

3. Twitter/X conversations
   - Search for [problem keywords] + complaint keywords
   - Find users talking about this problem
   - Note patterns in their language

Focus on finding:
- WHO specifically has this problem (job titles, contexts, situations)
- HOW they describe it (their words, not industry jargon)
- WHAT they've tried (existing solutions, workarounds, why they failed)
- HOW SEVERE (quantifiable impact: hours wasted, money lost, consequences)

Organize findings by:
- User segment (e.g., "elementary teachers", "general contractors bidding $500K-$5M projects")
- Pain point themes (with frequency count)
- Verbatim quotes (most vivid examples)
- Quantified impact (time/cost data from posts)

Format as markdown with clear sections and quote attribution.
```

---

## Step 1C: Technical Feasibility Test (AI Quality)

**Use in**: Any AI tool

```
I want to build [YOUR PRODUCT] using [AI MODEL/API].

Help me design a quick test to validate feasibility:

1. Generate 10 test cases that represent typical use
   - Cover edge cases
   - Include both simple and complex examples
   - Represent real user scenarios

2. For each test case, write:
   - Input (what user would provide)
   - Expected output (what constitutes "success")
   - Acceptance criteria (how to judge if it's good enough)

3. Provide code template to run the test:
   - Loop through test cases
   - Call API
   - Evaluate results against criteria
   - Calculate success rate

Target language: [Python/JavaScript/etc.]
API/Model: [Anthropic Claude/OpenAI/etc.]
```

---

## Step 1C: Technical Feasibility Test (API Integration)

**Use in**: Any AI tool

```
I want to integrate with [EXTERNAL API/SERVICE] to get [WHAT DATA].

Help me test if this is feasible:

1. Find the API documentation
   - Identify required endpoints
   - Check authentication requirements
   - Note rate limits and costs

2. Generate test code to:
   - Authenticate with API
   - Fetch sample data (5-10 test queries)
   - Check if data includes what we need
   - Measure response times

3. Evaluate feasibility:
   - Does API provide required data?
   - Is data quality sufficient?
   - Are there deal-breaker limitations?
   - What's the cost at expected scale?

Provide working code I can run immediately.
Target language: [Python/JavaScript/etc.]
```

---

## Step 2A: Synthesize User Interviews

**Use in**: Any AI tool

```
I conducted [NUMBER] user interviews about [PROBLEM AREA].

Here are my raw notes from each interview:

**Interview 1**:
[PASTE NOTES]

**Interview 2**:
[PASTE NOTES]

[Continue for all interviews]

Synthesize these findings:

1. **Current workflow patterns**
   - How do most users approach this task?
   - What tools do they use?
   - How long does it take?

2. **Pain point themes** (ranked by frequency)
   - What problems came up most often?
   - How did users describe the pain?
   - Include verbatim quotes for top 3 pain points

3. **Quantified impact**
   - Time wasted: [X hours per week/month]
   - Money lost: [Y dollars]
   - Other consequences: [specific examples]

4. **Current workarounds**
   - What are they doing now to cope?
   - Why don't those solutions work?

5. **Willingness to change**
   - How motivated are they to solve this?
   - What would make them try a new solution?
   - Price sensitivity signals

6. **Decision**
   - Should I build this? (Yes/No/Need more data)
   - Reasoning based on findings
   - If yes, what's the minimum viable solution?

Format as markdown with clear sections.
```

---

## Step 2B: Synthesize Problem Research

**Use in**: Any AI tool

```
Based on the user voice research you did, organize findings:

1. **User segments** (who has this problem?)
   - Segment 1: [Description, example quotes]
   - Segment 2: [Description, example quotes]
   - Which segment is most underserved?

2. **Pain point themes** (ranked by frequency)
   - Theme 1: [Description, frequency, vivid quotes]
   - Theme 2: [Description, frequency, vivid quotes]
   - Theme 3: [Description, frequency, vivid quotes]

3. **Quantified impact** (from user posts)
   - Time wasted: [X hours per week/month from posts]
   - Money lost: [Y dollars from posts]
   - Specific consequences: [examples from users]

4. **Why current solutions fail**
   - Solution 1: [Why users reject it, quotes]
   - Solution 2: [Why users reject it, quotes]

5. **Our opportunity**
   - What gap can we fill that existing solutions don't?
   - Which user segment should we target first?
   - What's the minimum viable solution?

**Decision**: Build / Don't build / Need more data
**Reasoning**: [Based on voice of user data]

Format as markdown.
```

---

## Step 3: Generate PRD

**Use in**: Any AI tool

```
I've completed discovery research for my product idea. Help me write a PRD (Product Requirements Document) that an AI coding assistant (Cursor) can use to build the MVP.

**My Discovery Work**:

[PASTE YOUR MARKET RESEARCH FROM STEP 0]

[PASTE YOUR VALIDATION WORK FROM STEP 2 - interviews/research/experiment]

**Instructions**:

Using this template, generate a complete PRD:

# [Product Name] - Product Requirements Document

**Last Updated**: [Date]  
**Status**: Discovery Complete / Ready for Development

---

## Product Overview

**One-line description**:
[Specific: what it does + who uses it]

**Problem we're solving**:
[From discovery: specific user segment, specific problem, quantified impact]

**Solution approach**:
[How this solves the problem - high level, not implementation]

**Evidence**:
[What you learned - cite specific findings]
- User interviews: "[key finding with quote]"
- Market research: "[competitive gap we're filling]"
- Technical validation: "[feasibility confirmed]"

---

## Target Users

**Primary persona**:
- Who: [Specific segment from research, NOT "users"]
- Job-to-be-done: [What outcome they want]
- Current workflow: [How they do this today from interviews]
- Pain point: [Specific problem from research, with time/cost impact]
- Quote: "[Verbatim user quote that captures pain]"

---

## MVP Scope

### Core Features (Must Have for V1)

**Feature 1: [Name based on highest-value pain point]**
- What it does: [Specific capability]
- User value: [Time saved / problem solved - quantified]
- Success metric: [How we know it works]
- Priority: P0 (launch blocker)

**Feature 2: [Name based on second pain point]**
- What it does: [Specific capability]
- User value: [Why this matters]
- Success metric: [How we measure]
- Priority: P1 (launch blocker)

[Add 1-2 more core features if validated in research]

### Explicitly Out of Scope (V2+)

- [Feature mentioned by users but not validated enough]
  - Why deferred: [Not critical for MVP / complexity too high / can validate after]

---

## User Flows

**Primary flow** (happy path):
1. User starts at [entry point]
2. User [action]
3. System [behavior]
4. User sees [outcome]
5. Success state: [What indicates they got value]

**Edge cases**:
- If [error scenario] → System [behavior], User sees [message]

---

## Technical Requirements

**Platform**: [Web / Mobile / Both - based on user workflow from research]

**Performance requirements**:
- [Metric]: [Threshold from user expectations]
- [Metric]: [Threshold]

**Third-party services** (if known from technical validation):
- [API/Service]: [Purpose, why we need it]

**Compliance** (if applicable from market research):
- [Standard]: [Specific requirements]

---

## Success Metrics

**Primary metric** (North Star):
[Main indicator that product solves the problem]

**How we'll measure**:
- [Input metric]: [Target] - [How measured]
- [Adoption metric]: [Target] - [How measured]
- [Value metric]: [Target] - [How measured]

**Decision point**: [When we evaluate MVP success]

---

## Next Steps

1. Knowledge handoff: Create CONTEXT.md, CONSTRAINTS.md, .cursorrules
2. Infrastructure setup in Cursor (4-6 hours)
3. Build MVP features (based on prioritization above)
4. Beta test with [N] users from research
5. Measure success metrics
6. Iterate or pivot based on data

---

Based on the discovery data I provided:
- Fill in all brackets with specific information
- Be concrete, not generic
- Quote actual user findings where relevant
- Make technical requirements specific (not "fast" but "<2s load time")
- Ensure MVP scope is minimal but solves the core validated problem
```

---

## Usage Tips

1. **Always start with Step 0** - Market research orients everything else
2. **Copy entire prompts** - Don't skip sections, they're designed to get complete output
3. **Replace ALL [BRACKETED] sections** with your specifics before pasting
4. **Iterate if needed** - If output isn't specific enough, ask AI to "be more concrete" or "add more detail to [section]"
5. **Use web search** - For Steps 0, 1B especially, make sure your AI tool has web access enabled
6. **Save outputs** - Keep the AI's responses organized (market research, synthesis, PRD) for reference

---

## Time Budget

- Step 0: 30-60 min (market research)
- Step 1: 30 min (pick method + generate prompt)
- Step 2: 2-4 hours (execute + synthesize)
- Step 3: 1-2 hours (generate PRD + refine)

**Total: 4-8 hours from idea to structured PRD**