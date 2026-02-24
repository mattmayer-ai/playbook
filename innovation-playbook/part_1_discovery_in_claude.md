# Part 2: PRD Development

**Purpose:** Transform Discovery Insights Report into implementation-ready PRD with prioritized features, identified risks, clear constraints, and success metrics.

**Time:** 2-3 hours

**Input:** Discovery Insights Report from Part 1

**Output:** Complete PRD ready for development

***

### Why PRD Development Matters

**Part 1 gave you:** Evidence-backed direction ("here's the problem, here's our hypothesis")

**Part 2 gives you:** Implementation specification ("here's exactly what to build, in what order, with what constraints, and how we'll know it worked")

<table><thead><tr><th width="314">Without this step</th><th>With this step</th></tr></thead><tbody><tr><td>"Build a coordinator dashboard"</td><td>"Build dashboard with 3 P0 features (patient matching, contact list, diversity tracking), defer analytics to V2, must integrate with EHR API, success = 50% time savings"</td></tr></tbody></table>

***

### Prototype vs. MVP vs. V2

Before prioritizing features, define what you're building:

<table><thead><tr><th width="133">Type</th><th>Purpose</th><th>Scope</th><th>Quality Bar</th></tr></thead><tbody><tr><td><strong>Prototype</strong></td><td>Test hypothesis with users</td><td>Core flow only</td><td>Works for demo, not production</td></tr><tr><td><strong>MVP</strong></td><td>Validate with real usage</td><td>Minimum to deliver value</td><td>Production-ready, limited features</td></tr><tr><td><strong>V2</strong></td><td>Scale based on learnings</td><td>Expanded features</td><td>Full polish</td></tr></tbody></table>

***

### Component 1: Feature Prioritization (30 min)

#### Priority Levels

<table><thead><tr><th width="161">Level</th><th width="184">Definition</th><th>Criteria</th></tr></thead><tbody><tr><td><strong>P0</strong></td><td>Launch blocker</td><td>User can't complete primary job without this</td></tr><tr><td><strong>P1</strong></td><td>High priority</td><td>Significantly improves value but minimally viable without</td></tr><tr><td><strong>V2</strong></td><td>Deferred</td><td>Valuable but can validate need after launch</td></tr></tbody></table>

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

Rules:
- Limit P0 to 3-5 features max (if everything is P0, nothing is)
- P1 features should be completable in 1-2 sprints each
- V2 features need clear "why defer" reasoning
```

***

### Component 2: Risk Identification & Mitigation (30 min)

#### Risk Categories

<table><thead><tr><th width="167">Category</th><th>Description</th><th>Example</th></tr></thead><tbody><tr><td><strong>Technical</strong></td><td>Can we build this?</td><td>"EHR integration may not provide real-time data"</td></tr><tr><td><strong>Adoption</strong></td><td>Will users actually use this?</td><td>"Coordinators may not trust AI confidence scores"</td></tr><tr><td><strong>Business</strong></td><td>Does this align with constraints?</td><td>"HIPAA requirements may limit data access"</td></tr><tr><td><strong>Data</strong></td><td>Do we have the data we need?</td><td>"Patient eligibility data may be incomplete"</td></tr></tbody></table>

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
5. **Mitigation strategy**: [How to reduce likelihood or impact]
6. **Contingency plan**: [What if risk materializes]

Create risk table:

| Risk | Category | Likelihood | Impact | Mitigation | Contingency |
|------|----------|------------|--------|------------|-------------|

Focus on:
- Assumptions marked "TO VALIDATE" (these are risks)
- Technical dependencies (APIs, integrations)
- User adoption barriers (workflow changes)
- Regulatory/compliance requirements
```

***

### Component 3: Constraints Analysis (20 min)

#### Constraint Types

<table><thead><tr><th width="200">Type</th><th>Examples</th></tr></thead><tbody><tr><td><strong>Technical</strong></td><td>Platform, APIs, performance thresholds</td></tr><tr><td><strong>Regulatory</strong></td><td>HIPAA, GDPR, industry-specific</td></tr><tr><td><strong>Business</strong></td><td>Budget, vendor relationships, strategic alignment</td></tr><tr><td><strong>Time</strong></td><td>Deadlines, dependencies, seasonal factors</td></tr><tr><td><strong>Team</strong></td><td>Capacity, skills, timezone</td></tr><tr><td><strong>User</strong></td><td>Workflow integration, change tolerance, existing tools</td></tr></tbody></table>

#### Copy-Paste Prompt

```
Map all constraints:

[PASTE PROBLEM REFRAME from Part 1 - includes current workflow]
[PASTE RECOMMENDED DIRECTION from Part 1]

For each constraint type:

## Technical Constraints
- Platform: [What systems must we integrate with]
- Performance: [Response time, load requirements]
- APIs/Services: [Third-party dependencies]

## Regulatory Constraints
- Compliance: [HIPAA, GDPR, industry-specific]
- Data handling: [What can/cannot be stored]

## Business Constraints
- Budget: [Available resources]
- Timeline: [Hard deadlines]
- Vendor: [Existing partnerships]

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

<table><thead><tr><th width="181">Level</th><th>Description</th><th>Example</th></tr></thead><tbody><tr><td><strong>Input</strong></td><td>What users do</td><td>Usage, adoption, engagement</td></tr><tr><td><strong>Output</strong></td><td>What product delivers</td><td>Efficiency, quality, outcomes</td></tr><tr><td><strong>Outcome</strong></td><td>Business impact</td><td>Revenue, cost savings, strategic goals</td></tr></tbody></table>

#### Copy-Paste Prompt

```
Define success metrics based on hypothesis and features:

[PASTE HYPOTHESIS from Part 1]
[PASTE PRIORITIZED FEATURES from Component 1]

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

**Guardrail Metrics** (Must Not Degrade):
1. [Metric]: [Threshold] - [Concern if breached]

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

<table><thead><tr><th width="296">Category</th><th>Trade-Off</th></tr></thead><tbody><tr><td><strong>Scope vs. Time</strong></td><td>Feature richness vs. speed to market</td></tr><tr><td><strong>Quality vs. Speed</strong></td><td>Production polish vs. rapid validation</td></tr><tr><td><strong>Flexibility vs. Simplicity</strong></td><td>Configurable vs. opinionated</td></tr><tr><td><strong>Build vs. Buy</strong></td><td>Custom development vs. third-party integration</td></tr></tbody></table>

#### Copy-Paste Prompt

```
Document trade-off decisions:

[PASTE MVP SCOPE from Component 5]
[PASTE CONSTRAINTS from Component 3]

For each major decision:

**Decision**: [What we chose]
**Alternative**: [What we didn't choose]
**Trade-off**: [What we gained vs. gave up]
**Reasoning**: [Why this choice, based on evidence/constraints]
**Revisit condition**: [When we might reverse]
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
[Problem, hypothesis, success criteria - 3 sentences]

## Product Overview
- **One-line**: [What it does + who uses it]
- **Problem**: [Root cause from discovery]
- **Hypothesis**: [Testable statement with mechanism]
- **Evidence**: [Key findings from research]

## Target Users
[From Part 1 - who, job-to-be-done, pain points]

## Features & Prioritization
[P0, P1, V2 tables from Component 1]

## Risk Analysis
[Risk table with mitigations from Component 2]

## Constraints
[All constraint types from Component 3]

## Success Metrics
[North Star, input/output/guardrail from Component 4]

## MVP Scope
[In scope, out of scope from Component 5]

## Key Trade-Offs
[Major decisions from Component 6]

## User Flows
[Primary flow for P0 features]

## Open Questions
[What we still need to learn]

Format as professional markdown.
```

***

### PRD Quality Checklist

<table><thead><tr><th width="575">Criterion</th><th>Check</th></tr></thead><tbody><tr><td>Problem is root cause, not symptom</td><td>☐</td></tr><tr><td>Hypothesis is testable and falsifiable</td><td>☐</td></tr><tr><td>Assumptions are explicit</td><td>☐</td></tr><tr><td>Features linked to evidence</td><td>☐</td></tr><tr><td>P0 limited to 3-5 features</td><td>☐</td></tr><tr><td>Out of scope is defined with reasoning</td><td>☐</td></tr><tr><td>Success metrics are measurable</td><td>☐</td></tr><tr><td>Risks have mitigations</td><td>☐</td></tr><tr><td>Constraints shape solution</td><td>☐</td></tr></tbody></table>

***

### Summary: PRD Development (2-3 hours)

<table><thead><tr><th width="239">Component</th><th width="125">Time</th><th>Output</th></tr></thead><tbody><tr><td>Feature Prioritization</td><td>30 min</td><td>P0, P1, V2 with reasoning</td></tr><tr><td>Risk Analysis</td><td>30 min</td><td>Risk table with mitigations</td></tr><tr><td>Constraints Analysis</td><td>20 min</td><td>6 types that shape solution</td></tr><tr><td>Success Metrics</td><td>30 min</td><td>North Star + input/output/guardrail</td></tr><tr><td>MVP Boundaries</td><td>20 min</td><td>In scope vs. out of scope</td></tr><tr><td>Trade-Offs</td><td>20 min</td><td>Major decisions with rationale</td></tr><tr><td>Final PRD</td><td>30 min</td><td>Complete document</td></tr></tbody></table>

**Total time:** 2-3 hours

**Input:** Discovery Insights Report from Part 1

**Output:** Complete PRD ready for Knowledge Handoff

***

**Next: Part 3: Knowledge Handoff** — Package discovery and PRD for Cursor consumption.
