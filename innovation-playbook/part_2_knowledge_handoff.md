# Part 3: Knowledge Handoff

**Purpose**: Package discovery and PRD into structured format that Cursor can consume effectively.

**The Gap**: Claude is conversational. Cursor is code-focused and file-based. The handoff is where context gets lost.

**Time**: 4-6 hours

**Input**: Discovery Insights Report (Part 1) + Complete PRD (Part 2)

***

### Why the Handoff Matters

You've spent 6-10 hours in discovery and PRD development. You have:

* Discovery Insights Report (assumptions, hypothesis, insights, problem reframe, recommended direction)
* Complete PRD (features, risks, constraints, metrics, MVP scope, trade-offs)

**The problem**: If you just paste the PRD into Cursor chat, it won't retain context. You need to structure knowledge for persistent reference.

**The solution**: Create a project knowledge base that Cursor can search and reference.

***

### What Cursor Needs

Cursor is effective when it has:

* **Product context** - What problem and for whom
* **Technical constraints** - Non-negotiable requirements
* **Architectural decisions** - Choices we've made and why
* **Domain knowledge** - Industry-specific patterns
* **Success criteria** - How we know if implementation is correct

#### Example: The Difference Context Makes

**Without context**:

```
User: "Create a user profile screen"
Cursor: [Generates generic form with name, email, photo]
```

**With context** (from PRD + constraints):

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

**Source**: Complete PRD from Part 2

**What to do**: Copy your complete PRD from Part 2 into `docs/PRD.md`

Your PRD already includes:

* Executive Summary
* Product Overview (problem, solution, evidence)
* Features & Prioritization (P0, P1, V2)
* Risk Analysis
* Constraints
* Success Metrics
* MVP Scope
* Key Trade-Offs
* User Flows
* Technical Architecture
* Open Questions & Validation Plan

**No changes needed** - just copy it into the docs folder.

***

### File 2: DISCOVERY\_INSIGHTS.md

**Source**: Discovery Insights Report from Part 1

**What to do**: Copy your complete Discovery Insights Report from Part 1 into `docs/DISCOVERY_INSIGHTS.md`

Your report already includes:

* Assumptions Matrix
* Hypothesis
* Key Insights
* Problem Reframe
* Recommended Direction
* Methodology

**Why separate from PRD**: Discovery shows your thinking and evidence. PRD shows what to build. Cursor benefits from seeing both.

***

### File 3: CONTEXT.md

**Purpose**: Domain knowledge and background for implementation.

**Template**:

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

**Source**: Extracted from Part 2, Component 3

**Purpose**: Non-negotiable requirements.

**Template**:

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

## Time Constraints

- **Deadline**: [When, why]
- **Dependencies**: [What must happen first]
- **Seasonal**: [Time-sensitive factors]

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

## How Constraints Shape Solution

[From Part 2 Component 3 - explain how constraints combine to determine approach]

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

**Purpose**: Tell Cursor how to write code for your project.

**Template**:

```markdown
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

Example for healthcare:
- Never log PHI (names, DOB, medical data, identifiers)
- All PHI encrypted at rest and in transit
- Audit logging for all PHI access
- Explicit user consent before collection
- Data minimization

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
  - style: Formatting
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

**Purpose**: Quick reference for anyone opening the project.

**Template**:

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

src/ ├── components/ # Reusable UI components ├── screens/ # Full screens (or pages/) ├── services/ # API clients, business logic ├── hooks/ # Custom React hooks ├── utils/ # Pure functions └── types/ # TypeScript types

### Key Documentation

* **PRD** - Product requirements and scope
* **Discovery Insights** - Research synthesis and evidence
* **Constraints** - Technical and compliance requirements
* **Context** - Domain knowledge

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

**When to create**: After making your first architectural decisions

**Purpose**: Document key technical decisions.

**Template**:

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

* [ ] `docs/PRD.md` - Complete PRD from Part 2
* [ ] `docs/DISCOVERY_INSIGHTS.md` - Report from Part 1
* [ ] `docs/CONTEXT.md` - Domain knowledge
* [ ] `docs/CONSTRAINTS.md` - Technical/compliance requirements
* [ ] `.cursorrules` - Coding patterns
* [ ] `README.md` - Quick reference

#### Optional but Recommended

* [ ] `docs/ARCHITECTURE.md` - Add after first decisions
* [ ] `env.template` - Environment variables

#### Content Quality

* [ ] PRD includes specific user segments (not generic "users")
* [ ] Success metrics quantifiable with targets
* [ ] MVP scope explicitly defined
* [ ] Out-of-scope items with reasoning
* [ ] User flows include edge cases
* [ ] Technical constraints specific (not "fast" but "<2s")
* [ ] Compliance requirements explicit
* [ ] Discovery Insights shows evidence trail

#### Cursor Setup

* [ ] Project opened in Cursor
* [ ] All docs files in `docs/` directory
* [ ] `.cursorrules` in project root
* [ ] Test: "Summarize the product requirements" (Cursor should reference PRD)

#### Context Validation

Test Cursor's understanding:

* [ ] "What problem does this product solve?"
* [ ] "What are the compliance requirements?"
* [ ] "What's explicitly out of scope for MVP?"
* [ ] "What technical constraints must we respect?"
* [ ] "What are key insights from user research?"

If Cursor can't answer, add more context.

***

### Example: Minimal Handoff

#### TakeCost AutoTake

**docs/PRD.md**:

```markdown
# TakeCost AutoTake - PRD

## Product Overview
**One-line**: AI-powered construction estimation reducing bid prep 8 hours → <2 hours.

**Problem**: Contractors lose bids due to late submission, not pricing errors.

**Solution**: CV + AI extracts measurements from blueprints, generates estimates.

## Features & Prioritization

| Feature | Priority | Reasoning |
|---------|----------|-----------|
| PDF → measurement extraction | **P0** | Core job broken without it |
| Material pricing lookup | **P0** | Without pricing, just measurements |
| Estimate generation | **P0** | Deliverable contractors need |

## Constraints
- Performance: Process blueprint <30 seconds
- Accuracy: 90%+ extraction
- Must integrate with TakeCost material database
- Cannot use Google Cloud (client uses AWS)

## Success Metrics
**North Star**: Estimation time <2 hours (vs 8 hours manual)
```

**docs/CONSTRAINTS.md**:

```markdown
# TakeCost AutoTake - Constraints

## Technical
- Must integrate with TakeCost material database
- PDF processing must handle scanned docs (OCR)
- Cannot use Google Cloud (AWS only)
- Performance: <30 seconds blueprint processing

## Code Quality
- TypeScript strict mode
- No `any` types
- 80% test coverage minimum
```

**.cursorrules**:

```markdown
# TakeCost AutoTake

Tech stack: React + TypeScript, AWS Bedrock, Scale AI, PostgreSQL

## Error Handling
- CV failures → graceful degradation (user uploads measurements)
- AI failures → retry with exponential backoff
- Never expose Scale AI/Bedrock errors to users

## Testing
- Unit tests for measurement calculations
- Integration tests for CV → estimate pipeline
- Mock Scale AI and Bedrock in tests
```

***

### Summary: Knowledge Handoff

**What you create**:

* PRD.md (from Part 2)
* DISCOVERY\_INSIGHTS.md (from Part 1)
* CONTEXT.md (domain knowledge)
* CONSTRAINTS.md (non-negotiable requirements)
* .cursorrules (coding patterns)
* README.md (quick reference)
* ARCHITECTURE.md (add as you build)

**Time investment**: 4-6 hours to package work

**Why it matters**: Cursor is only as effective as the context you provide. Good handoff means Cursor makes correct assumptions about architecture, security, compliance, and user needs.

***

**Next**: Part 4: Infrastructure Setup
