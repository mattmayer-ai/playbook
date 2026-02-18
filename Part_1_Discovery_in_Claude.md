# Part 1: Rapid Discovery in Claude

**Purpose**: Do just enough discovery to write a solid PRD before coding. Everything in this phase happens in Claude—conversational, AI-assisted, artifact-focused.

**Time**: 4-8 hours (not weeks)

**Output**: Structured PRD ready for Cursor consumption.

---

## Why Any Discovery At All

You need enough context to write a PRD that Cursor can execute against. Not full validation—that comes after MVP. Just enough to avoid building something obviously wrong.

**Bad**: "Build a productivity app" → Cursor has no direction  
**Good**: "Build a lesson planning tool that reduces teacher prep time from 2 hours to 15 minutes by automating standards alignment"

The difference is 4-8 hours of focused discovery with AI assistance.

---

## The Rapid Discovery Process

Three steps, 4-8 hours total:

1. **Pick Your Validation Method** (1 hour) - Choose based on what you need to know
2. **Execute Discovery** (2-5 hours) - AI-assisted research or quick interviews
3. **Write the PRD** (1-2 hours) - Package into structured format for Cursor

**Not included**: Full assumption mapping, extensive experiments, 697-complaint analysis. Those are for post-MVP validation.

---

## Step 1: Pick Your Validation Method (1 hour)

Choose ONE based on what you're uncertain about.

### Option A: User Interviews (if you have access to users)

**Use when**: You have a problem hypothesis but don't know if it's painful enough

**What to do**:
- Find 3-5 people who have the problem
- 30-minute calls each
- Ask: What's your current workflow? Where does it break? How much time/money does that cost?

**Time**: 3-4 hours (includes recruitment, calls, synthesis)

**Claude prompt**:
```
I'm building [product idea]. Help me create an interview script for 30-minute calls with [target users].

Focus on:
- Understanding their current workflow
- Identifying pain points
- Quantifying impact (time/cost)
- Testing willingness to change

Generate 10-12 questions that avoid leading them to my solution.
```

**Output**: 3-5 user quotes, pain point severity, current workarounds

### Option B: Industry Research (if you need market context)

**Use when**: You're entering unfamiliar domain and need to understand landscape

**What to do**:
- Use Claude with web search
- Research: market size, existing solutions, regulatory constraints, pricing
- Synthesize into competitive analysis

**Time**: 2-3 hours (AI-assisted research)

**Claude prompt**:
```
I'm building [product idea] in [industry]. Help me research:

1. Market landscape: Who are the key players? What do they offer?
2. Pricing: What do existing solutions cost? What do users pay?
3. Regulations: Are there compliance requirements I should know?
4. Gaps: What are users complaining about in existing solutions?

Use web search to find recent reviews, articles, and discussions.
Then synthesize findings into a competitive analysis.
```

**Output**: Competitive landscape, pricing benchmarks, regulatory requirements, market gaps

### Option C: Quick Experiment (if you need technical validation)

**Use when**: You're unsure if the technical approach will work

**What to do**:
- Build smallest possible test (1-3 hours)
- Example: If building AI tool, test prompt quality with 5-10 examples
- Example: If building integration, test API with sample data

**Time**: 2-4 hours (includes coding, testing)

**What to validate**:
- Can AI generate acceptable output quality?
- Does the API have required data?
- Is performance acceptable?

**Output**: Working prototype or negative result (both are valuable)

### Option D: Problem Research (if starting from scratch)

**Use when**: You have a vague idea but need to sharpen the problem statement

**What to do**:
- Use Claude to explore problem space
- Research forums, Reddit, Twitter for complaints
- Identify specific user segments and pain points

**Time**: 2-3 hours (AI-assisted research)

**Claude prompt**:
```
I think there's a problem in [domain] around [vague idea].

Help me:
1. Search for complaints, discussions, forum posts about this problem
2. Identify who specifically has this problem (not "users" but specific segments)
3. Find patterns in what they complain about
4. Estimate severity (how much time/money does this cost them?)

Synthesize findings into a specific problem statement:
- Who has the problem (specific segment)
- What they're trying to accomplish
- Why current solutions fail
- How much this costs them (time/money)
```

**Output**: Specific problem statement with evidence

---

## Step 2: Execute Discovery (2-5 hours)

### If You Chose User Interviews:

**Interview structure** (30 minutes each):

1. **Current workflow** (10 min)
   - "Walk me through the last time you [did this task]"
   - "What tools do you use?"
   - "How long does this typically take?"

2. **Pain points** (10 min)
   - "Where does this break down?"
   - "What's the most frustrating part?"
   - "Have you tried other solutions? Why didn't they work?"

3. **Quantify impact** (5 min)
   - "How much time does this problem cost you per week/month?"
   - "What happens if you don't solve this?"
   - "How much would you pay to fix this?"

4. **Solution reaction** (5 min)
   - "If there was a tool that [your solution], would you use it?"
   - "What would make you NOT use it?"

**Document findings in Claude**:
```
## User Interview Synthesis

**Interviews conducted**: 3-5 users
**Date**: [Date]

**Key findings**:

1. **Current workflow**: [How they do this today]
   - Quote: "[Verbatim user quote]"

2. **Pain point**: [Specific problem]
   - Severity: [Time/cost impact]
   - Quote: "[Verbatim user quote]"

3. **Current workarounds**: [What they do now]
   - Why it fails: [Specific reason]

4. **Willingness to change**: [High/Medium/Low]
   - Evidence: [What they said]

**Decision**: Build / Don't build / Need more validation
**Reasoning**: [Based on findings]
```

### If You Chose Industry Research:

**Research checklist**:

- [ ] Identify 3-5 existing solutions
- [ ] Find pricing for each (free tier, paid plans)
- [ ] Read recent reviews (G2, Capterra, Reddit)
- [ ] Check regulatory requirements (if applicable)
- [ ] Identify gaps in existing solutions

**Claude-assisted research**:
```
Research [product category] tools:

1. Who are the top 5 solutions?
2. What do they cost? (use web search to find pricing pages)
3. What are users complaining about? (search for "[tool name] review" on Reddit, G2)
4. What features are missing? (look for "I wish [tool] had...")
5. Are there regulatory requirements? (HIPAA, GDPR, etc.)

Synthesize into competitive analysis table:
| Tool | Price | Strengths | Weaknesses | Gap We Can Fill |
```

**Output format**:
```markdown
## Industry Research Summary

**Market**: [Size, growth rate]
**Existing solutions**: [3-5 competitors]

**Competitive Analysis**:

| Tool | Pricing | Strengths | Weaknesses | Our Opportunity |
|------|---------|-----------|------------|-----------------|
| [Tool 1] | $X/mo | [What they do well] | [What users complain about] | [Gap] |
| [Tool 2] | $Y/mo | [Strengths] | [Weaknesses] | [Gap] |

**Regulatory constraints**: [If applicable]
**Pricing benchmark**: [What market will pay]
**Our angle**: [How we differentiate]
```

### If You Chose Quick Experiment:

**Example: Testing AI output quality**

```python
# test_ai_quality.py
# 1-2 hours to validate if AI can generate acceptable output

import anthropic

client = anthropic.Anthropic()

test_cases = [
    "Generate lesson plan for 4th grade math: multiplication tables",
    "Generate lesson plan for 6th grade science: photosynthesis",
    # Add 5-10 representative examples
]

results = []
for test in test_cases:
    response = client.messages.create(
        model="claude-sonnet-4-20250514",
        max_tokens=1000,
        messages=[{"role": "user", "content": test}]
    )
    
    results.append({
        "input": test,
        "output": response.content[0].text,
        "acceptable": True  # Manual review: Does this meet quality bar?
    })

# Review results
acceptable_rate = sum(r["acceptable"] for r in results) / len(results)
print(f"Acceptance rate: {acceptable_rate * 100}%")

# Decision
if acceptable_rate >= 0.7:
    print("✓ AI quality sufficient - proceed to build")
else:
    print("✗ AI quality insufficient - need better prompts or different approach")
```

**Document findings**:
```markdown
## Technical Validation: AI Output Quality

**Test date**: [Date]
**Test cases**: 10 examples (representative use cases)

**Results**:
- Acceptable quality: 8/10 (80%)
- Issues found: [Specific problems]
- Workarounds: [How to improve prompts]

**Decision**: Proceed / Need improvement / Try different approach
**Reasoning**: [Based on test results]
```

### If You Chose Problem Research:

**Research prompt for Claude**:
```
Search for discussions about [problem area] in [domain]:

1. Find Reddit threads, forum posts, Twitter discussions
2. Look for complaints about current solutions
3. Identify patterns in what people say
4. Find specific examples of pain (time wasted, money lost, frustration)

Focus on finding:
- Who specifically has this problem (job titles, contexts)
- How they describe it (their language, not industry jargon)
- What they've tried (existing solutions, workarounds)
- How severe it is (quantifiable impact)

Synthesize into problem statement.
```

**Output**:
```markdown
## Problem Research Summary

**Problem area**: [General domain]
**Sources**: Reddit ([subreddit]), Forums ([site]), Twitter

**Who has this problem**: [Specific user segments]
- Example: "Elementary teachers preparing lesson plans"
- NOT: "Educators" (too vague)

**How they describe it**: [Verbatim quotes]
- "[User quote from Reddit]"
- "[User quote from forum]"

**Current solutions and why they fail**:
- [Solution 1]: [Why it doesn't work]
- [Solution 2]: [Why it doesn't work]

**Quantified impact**:
- Time: [X hours per week/month]
- Money: [Y dollars lost/wasted]
- Frustration: [Specific consequences]

**Our angle**: [Specific approach to solve this]
```

---

## Step 3: Write the PRD (1-2 hours)

Take your discovery output and structure it for Cursor.

### Rapid PRD Template

```markdown
# [Product Name] - Product Requirements Document

**Last Updated**: [Date]  
**Status**: Discovery Complete / Ready for Development

---

## Product Overview

**One-line description**:
[What this product does and who uses it]

**Problem we're solving**:
[From your discovery - specific user segment, specific problem, quantified impact]

**Solution approach**:
[How this product solves the problem - high level]

**Evidence**:
[What you learned in discovery]
- If user interviews: "3/5 users spend 2+ hours per week on this problem"
- If industry research: "Existing solutions cost $50-100/month but don't solve X"
- If experiment: "AI generates acceptable output in 80% of test cases"
- If problem research: "200+ complaints on Reddit about this exact issue"

---

## Target Users

**Primary persona**:
- Who: [Specific segment, not "users"]
- Job-to-be-done: [What they're trying to accomplish]
- Current workflow: [How they do this today]
- Pain point: [What breaks, costs time/money]

---

## MVP Scope

### Core Features (Must Have)

**Feature 1: [Name]**
- What it does: [Specific capability]
- User value: [Why this matters - time saved, problem solved]
- Success metric: [How we measure if it works]

**Feature 2: [Name]**
- What it does: [Specific capability]
- User value: [Why this matters]
- Success metric: [How we measure]

### Explicitly Out of Scope (V2+)

- [Feature we're deferring]: [Why - not validated, too complex, not critical]

---

## User Flows

**Primary flow**:
1. User starts at [screen/state]
2. User does [action]
3. System responds [behavior]
4. User sees [outcome]

**Edge cases**:
- If [error], then [behavior]
- If [condition], then [behavior]

---

## Technical Requirements

**Platform**: Web / Mobile / Both

**Performance**:
- [Requirement]: [Threshold]
  Example: Page load <2s, API response <500ms

**Third-party services** (if known):
- [Service]: [Purpose]
  Example: OpenAI API for text generation

**Compliance** (if applicable):
- [Standard]: [Specific requirement]
  Example: HIPAA - no PHI in logs

---

## Success Metrics

**Primary metric**: [Main indicator of success]
Example: Reduces prep time from 2 hours to 15 minutes

**How we'll measure**:
- [Metric]: [Target]
- [Metric]: [Target]

---

## Open Questions

1. [Question requiring decision]
2. [Question requiring research]

---

## Next Steps

1. Create knowledge handoff package (CONTEXT.md, CONSTRAINTS.md, .cursorrules)
2. Set up infrastructure in Cursor
3. Build MVP features
4. Test with 5-10 users
5. Iterate based on feedback
```

### Use Claude to Generate PRD

**Prompt**:
```
Based on this discovery work:

[Paste your interview synthesis / research summary / experiment results]

Generate a PRD using this template:

[Paste rapid PRD template]

Make it specific and actionable. Focus on what Cursor needs to know to start building.
Include:
- Specific user segment (not "users")
- Quantified problem (time/cost)
- Clear MVP scope
- Success metrics
```

---

## Summary: Rapid Discovery (4-8 hours)

**What you produce**:
1. Discovery output (2-5 hours): User interviews OR industry research OR quick experiment OR problem research
2. Structured PRD (1-2 hours): Ready for Cursor consumption

**Total time**: 4-8 hours (not weeks)

**Decision**: After these 4-8 hours, you have enough to start building. Full validation comes after MVP, not before.

**When to invest more time**:
- Regulated industry (healthcare, finance) - add 2-4 hours for compliance research
- Unfamiliar domain - add 2-3 hours for market landscape research
- High technical risk - add 2-4 hours for proof-of-concept

**When 4-8 hours is enough**:
- You have domain expertise
- Problem is clear, solution is uncertain
- You can test with real users post-MVP
- Risk tolerance is high (startup, side project)

---

**Next**: [Part 2: Knowledge Handoff (Claude → Cursor)](./Part_2_Knowledge_Handoff.md)