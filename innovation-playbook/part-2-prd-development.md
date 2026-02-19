# Part 2: PRD Development

**Purpose**: Transform Discovery Insights Report into implementation-ready PRD with prioritized features, identified risks, clear constraints, and success metrics.

**Time**: 2-3 hours

**Input**: Discovery Insights Report from Part 1

**Output**: Complete PRD ready for development

***

### Why PRD Development Matters

**Part 1 gave you**: Evidence-backed direction ("build this, here's why")\
**Part 2 gives you**: Implementation specification ("here's exactly what to build, in what order, with what constraints, and how we'll know it worked")

**Without this step**: "Build a site coordinator dashboard" → Direction but no boundaries\
**With this step**: "Build dashboard with 3 P0 features (patient matching, contact list, diversity tracking), defer analytics to V2, must integrate with EHR API, success = 50% time savings"

***

### Prototype vs. MVP vs. V2

Before prioritizing features, define what you're building:

<table><thead><tr><th width="114">Type</th><th>Purpose</th><th width="141">Timeline</th><th>Scope</th><th>Quality Bar</th></tr></thead><tbody><tr><td><strong>Prototype</strong></td><td>Prove concept, win buy-in, hiring challenge</td><td>Days-weeks</td><td>1-3 core workflows</td><td>Demo-quality, may have hardcoded data</td></tr><tr><td><strong>MVP</strong></td><td>Validate with real users, gather data</td><td>Weeks-months</td><td>Core job-to-be-done complete</td><td>Production-ready, real data, basic error handling</td></tr><tr><td><strong>V2+</strong></td><td>Scale, optimize, expand</td><td>Months+</td><td>Additional features, optimizations</td><td>Full production quality</td></tr></tbody></table>

***

### Component 1: Feature Prioritization (30 min)

#### Priority Levels

**P0 (Launch Blocker)**: Without this, product doesn't solve core problem

* User can't complete primary job-to-be-done
* Evidence from research says this is critical pain point
* Example: "Patient matching algorithm" - without it, coordinator dashboard is useless

**P1 (High Priority)**: Significantly improves value but product minimally viable without it

* Addresses secondary pain point from research
* Makes product more usable but not essential
* Example: "Diversity tracking dashboard" - improves outcome but matching is core job

**V2 (Deferred)**: Valuable but can validate need after launch

* Mentioned by users but not urgent
* Adds complexity vs value at this stage
* Can build after core validated
* Example: "Predictive site performance" - nice analytics, not critical

#### Decision Tree

```
Does removing this break the core job-to-be-done?
├─ YES → P0
└─ NO → Did 3+ users cite this as painful?
    ├─ YES → P1
    └─ NO → Is this technically complex/risky?
        ├─ YES → V2 (validate core first)
        └─ NO → Can we measure if this works?
            ├─ YES → P1 (if capacity allows)
            └─ NO → V2 (defer until measurable)
```

#### Copy-Paste Prompt

```
Based on Discovery Insights Report, prioritize features:

[PASTE RECOMMENDED DIRECTION from Part 1 - Core Capabilities section]
[PASTE KEY INSIGHTS from Part 1 - what users said was painful]

For each capability/feature:

1. **Feature name**: [Specific capability]
2. **User problem it solves**: [From research]
3. **Evidence**: [How many users mentioned, severity]
4. **Priority**:
   - P0 if: Core job breaks without it
   - P1 if: Significantly improves value but not essential
   - V2 if: Nice-to-have or needs validation first
5. **Reasoning**: [Why this priority]

Create feature priority table:

| Feature | User Value | Evidence | Complexity | Priority | Reasoning |
|---------|------------|----------|------------|----------|-----------|
| [Name] | [What it solves] | [N users, severity] | [Low/Med/High] | P0/P1/V2 | [Why] |

Rules:
- Limit P0 to 3-5 features max (if everything is P0, nothing is)
- P1 features should be completable in 1-2 sprints each
- V2 features need clear "why defer" reasoning
```

***

### Component 2: Risk Identification & Mitigation (30 min)

#### Risk Categories

**Technical**: Can we build this?

* API availability, integration complexity, performance
* Example: "EHR integration may not provide real-time data"

**Adoption**: Will users actually use this?

* Workflow changes, learning curve, competing priorities
* Example: "Coordinators may not trust AI confidence scores"

**Business**: Does this align with constraints?

* Regulatory compliance, vendor relationships, budget
* Example: "HIPAA requirements may limit data access"

**Data**: Do we have the data we need?

* Data quality, availability, privacy constraints
* Example: "Patient eligibility data may be incomplete"

#### Copy-Paste Prompt

```
Based on Discovery Insights Report and features, identify risks:

[PASTE RECOMMENDED DIRECTION from Part 1]
[PASTE ASSUMPTIONS MATRIX from Part 1 - especially "TO VALIDATE" items]
[PASTE PRIORITIZED FEATURES from Component 1]

For each risk:

1. **Risk description**: [What could go wrong]
2. **Category**: Technical / Adoption / Business / Data
3. **Likelihood**: High / Medium / Low
4. **Impact if occurs**: High / Medium / Low
5. **Risk level**: [High/Medium/Low]
6. **Mitigation strategy**: [How to reduce likelihood or impact]
7. **Contingency plan**: [What if risk materializes]

Create risk table:

| Risk | Category | Likelihood | Impact | Level | Mitigation | Contingency |
|------|----------|------------|--------|-------|------------|-------------|
| [Description] | [Type] | [L/M/H] | [L/M/H] | [L/M/H] | [Prevent] | [If happens] |

Focus on:
- Assumptions marked "TO VALIDATE" (these are risks)
- Technical dependencies (APIs, integrations)
- User adoption barriers (workflow changes)
- Regulatory/compliance requirements
```

***

### Component 3: Constraints Analysis (20 min)

#### Constraint Types

**Technical**: Platform, APIs, performance thresholds\
**Regulatory**: HIPAA, GDPR, compliance requirements\
**Business**: Budget, vendor relationships, strategic alignment\
**Time**: Deadlines, dependencies, seasonal factors\
**Team**: Capacity, skills, timezone\
**User**: Workflow integration, change tolerance, existing tools

#### Copy-Paste Prompt

```
Map all constraints:

[PASTE PROBLEM REFRAME from Part 1 - includes current workflow]
[PASTE RECOMMENDED DIRECTION from Part 1]
[PASTE ASSUMPTIONS MATRIX from Part 1]

For each constraint type:

## Technical Constraints
- Platform: [What systems must we integrate with, work on]
- Performance: [Response time, load requirements]
- Infrastructure: [Existing tech stack we must use]
- APIs/Services: [Third-party dependencies, rate limits]

## Regulatory Constraints
- Compliance: [HIPAA, GDPR, industry-specific]
- Data handling: [What can/cannot be stored, logged, transmitted]
- Audit: [What must be tracked]

## Business Constraints
- Budget: [Available resources]
- Timeline: [Hard deadlines, why they exist]
- Vendor: [Existing partnerships we must use/avoid]
- Strategic: [Company direction that shapes approach]

## Time Constraints
- Deadline: [When, why]
- Dependencies: [What must happen first]
- Seasonal: [Time-sensitive factors]

## Team Constraints
- Capacity: [Available hours, people]
- Skills: [Expertise exists, gaps]
- Location: [Timezone, remote/co-located]

## User Constraints
- Workflow: [Can't disrupt existing process]
- Tools: [Already using X systems]
- Change tolerance: [How much learning acceptable]

For each:
- **Why it matters**: [Impact on product]
- **How it shapes solution**: [What we must/can't do]
```

***

### Component 4: Success Metrics Framework (30 min)

#### Metric Levels

**Input Metrics** (What users do): Usage, adoption, engagement\
**Output Metrics** (What product delivers): Efficiency, quality, outcomes\
**Outcome Metrics** (Business impact): Revenue, cost savings, strategic goals

#### Copy-Paste Prompt

```
Define success metrics based on hypothesis and features:

[PASTE HYPOTHESIS from Part 1 - Success Criteria section]
[PASTE PRIORITIZED FEATURES from Component 1]

For each P0 and P1 feature:

**Feature**: [Name]
**Input metric** (usage): [What behavior indicates adoption]
- How measured: [Tool, event]
- Target: [Threshold]

**Output metric** (value): [What product produces]
- How measured: [Calculation]
- Target: [Threshold]

Then synthesize:

## Success Metrics

**Primary Metric** (North Star):
[ONE metric indicating overall success]
- Target: [Specific threshold]
- Timeline: [When we measure]

**Input Metrics** (Leading Indicators):
1. [Metric]: [Target] - [How measured]
2. [Metric]: [Target] - [How measured]

**Output Metrics** (Product Value):
1. [Metric]: [Target] - [How measured]
2. [Metric]: [Target] - [How measured]

**Outcome Metrics** (Business Impact):
1. [Metric]: [Target] - [How measured]

**Decision Point**:
After [N] weeks/users, if [metric] below [threshold], then [action].
```

***

### Component 5: MVP Boundary Decisions (20 min)

#### Include If

* P0 feature (core job broken without it)
* Validates critical assumption from research
* Users specifically mentioned need
* Required for measuring success metrics

#### Exclude If

* Nice-to-have (P1/V2)
* Adds complexity without validated need
* Can be added after usage data
* Requires significant technical risk

#### Copy-Paste Prompt

```
Define MVP boundaries:

[PASTE PRIORITIZED FEATURES from Component 1]
[PASTE RISK ANALYSIS from Component 2]
[PASTE CONSTRAINTS from Component 3]

## In Scope (Must Build)
List P0 features and P1 features that:
- Directly support P0 functionality
- Low complexity + high value
- Required to measure success metrics

**Feature**: [Name]
- **Why included**: [Validates X / Enables Y / Needed for metric Z]
- **Definition of Done**: [What "complete" looks like]

## Out of Scope (V2+)
**Feature**: [Name]
- **Why deferred**: [Can validate after launch / High complexity / Nice-to-have]
- **When to revisit**: [After N users / When metric X achieved]

## Edge Cases
**Must Handle in MVP**:
- [Edge case]: [Why critical]

**Defer to V2**:
- [Edge case]: [Why acceptable to skip]
```

***

### Component 6: Feature Trade-Offs (20 min)

#### Trade-Off Categories

**Scope vs. Time**: Feature richness vs. speed to market\
**Quality vs. Speed**: Production polish vs. rapid validation\
**Flexibility vs. Simplicity**: Configurable vs. opinionated\
**Build vs. Buy**: Custom development vs. third-party integration

#### Copy-Paste Prompt

```
Document trade-off decisions:

[PASTE MVP SCOPE from Component 5]
[PASTE PRIORITIZED FEATURES from Component 1]
[PASTE CONSTRAINTS from Component 3]

For each major decision:

**Decision**: [What we chose]
**Alternative**: [What we didn't choose]
**Trade-off**: [What we gained vs. gave up]
**Reasoning**: [Why this choice, based on evidence/constraints]
**Revisit condition**: [When we might reverse]

Categories:
1. Scope (features included vs. excluded)
2. Technical (architecture, platform, tools)
3. UX (simplicity vs. flexibility)
4. Timeline (MVP speed vs. completeness)
```

***

### Final PRD Compilation (30 min)

#### Copy-Paste Prompt

```
Compile all PRD components:

[PASTE DISCOVERY INSIGHTS REPORT from Part 1]
[PASTE PRIORITIZED FEATURES from Component 1]
[PASTE RISK ANALYSIS from Component 2]
[PASTE CONSTRAINTS from Component 3]
[PASTE SUCCESS METRICS from Component 4]
[PASTE MVP SCOPE from Component 5]
[PASTE TRADE-OFFS from Component 6]

Generate complete PRD:

# [Product Name] - Product Requirements Document

**Version**: 1.0
**Last Updated**: [Date]
**Status**: Ready for Development
**Type**: [Prototype / MVP / V2]

## Executive Summary
[Problem, solution, success criteria, timeline/scope]

## Product Overview
[One-line, problem statement, target users, evidence]

## Features & Prioritization
[P0, P1, V2 tables]

## Risk Analysis
[Risk table with mitigations]

## Constraints
[All constraint types + how they shape solution]

## Success Metrics
[North Star, input/output/outcome, decision point]

## MVP Scope
[In scope, out of scope with reasoning, edge cases]

## Key Trade-Offs
[Major decisions with reasoning]

## User Flows
[Primary flow for P0 features]

## Technical Architecture
[Platform, services, data model, integrations]

## Open Questions & Validation Plan
[Must validate before launch, stakeholder questions]

## Appendices
[Link to Discovery Insights Report]

Format as professional markdown.
```

***

### Summary: PRD Development (2-3 hours)

**What you produce**:

1. Feature Prioritization (30 min): P0, P1, V2 with decision framework
2. Risk Analysis (30 min): Technical, Adoption, Business, Data risks with mitigations
3. Constraints Analysis (20 min): 6 types that shape solution
4. Success Metrics (30 min): North Star, input/output/outcome, decision point
5. MVP Boundaries (20 min): In scope vs. out of scope with reasoning
6. Trade-Offs (20 min): Major decisions with rationale
7. Final PRD (30 min): Complete, implementation-ready document

**Total time**: 2-3 hours

**Input**: Discovery Insights Report from Part 1

**Output**: Complete PRD ready for Knowledge Handoff (Part 3)

***

**Next**: Part 3: Knowledge Handoff
