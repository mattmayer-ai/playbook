# Part 3: Knowledge Handoff

**Purpose:** Package discovery and PRD into structured format that Cursor can consume effectively.

**The Gap:** Claude is conversational. Cursor is code-focused and file-based. The handoff is where context gets lost.

**Time:** 4-6 hours

**Input:** Discovery Insights Report (Part 1) + Complete PRD (Part 2)

***

### Why the Handoff Matters

You've spent 6-11 hours in discovery and PRD development. You have:

* Discovery Insights Report (assumptions, hypothesis, insights, problem reframe, recommended direction)
* Complete PRD (features, risks, constraints, metrics, MVP scope, trade-offs)

**The problem:** If you just paste the PRD into Cursor chat, it won't retain context. You need to structure knowledge for persistent reference.

**The solution:** Create a project knowledge base that Cursor can search and reference.

***

### What Cursor Needs

Cursor is effective when it has:

* **Product context** — What problem and for whom
* **Technical constraints** — Non-negotiable requirements
* **Architectural decisions** — Choices we've made and why
* **Domain knowledge** — Industry-specific patterns
* **Success criteria** — How we know if implementation is correct

#### The Difference Context Makes

**Without context:**

```
User: "Create a user profile screen"
Cursor: [Generates generic form with name, email, photo]
```

**With context (from PRD + constraints):**

```
User: "Create a user profile screen"
Cursor: [References PRD, sees healthcare compliance]
Cursor: [Generates form with consent toggles, audit logging, no PHI in errors]
```

***

### File Structure

```
project-root/
├── docs/
│   ├── PRD.md                    # Complete PRD from Part 2
│   ├── DISCOVERY_INSIGHTS.md     # Synthesis report from Part 1
│   ├── CONTEXT.md                # Domain knowledge
│   ├── CONSTRAINTS.md            # Technical and compliance limits
│   └── ARCHITECTURE.md           # Technical decisions (add as you build)
├── .cursorrules                  # Cursor-specific patterns
└── README.md                     # Quick reference
```

***

### File 1: PRD.md

**Source:** Complete PRD from Part 2

**What to do:** Copy your complete PRD from Part 2 into `docs/PRD.md`

Your PRD already includes:

* Executive Summary
* Product Overview (problem, hypothesis, evidence)
* Target Users
* Features & Prioritization (P0, P1, V2)
* Risk Analysis
* Constraints
* Success Metrics
* MVP Scope
* Key Trade-Offs
* User Flows
* Open Questions

No changes needed — just copy it into the docs folder.

***

### File 2: DISCOVERY\_INSIGHTS.md

**Source:** Discovery Insights Report from Part 1

**What to do:** Copy your complete Discovery Insights Report from Part 1 into `docs/DISCOVERY_INSIGHTS.md`

Your report already includes:

* Executive Summary
* Hypothesis
* Key Insights
* Problem Reframe
* Assumptions Matrix (with validation status)
* Recommended Direction
* What to Validate Next

**Why separate from PRD:** Discovery shows your thinking and evidence. PRD shows what to build. Cursor benefits from seeing both.

***

### File 3: CONTEXT.md

**Purpose:** Domain knowledge and background for implementation.

**Template:**

```markdown
# [Product Name] - Context

**Purpose**: Domain knowledge and background information.

---

## Industry Context

**Domain**: [Healthcare / Construction / Education / etc.]

**Key terminology**:
- **[Term]**: [Definition and how we use it]

**Industry standards**:
- [Standard]: [What it requires]

**Compliance landscape**:
- [Why regulated]
- [Key regulations]
- [Penalties for non-compliance]

---

## User Context

**Who they are**: [Demographics, work environment, technical sophistication]

**How they work today**: [Current tools, workflow, pain points]

**Decision-making process**: [Who decides? Buying process?]

**Resistance factors**: [What makes adoption hard?]

---

## Competitive Context

**Existing solutions**:
1. **[Competitor]**
   - Strengths: [What they do well]
   - Weaknesses: [Where they fail]
   - Our differentiation: [Why we're different]

**Why users stick**: [Switching costs, incumbent advantages]

**Why users switch**: [Market shifts, new pain points]

---

## Technical Context

**Legacy systems we integrate with**:
- [System]: [Purpose, API quality, reliability]

**Data sources**:
- [Source]: [What data, freshness, reliability]

**Technical debt we're avoiding**:
- [Pattern to avoid]: [Why problematic]

**Patterns we're adopting**:
- [Pattern]: [Why it fits]

---

## Research Insights Summary

**Key findings**:
[Reference top insights from DISCOVERY_INSIGHTS.md]

**User quotes**:
> "[Verbatim quote capturing core insight]"
> — [User type/role]

**Surprising discoveries**:
- [What we didn't expect]
- [How it changed approach]

---

## Acronyms and Jargon

| Acronym | Full Term | Meaning in our context |
|---------|-----------|------------------------|
| [ABC] | [Full name] | [How we use it] |
```

***

### File 4: CONSTRAINTS.md

**Source:** Extracted from Part 2, Component 3

**Purpose:** Non-negotiable requirements.

**Template:**

```markdown
# [Product Name] - Constraints

**Purpose**: Non-negotiable technical and compliance requirements.

---

## Technical Constraints

### Platform
- **Must support**: [OS versions, browsers, devices]
- **Cannot use**: [Restricted technologies]
- **Performance budget**: [Load time, memory, bandwidth]

### Infrastructure
- **Must deploy to**: [Platform]
- **Cannot use**: [Restricted cloud providers]
- **Data residency**: [Geographic requirements]

### Security
- **Authentication**: [Required method]
- **Authorization**: [RBAC, ABAC, etc.]
- **Encryption**: [At rest, in transit]
- **Secrets management**: [How stored]

---

## Regulatory Constraints

### Healthcare (HIPAA) - if applicable
- **PHI handling**:
  - Never log PHI (names, dates, identifiers)
  - Encrypt at rest and in transit
  - Audit all access
  - Minimum necessary principle

- **User consent**:
  - Explicit consent before collection
  - Granular controls
  - Revocable at any time

### Privacy (GDPR, PIPEDA) - if applicable
- **Data minimization**: Only collect what's necessary
- **Purpose limitation**: Use only for stated purpose
- **Consent management**: Explicit, informed, revocable
- **Data portability**: Users can export data

---

## Business Constraints

- **Budget**: [Available resources]
- **Timeline**: [Hard deadlines with reasoning]
- **Vendor**: [Existing partnerships]
- **Strategic**: [Company direction]

---

## Team Constraints

- **Capacity**: [Available hours, people]
- **Skills**: [Expertise exists, gaps]
- **Location**: [Timezone, remote/co-located]

---

## User Constraints

- **Workflow**: [Can't disrupt existing process]
- **Tools**: [Already using X systems]
- **Change tolerance**: [Learning acceptable]

---

## Code Quality Constraints

### TypeScript
- **Strict mode**: Always enabled
- **No `any`**: Use `unknown` or specific types
- **Explicit return types**: For public functions

### Testing
- **Minimum coverage**: [Percentage]
- **Critical paths**: [What must have tests]
- **Integration tests**: [What requires E2E]

### Error Handling
- **User-facing errors**: Never expose stack traces
- **Logging**: No secrets, no PII/PHI
- **Retry logic**: [For what operations]

---

## Third-Party Dependencies

### Allowed
- [Library]: [Version range, purpose]

### Restricted
- [Library]: [Why not allowed]

### Evaluation criteria
- License compatible
- Maintained (update within X months)
- Security (no critical CVEs)
```

***

### File 5: .cursorrules

**Purpose:** Tell Cursor how to write code for your project.

**Template:**

```
# [Product Name] - Cursor Development Rules

## Project Overview
[One-line description from PRD]
Tech stack: [Frontend, backend, database]

## Code Quality Standards
- TypeScript strict mode; prefer explicit types over `any`
- ESLint and Prettier before every commit
- Meaningful names; self-documenting code
- Comments for complex logic only

## Project Structure
src/
├── components/   # Reusable UI
├── screens/      # Full screens (or pages/)
├── services/     # API clients, business logic
├── hooks/        # Custom React hooks
├── utils/        # Pure functions
├── types/        # Shared TypeScript types
└── config/       # App configuration

## Error Handling
- Try-catch for all async operations
- User-friendly error messages (never stack traces)
- Log errors with context (never log PHI/PII/secrets)

## Security and Compliance
[Paste domain-specific rules from CONSTRAINTS.md]

## API Patterns
- Use React Query for server state
- Handle loading and error states explicitly
- Implement retry logic for transient failures
- Cache responses appropriately

## Testing
- Unit tests for business logic
- Integration tests for API endpoints
- E2E tests for critical flows (see PRD.md - User Flows)
- Mock external services consistently

## Git Conventions
- Conventional commits: type(scope): description
  - feat: New feature
  - fix: Bug fix
  - docs: Documentation
  - refactor: Code change (no bug fix, no feature)
  - test: Adding tests
  - chore: Maintenance
- Atomic commits (one logical change)
- Never commit secrets, .env, generated files

## Documentation
- README: How to run, deploy, contribute
- Code comments: Why, not what
- JSDoc for public APIs
- Update ARCHITECTURE.md for architectural changes
```

***

### File 6: README.md

**Purpose:** Quick reference for anyone opening the project.

**Template:**

````markdown
# [Product Name]

[One-line description from PRD]

## Overview

[Brief summary: what it does, who it's for, what problem it solves]

## Tech Stack

- **Frontend**: [Technology]
- **Backend**: [Technology or BaaS]
- **Database**: [Technology]
- **Hosting**: [Platform]
- **Key Services**: [External integrations]

## Prerequisites

- Node.js 18+
- [Other requirements]

## Getting Started

1. Clone repository
   ```bash
   git clone [repo-url]
   cd [project-name]
````

2.  Install dependencies

    ```bash
    npm install
    ```
3.  Set up environment

    ```bash
    cp env.template .env
    # Edit .env with your values
    ```
4.  Run development server

    ```bash
    npm run dev
    ```
5.  Run tests

    ```bash
    npm test
    ```

### Project Structure

```
src/
├── components/   # Reusable UI components
├── screens/      # Full screens (or pages/)
├── services/     # API clients, business logic
├── hooks/        # Custom React hooks
├── utils/        # Pure functions
└── types/        # TypeScript types
```

### Key Documentation

* PRD - Product requirements and scope
* Discovery Insights - Research synthesis and evidence
* Constraints - Technical and compliance requirements
* Context - Domain knowledge

### Development Workflow

1. Create feature branch: `git checkout -b feat/feature-name`
2. Write code following `.cursorrules`
3. Run linter: `npm run lint`
4. Run tests: `npm test`
5. Commit: `feat(scope): description`
6. Push and create PR

### Deployment

\[Instructions for deploying to staging and production]

### Contributing

See `.cursorrules` for coding standards.

### License

\[License type]

````

---

## File 7: ARCHITECTURE.md (Optional)

**When to create:** After making your first architectural decisions

**Purpose:** Document key technical decisions.

**Template:**

```markdown
# [Product Name] - Architecture

**Purpose**: Document key technical decisions and reasoning.

---

## High-Level Architecture

[ASCII diagram or description]

---

## Architectural Decisions

### ADR-001: [Decision Title]

**Date**: [When decided]
**Status**: [Proposed / Accepted / Deprecated]

**Context**: [What problem? What constraints?]

**Decision**: [What we chose]

**Reasoning**: [Why we made this choice]

**Alternatives considered**:
1. **[Option]**: [Pros/cons, why not chosen]

**Consequences**:
- **Positive**: [Benefits]
- **Negative**: [Trade-offs]

**Revisit when**: [Conditions for reconsideration]

---

[Add more ADRs as you make decisions]
````

***

### Handoff Checklist

#### Required Files

<table><thead><tr><th width="305">File</th><th width="305">Source</th><th>Status</th></tr></thead><tbody><tr><td><code>docs/PRD.md</code></td><td>Part 2 output</td><td>☐</td></tr><tr><td><code>docs/DISCOVERY_INSIGHTS.md</code></td><td>Part 1 output</td><td>☐</td></tr><tr><td><code>docs/CONTEXT.md</code></td><td>Domain knowledge</td><td>☐</td></tr><tr><td><code>docs/CONSTRAINTS.md</code></td><td>Technical/compliance</td><td>☐</td></tr><tr><td><code>.cursorrules</code></td><td>Coding patterns</td><td>☐</td></tr><tr><td><code>README.md</code></td><td>Quick reference</td><td>☐</td></tr></tbody></table>

#### Optional but Recommended

<table><thead><tr><th width="270">File</th><th>When to Add</th></tr></thead><tbody><tr><td><code>docs/ARCHITECTURE.md</code></td><td>After first architectural decisions</td></tr><tr><td><code>env.template</code></td><td>When environment variables needed</td></tr></tbody></table>

#### Content Quality

<table><thead><tr><th width="615">Check</th><th>Status</th></tr></thead><tbody><tr><td>PRD includes specific user segments (not generic "users")</td><td>☐</td></tr><tr><td>Success metrics quantifiable with targets</td><td>☐</td></tr><tr><td>MVP scope explicitly defined</td><td>☐</td></tr><tr><td>Out-of-scope items with reasoning</td><td>☐</td></tr><tr><td>User flows include edge cases</td><td>☐</td></tr><tr><td>Technical constraints specific (not "fast" but "&#x3C;2s")</td><td>☐</td></tr><tr><td>Compliance requirements explicit</td><td>☐</td></tr><tr><td>Discovery Insights shows evidence trail</td><td>☐</td></tr></tbody></table>

#### Cursor Setup

<table><thead><tr><th width="617">Check</th><th>Status</th></tr></thead><tbody><tr><td>Project opened in Cursor</td><td>☐</td></tr><tr><td>All docs files in <code>docs/</code> directory</td><td>☐</td></tr><tr><td><code>.cursorrules</code> in project root</td><td>☐</td></tr><tr><td>Test: "Summarize the product requirements" works</td><td>☐</td></tr></tbody></table>

#### Context Validation

Test Cursor's understanding:

* "What problem does this product solve?"
* "What are the compliance requirements?"
* "What's explicitly out of scope for MVP?"
* "What technical constraints must we respect?"
* "What are key insights from user research?"

If Cursor can't answer, add more context.

***

### Summary: Knowledge Handoff

**What you create:**

* PRD.md (from Part 2)
* DISCOVERY\_INSIGHTS.md (from Part 1)
* CONTEXT.md (domain knowledge)
* CONSTRAINTS.md (non-negotiable requirements)
* .cursorrules (coding patterns)
* README.md (quick reference)
* ARCHITECTURE.md (add as you build)

**Time investment:** 4-6 hours to package work

**Why it matters:** Cursor is only as effective as the context you provide. Good handoff means Cursor makes correct assumptions about architecture, security, compliance, and user needs.

***

**Next: Part 4: Infrastructure Setup** — Rapidly configure projects for scalable development.
