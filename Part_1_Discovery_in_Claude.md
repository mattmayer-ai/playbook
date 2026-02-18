# Part 1: Rapid Discovery with AI 

**Purpose**: Do just enough discovery to write a solid PRD before coding. Use any AI tool (Claude, ChatGPT, Perplexity, etc.) with the copy-paste prompts provided.

**Time**: 4-8 hours total

**Output**: Structured PRD ready for Cursor consumption

**What's included**: Ready-to-use prompts for each step—just fill in your specifics and paste into your AI tool of choice.

---

## Why Any Discovery At All

You need enough context to write a PRD that Cursor can execute against. Not full validation—that comes after MVP. Just enough to avoid building something obviously wrong.

**Bad**: "Build a productivity app" → Cursor has no direction  
**Good**: "Build a lesson planning tool that reduces teacher prep time from 2 hours to 15 minutes by automating standards alignment"

The difference is 4-8 hours of focused discovery with AI assistance.

---

## The Rapid Discovery Process

Four steps, 4-8 hours total:

0. **AI-Assisted Market Research** (30-60 min) - ALWAYS start here - understand the landscape
1. **Pick Your Validation Method** (30 min) - Choose based on what market research revealed
2. **Execute Discovery** (2-4 hours) - Follow your chosen method with AI assistance
3. **Generate PRD** (1-2 hours) - AI transforms findings into structured PRD

**Copy-paste prompts provided for every step.**

**Not included**: Full assumption mapping, extensive experiments, 697-complaint analysis. Those are for post-MVP validation.

---

## Step 0: AI-Assisted Market Research (30-60 min)

**START HERE EVERY TIME.** Before you pick a validation method, get AI to map the landscape.

This step uses web search heavily. Use Claude with web search, ChatGPT with browsing, or Perplexity.

### What You're Learning

- Who are the existing players?
- What do they cost?
- What are users complaining about?
- What gaps exist?
- Are there regulatory constraints?

### Copy-Paste Prompt (use in Claude, ChatGPT, etc.)

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

### Example Output You'll Get

```markdown
## Market Research: Lesson Planning Tools

### Existing Solutions

| Tool | Pricing | Strengths | User Complaints | Our Gap |
|------|---------|-----------|-----------------|---------|
| Planbook | $12/mo | Simple, clean UI | "Takes too long to align to standards" | Automated standards alignment |
| Common Curriculum | $15/mo | Standards library | "Not personalized to my teaching style" | AI personalization |
| Teachers Pay Teachers | Free-$10/item | Huge content library | "Hit or miss quality, takes time to find good stuff" | AI-curated + quality control |

### Common User Complaints (from Reddit r/Teachers, G2)
- "Still takes 1-2 hours per lesson to align to standards"
- "Can't easily adapt lessons for different learning levels"
- "Too many clicks to get to what I need"

### Identified Gaps
1. No tool automates standards alignment (all manual)
2. No AI personalization based on teaching style
3. No tools optimize for time reduction (focus on content quality)

### Regulatory Constraints
- FERPA compliance (if storing student data)
- District approval processes vary

### Pricing Benchmark
- Entry: $10-15/month individual
- School/district: $500-2000/year
- Freemium possible for user acquisition
```

### What This Tells You

After 30-60 minutes, you know:
- **Whether your idea already exists** (if yes, what gap you'll fill)
- **What users are willing to pay** (pricing benchmark)
- **What the real pain points are** (from complaints, not assumptions)
- **What validation method to use next** (interviews? experiment? problem research?)

### Decision Point

Based on market research:

**If competitors exist but users complain** → Proceed to Step 1 (pick validation method)  
**If market is saturated and users are happy** → Consider different idea  
**If no competitors exist** → Validate the problem is real (could be no competitors because no one wants this)

---

## Step 1: Pick Your Validation Method (30 min)

Now that you understand the market, choose ONE validation method based on what you're uncertain about.

Choose ONE based on what you're uncertain about.

### Option A: User Interviews (if you have access to users)

**Use when**: You have a problem hypothesis but don't know if it's painful enough

**What to do**:
- Find 3-5 people who have the problem
- 30-minute calls each
- Ask: What's your current workflow? Where does it break? How much time/money does that cost?

**Time**: 3-4 hours (includes recruitment, calls, synthesis)

**Copy-Paste Prompt**:
```
I'm building [YOUR PRODUCT IDEA - 1-2 sentences].

Target users: [WHO - e.g., "elementary teachers", "construction contractors", "healthcare administrators"]

Problem I think they have: [PROBLEM - e.g., "spend too much time on lesson planning", "lose bids due to slow estimation"]

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

**Output**: Interview script you can use immediately

### Option B: Deep Problem Research (if you need user voice)

**Use when**: Market research shows complaints exist, but you need deeper understanding of HOW users describe the problem

**What to do**:
- Use AI to search forums, Reddit, Twitter for actual user complaints
- Analyze language patterns (how do they describe the problem?)
- Identify specific user segments
- Quantify severity from their words

**Time**: 2-3 hours (AI-assisted research)

**Copy-Paste Prompt**:
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

**Output**: User voice analysis with verbatim quotes, pain patterns, severity data

### Option C: Quick Technical Experiment (if you need feasibility validation)

**Use when**: You're unsure if the technical approach will actually work

**What to do**:
- Build smallest possible test (1-3 hours of coding)
- Example: If building AI tool, test prompt quality with 5-10 examples
- Example: If building integration, test API with sample data
- Example: If building automation, test with manual process first

**Time**: 2-4 hours (includes coding, testing, analysis)

**What to validate**:
- Can AI generate acceptable output quality?
- Does the API have required data/endpoints?
- Is performance acceptable for user experience?
- Are there blockers we didn't anticipate?

**Copy-Paste Prompt (for AI quality testing)**:
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

**Copy-Paste Prompt (for API integration testing)**:
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

**Output**: Working prototype OR evidence that approach won't work (both are valuable)

---

## Step 2: Execute Discovery (2-4 hours)

### If You Chose User Interviews:

**After conducting 3-5 interviews**, use AI to synthesize findings.

**Copy-Paste Synthesis Prompt**:
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

**Example Output You'll Get**:
```markdown
## User Interview Synthesis

**Interviews conducted**: 5 elementary teachers
**Date**: February 2026

**Key findings**:

1. **Current workflow**: Teachers spend 1.5-2 hours per lesson plan
   - Quote: "I spend my Sunday afternoons planning the whole week"
   - Tools: Google Docs, Pinterest, Teachers Pay Teachers
   - Average time: 90 minutes per lesson

2. **Top pain points**:
   - **Standards alignment takes forever** (5/5 mentioned)
     - Quote: "I have to cross-reference 3 different documents to make sure I'm hitting the right standards"
   - **Differentiation is time-consuming** (4/5 mentioned)
     - Quote: "I have kids reading at grade 1 and grade 6 level. Making versions of the same lesson for each takes hours"

3. **Quantified impact**:
   - Time: 8-10 hours per week on lesson planning
   - Personal cost: Weekend time, evening work
   - Consequence: "I'm exhausted and don't have time for my own kids"

4. **Current workarounds**:
   - Buy pre-made lesson plans (but still need to customize)
   - Reuse last year's plans (but standards change)
   - Share with colleagues (but they teach different grade levels)

5. **Willingness to change**: HIGH
   - 5/5 would try a tool that cuts planning time in half
   - 4/5 said they'd pay $15-20/month
   - Main concern: "Will it actually save time or just be another tool I have to learn?"

**Decision**: Build
**Reasoning**: Clear, painful problem (8-10 hrs/week wasted). Users willing to pay. Standards alignment is the highest-value feature to build first.
**MVP**: Automated standards alignment for common lesson structures. Defer differentiation to V2.
```

### If You Chose Deep Problem Research:

Use the AI to analyze and organize all the forum/Reddit posts it found.

**Copy-Paste Synthesis Prompt**:
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

### If You Chose Quick Technical Experiment:

After running your test code (from the prompt earlier), analyze results.

**Example Analysis** (AI quality test):
```markdown
## Technical Validation: AI Lesson Plan Generation

**Test date**: February 2026
**Test cases**: 10 lesson plans (grades 3-6, math and science)
**Model tested**: Claude Sonnet 4

**Results**:
- Acceptable quality: 8/10 (80%)
- Too generic: 2/10
- Standards alignment: 9/10 accurate
- Time to generate: <30 seconds per plan

**Issues found**:
- Needs better prompts for subject-specific vocabulary
- Sometimes misses grade-appropriate complexity

**Workarounds identified**:
- Add grade-level examples to prompts
- Include subject-specific context

**Decision**: Proceed - 80% quality is sufficient for MVP
**Reasoning**: Quality bar met. Identified prompt improvements. Speed is excellent.
```

If test fails (quality <70%), document what failed and why, then decide: improve prompts, try different model, or change approach.

---

## Step 3: Write the PRD (1-2 hours)

Take your discovery output and structure it for Cursor.

### Copy-Paste PRD Generation Prompt

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
- [Feature that's nice-to-have]
  - Why deferred: [Reasoning]

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
- If [edge case] → System [fallback behavior]

---

## Technical Requirements

**Platform**: [Web / Mobile / Both - based on user workflow from research]

**Performance requirements**:
- [Metric]: [Threshold from user expectations]
  Example: "Generate lesson plan in <30 seconds" (based on interview feedback)
- [Metric]: [Threshold]

**Third-party services** (if known from technical validation):
- [API/Service]: [Purpose, why we need it]
  Example: "Anthropic Claude API for lesson plan generation (validated 80% quality)"

**Data requirements**:
- What data we need to store: [From user workflows]
- What data we need to source: [From technical validation]

**Compliance** (if applicable from market research):
- [Standard]: [Specific requirements]
  Example: "FERPA compliance - no student PII stored, only teacher accounts"

---

## Success Metrics

**Primary metric** (North Star):
[Main indicator that product solves the problem]
Example: "Reduce lesson planning time from 90 minutes to <30 minutes"

**How we'll measure**:
- [Input metric]: [Target] - [How measured]
  Example: "Time from start to download: <30 min - tracked in app"
- [Adoption metric]: [Target] - [How measured]
  Example: "70% of users complete their first lesson plan - analytics event"
- [Value metric]: [Target] - [How measured]
  Example: "80% report time savings - post-use survey"

**Decision point**: [When we evaluate MVP success]
Example: "After 50 teachers use the tool - if <60% report time savings, pivot approach"

---

## Open Questions

[Only include if there are genuine blockers]

1. [Question that requires decision before building]
   - Context: [Why this matters]
   - Blocking: [Yes/No]
   - Decision needed by: [When]

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

### What You'll Get

A complete, structured PRD that Cursor can use to understand:
- Exactly what problem you're solving (with evidence)
- Who you're solving it for (with quotes)
- What to build first (prioritized features)
- How to measure success (specific metrics)
- What NOT to build yet (out of scope)

```markdown
---

## Summary: Rapid Discovery (4-8 hours)

**What you produce**:
0. Market research (30-60 min): Competitive landscape, user complaints, pricing, gaps
1. Validation method choice (30 min): Pick ONE based on what market research revealed
2. Discovery execution (2-4 hours): User interviews OR problem research OR technical experiment  
3. Structured PRD (1-2 hours): Ready for Cursor consumption with AI assistance

**Total time**: 4-8 hours (not weeks)

**Tools you used**: Any conversational AI (Claude, ChatGPT, etc.) with web search capability

**Decision**: After these 4-8 hours, you have enough to start building. Full validation comes after MVP, not before.

### When to invest more time:

- **Regulated industry** (healthcare, finance) - add 2-4 hours for compliance deep-dive
- **Unfamiliar domain** - add 2-3 hours for additional market research
- **High technical risk** - add 2-4 hours for more extensive proof-of-concept
- **Enterprise sales** - add 3-4 hours for buyer persona research

### When 4-8 hours is enough:

- You have domain expertise
- Problem is clear from market research
- You can test with real users post-MVP
- Risk tolerance is high (startup, side project)
- You're validating solution approach, not problem existence

### Red flags that mean "don't build":

- Market research shows no complaints about existing solutions
- Users in interviews can't quantify the problem
- Technical experiment shows fundamental blockers
- Regulatory requirements are prohibitively complex
- Competitive analysis shows saturated market with happy users

### Green lights that mean "build the MVP":

- 3+ users articulate same pain point
- Quantified impact (time/money) is significant  
- Technical feasibility validated
- Clear gap in competitive landscape
- Users express willingness to pay

---

**Next**: [Part 2: Knowledge Handoff (Claude → Cursor)](./Part_2_Knowledge_Handoff.md)
