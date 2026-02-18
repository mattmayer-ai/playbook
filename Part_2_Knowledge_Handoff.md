# Part 2: Knowledge Handoff (Claude → Cursor)

**Purpose**: Package discovery output from Claude into structured format that Cursor can consume effectively.

**The Gap**: Claude is conversational and iterative. Cursor is code-focused and file-based. The handoff is where most context gets lost.

---

## Why the Handoff Matters

You've spent 4-8 weeks in discovery. You have:
- User research synthesis
- Validated assumptions
- Experiment results
- A clear PRD

Now you need Cursor to understand all of this without re-explaining it every time you ask for a feature.

**The problem**: If you just paste the PRD into Cursor chat, it won't retain context. You need to structure knowledge for persistent reference.

**The solution**: Create a project knowledge base that Cursor can search and reference.

---

## What Cursor Needs to Know

Cursor is effective when it has:

1. **Product context** - What problem are we solving and for whom?
2. **Technical constraints** - What are the non-negotiable requirements?
3. **Architectural decisions** - What choices have we already made and why?
4. **Domain knowledge** - Industry-specific patterns or compliance requirements
5. **Success criteria** - How do we know if implementation is correct?

Without this, Cursor makes generic choices that don't match your requirements.

### Example: The Difference Context Makes

**Without context**:
```
User: "Create a user profile screen"
Cursor: [Generates generic form with name, email, photo upload]
```

**With context** (from PRD + constraints):
```
User: "Create a user profile screen"
Cursor: [References PRD, sees healthcare compliance requirement]
Cursor: [Generates form with consent toggles, audit logging, no PHI in error messages]
```

---

## How to Structure Context for Cursor

Use these files in your project root or `docs/` directory. Cursor searches these automatically when you reference the project.

### Core Files

```
project-root/
├── docs/
│   ├── PRD.md                    # Product requirements
│   ├── CONTEXT.md                # Background and domain knowledge
│   ├── CONSTRAINTS.md            # Technical and compliance limits
│   ├── ARCHITECTURE.md           # Key technical decisions
│   └── USER_RESEARCH.md          # Research synthesis (optional)
├── .cursorrules                  # Cursor-specific coding patterns
└── README.md                     # Quick reference
```

---

## PRD.md: Product Requirements

This is the main reference document. Structure it for AI consumption—clear sections, explicit relationships, no ambiguity.

### PRD Template for Cursor

```markdown
# [Product Name] - Product Requirements Document

**Last Updated**: [Date]  
**Status**: [Draft / Validated / In Development]  
**Decision Point**: [When we evaluate MVP success]

---

## Product Overview

**One-line description**:
[What this product does and who uses it]

**Problem we're solving**:
[From discovery: specific user segment, specific problem, why it matters]

**Solution approach**:
[How this product solves the problem - high level, not implementation details]

**Target users**:
**Primary**: [Specific persona]
- Job-to-be-done: [What they're trying to accomplish]
- Current workflow: [How they do this today]
- Pain points: [What breaks in current approach]

**Secondary**: [Other personas, if applicable]

---

## Validated Assumptions

**What we've proven** (from experiments):
1. [Assumption]: [Evidence]
   - Experiment: [What we tested]
   - Result: [What we learned]

2. [Assumption]: [Evidence]

**What we're still testing**:
1. [Assumption]: [Planned validation]

**Known risks we're accepting**:
1. [Risk]: [Why we're proceeding anyway]

---

## MVP Scope

### Core Features (Must Have)

**Feature 1: [Name]**
- **User value**: [Why this matters to users]
- **Success metric**: [How we measure if this works]
- **Priority**: P0 (blocks launch) / P1 (launch blocker) / P2 (post-launch)

**Feature 2: [Name]**
- **User value**: [Why this matters]
- **Success metric**: [How we measure]
- **Priority**: [P0/P1/P2]

### Explicitly Out of Scope (V2+)

1. **[Feature we're deferring]**
   - Why later: [Reasoning]
   - Revisit when: [Condition]

---

## User Flows

### Primary Flow: [Name]

**Happy path**:
1. User starts at [screen/state]
2. User does [action]
3. System validates [data/state]
4. System responds [behavior]
5. User sees [outcome]

**Edge cases**:
- **If [error condition]** → System [behavior], User sees [message]
- **If [edge case]** → System [behavior]

### Secondary Flow: [Name]
[Same structure]

---

## Technical Requirements

### Platform
- **Type**: Web / Mobile / Both
- **Deployment target**: [Environment]

### Performance
- **Load time**: [Threshold - e.g., <2s initial page load]
- **API response**: [Threshold - e.g., <500ms p95]
- **Offline capability**: [Yes/No - if mobile]

### Scalability
- **Concurrent users**: [Target - e.g., 1000 concurrent]
- **Data volume**: [Expected scale - e.g., 10K records/month]
- **Growth projection**: [Next 12 months]

### Compliance
- **Standards**: [e.g., HIPAA, PIPEDA, GDPR]
- **Data handling**: [Specific requirements]
- **Audit requirements**: [What needs logging]

### Integration Requirements
- **[External Service]**: [API / SDK]
  - Purpose: [Why we integrate]
  - Critical path: [Yes/No - blocks core functionality?]

---

## Data Model

### Key Entities

**Entity: [Name]**
```typescript
interface EntityName {
  id: string;
  // Required fields
  field1: Type;
  field2: Type;
  
  // Optional fields
  field3?: Type;
  
  // Audit fields
  createdAt: Date;
  updatedAt: Date;
  createdBy: string;
}
```

**Relationships**:
- [Entity A] → [Entity B]: [Relationship type - 1:1, 1:many, many:many]

---

## Success Metrics

**North Star Metric**: [Primary indicator of product success]

**Input Metrics** (leading indicators):
- **[Metric]**: [Target] - [How measured]
- **[Metric]**: [Target] - [How measured]

**Output Metrics** (lagging indicators):
- **[Metric]**: [Target] - [How measured]
- **[Metric]**: [Target] - [How measured]

**Instrumentation**:
- [Analytics platform]
- [Key events to track]

---

## Timeline and Milestones

**Phase 1: MVP** (Weeks 1-8)
- Week 1-2: Setup, core data models
- Week 3-5: Feature development
- Week 6-7: Testing, refinement
- Week 8: Staging deployment

**Decision Point** (Week 8):
- Criteria for beta: [Metrics/conditions]
- Go/No-go based on: [Specific thresholds]

**Phase 2: Beta** (Weeks 9-12)
- [Milestones and decision points]

---

## Open Questions

1. **[Question]**
   - Context: [Why this matters]
   - Decision needed by: [Date]
   - Blocking: [Yes/No]

2. **[Question]**

---

## Appendix

**User research**: See [USER_RESEARCH.md](./USER_RESEARCH.md)  
**Technical constraints**: See [CONSTRAINTS.md](./CONSTRAINTS.md)  
**Architecture decisions**: See [ARCHITECTURE.md](./ARCHITECTURE.md)
```

---

## CONTEXT.md: Background and Domain Knowledge

This file provides domain-specific context that Cursor can't infer from the PRD alone.

### CONTEXT Template

```markdown
# [Product Name] - Context

**Purpose**: Domain knowledge and background information for implementation.

---

## Industry Context

**Domain**: [Healthcare / Construction / Education / etc.]

**Key terminology**:
- **[Term]**: [Definition and how we use it]
- **[Term]**: [Definition]

**Industry standards**:
- [Standard]: [What it requires]
- [Standard]: [What it requires]

**Compliance landscape**:
- [Why this industry is regulated]
- [Key regulations that apply]
- [Penalties for non-compliance]

---

## User Context

**Who they are**:
[Demographics, work environment, technical sophistication]

**How they work today**:
[Current tools, workflow, pain points]

**Decision-making process**:
[Who decides to adopt? What's the buying process?]

**Resistance factors**:
[What makes adoption hard? Change management considerations?]

---

## Competitive Context

**Existing solutions**:
1. **[Competitor/Tool]**
   - Strengths: [What they do well]
   - Weaknesses: [Where they fail]
   - Our differentiation: [Why we're different]

**Why users stick with current solutions**:
[Switching costs, incumbent advantages]

**Why users are ready to switch**:
[Market shifts, new pain points, technology enablement]

---

## Technical Context

**Legacy systems we integrate with**:
- [System]: [Purpose, API quality, reliability]

**Data sources**:
- [Source]: [What data, how fresh, reliability]

**Technical debt we're avoiding**:
- [Pattern to avoid]: [Why it's problematic]

**Patterns we're adopting**:
- [Pattern]: [Why it fits this domain]

---

## Research Insights

**Key findings** (from discovery):
1. [Insight]: [Evidence and implication]
2. [Insight]: [Evidence and implication]

**User quotes**:
> "[Verbatim quote that captures core insight]"
> — [User type/role]

**Surprising discoveries**:
- [What we didn't expect]
- [How it changed our approach]

---

## Acronyms and Jargon

| Acronym | Full Term | Meaning in our context |
|---------|-----------|------------------------|
| [ABC] | [Full name] | [How we use it] |
| [DEF] | [Full name] | [How we use it] |
```

---

## CONSTRAINTS.md: Technical and Compliance Limits

Hard requirements that can't be negotiated. Cursor needs to know what's non-negotiable.

### CONSTRAINTS Template

```markdown
# [Product Name] - Constraints

**Purpose**: Non-negotiable technical and compliance requirements.

---

## Technical Constraints

### Platform
- **Must support**: [OS versions, browsers, devices]
- **Cannot use**: [Restricted technologies, libraries]
- **Performance budget**: [Load time, memory, bandwidth]

### Infrastructure
- **Must deploy to**: [Platform - AWS, Firebase, etc.]
- **Cannot use**: [Restricted cloud providers]
- **Data residency**: [Geographic requirements]

### Security
- **Authentication**: [Required method - OAuth, SSO, etc.]
- **Authorization**: [RBAC, ABAC, etc.]
- **Encryption**: [At rest, in transit requirements]
- **Secrets management**: [How secrets are stored]

### Scalability
- **Must handle**: [Load requirements]
- **Auto-scaling**: [Required/Not required]
- **Database**: [Read/write patterns, expected volume]

---

## Compliance Constraints

### Healthcare (HIPAA) - if applicable
- **PHI handling**:
  - Never log PHI (names, dates, identifiers)
  - Encrypt at rest and in transit
  - Audit all access
  - Minimum necessary principle

- **User consent**:
  - Explicit consent before data collection
  - Granular controls (not all-or-nothing)
  - Revocable at any time

- **Data retention**:
  - Delete data when requested (right to erasure)
  - Minimum retention period: [Duration]
  - Maximum retention period: [Duration]

### Financial (PCI-DSS) - if applicable
- **Payment data**:
  - Never store credit card numbers
  - Use tokenization (Stripe, etc.)
  - TLS 1.2+ for transmission

### Privacy (GDPR, PIPEDA) - if applicable
- **Data minimization**: Only collect what's necessary
- **Purpose limitation**: Use data only for stated purpose
- **Consent management**: Explicit, informed, revocable
- **Data portability**: Users can export their data

---

## Domain-Specific Constraints

### [Your industry]
- **[Constraint]**: [Requirement and why]
- **[Constraint]**: [Requirement and why]

---

## Code Quality Constraints

### TypeScript
- **Strict mode**: Always enabled
- **No `any`**: Use `unknown` or specific types
- **Explicit return types**: For public functions

### Testing
- **Minimum coverage**: [Percentage - e.g., 80%]
- **Critical paths**: [What must have tests]
- **Integration tests**: [What requires E2E coverage]

### Error Handling
- **User-facing errors**: Never expose stack traces
- **Logging**: No secrets, no PII/PHI
- **Retry logic**: [For what operations]

---

## Third-Party Dependencies

### Allowed
- [Library]: [Version range, purpose]
- [Library]: [Version range, purpose]

### Restricted
- [Library]: [Why it's not allowed]
- [Library]: [Why it's not allowed]

### Evaluation criteria
- License compatible: [Acceptable licenses]
- Maintained: [Last update within X months]
- Security: [No critical CVEs]

---

## Deployment Constraints

### Environments
- **Development**: [Access, resources]
- **Staging**: [Access, must mirror production]
- **Production**: [Access restricted to who]

### Release process
- **Testing required**: [Unit, integration, E2E]
- **Approval required**: [Who must approve]
- **Rollback plan**: [Must be tested before release]

### Monitoring
- **Must track**: [Metrics, errors, performance]
- **Alerting**: [What triggers alerts]
- **On-call**: [Who responds to incidents]
```

---

## ARCHITECTURE.md: Key Technical Decisions

Document architectural choices and reasoning. When Cursor asks "why is this structured this way?", the answer should be here.

### ARCHITECTURE Template

```markdown
# [Product Name] - Architecture

**Purpose**: Document key technical decisions and reasoning.

---

## High-Level Architecture

```
[ASCII diagram or description of system components]

User → [Frontend] → [API] → [Database]
                   ↓
              [External Services]
```

**Components**:
- **Frontend**: [Technology, why chosen]
- **Backend**: [Technology, why chosen]
- **Database**: [Technology, why chosen]
- **External Services**: [List and purpose]

---

## Architectural Decisions

### ADR-001: [Decision Title]

**Date**: [When decided]  
**Status**: [Proposed / Accepted / Deprecated]

**Context**:
[What problem are we solving? What constraints apply?]

**Decision**:
[What we chose to do]

**Reasoning**:
[Why we made this choice]

**Alternatives considered**:
1. **[Option]**: [Pros/cons, why not chosen]
2. **[Option]**: [Pros/cons, why not chosen]

**Consequences**:
- **Positive**: [Benefits]
- **Negative**: [Trade-offs we're accepting]

**Revisit when**:
[Conditions that would make us reconsider]

---

### ADR-002: [Next Decision]
[Same structure]

---

## Data Architecture

### Storage

**Primary database**: [Choice]
- **Why**: [Reasoning - e.g., document model fits domain, managed service]
- **Schema design**: [Key collections/tables and relationships]

**Cache layer**: [Choice - Redis, etc.]
- **Why**: [Reasoning]
- **What we cache**: [Data types, TTL]

**File storage**: [Choice - S3, Cloud Storage, etc.]
- **Why**: [Reasoning]
- **What we store**: [File types, retention]

### Data Flow

**Write path**:
1. [Step]
2. [Step]
3. [Validation and storage]

**Read path**:
1. [Step]
2. [Caching strategy]
3. [Fallback behavior]

---

## API Design

### Principles
- RESTful where appropriate
- GraphQL for [specific use cases]
- Versioning strategy: [URL / Header]

### Authentication
- Method: [JWT, session, OAuth]
- Token expiration: [Duration]
- Refresh strategy: [How tokens are refreshed]

### Rate Limiting
- Anonymous: [Limit]
- Authenticated: [Limit]
- Premium: [Limit]

---

## Frontend Architecture

### State Management
- **Server state**: [Library - React Query, SWR]
- **Client state**: [Library - Zustand, Context]
- **Why this split**: [Reasoning]

### Component Structure
- **Atomic design** or **Feature-based**
- **Shared components**: [Where they live]
- **Feature-specific**: [Where they live]

### Styling
- **Approach**: [Tailwind, CSS Modules, styled-components]
- **Why**: [Reasoning]
- **Theme**: [How we handle dark mode, tokens]

---

## Testing Strategy

### Unit Tests
- **What we test**: [Pure functions, business logic]
- **What we don't**: [UI components beyond smoke tests]
- **Coverage target**: [Percentage]

### Integration Tests
- **What we test**: [API endpoints, database interactions]
- **Mocking strategy**: [What we mock, what we don't]

### E2E Tests
- **Critical paths**: [User flows that must work]
- **Frequency**: [When we run these]

---

## Deployment Architecture

### Infrastructure
- **Hosting**: [Platform]
- **CI/CD**: [Tool and workflow]
- **Environments**: [Dev, staging, production setup]

### Scaling Strategy
- **Current**: [What we do now]
- **Future**: [When we'll need to scale, what changes]

---

## Security Architecture

### Authentication Flow
[Diagram or description]

### Authorization Model
- **RBAC**: [Roles and permissions]
- **Data access**: [Row-level security, if applicable]

### Secret Management
- **How secrets are stored**: [Service]
- **How they're accessed**: [Environment variables, vault, etc.]
- **Rotation policy**: [Frequency]

---

## Monitoring and Observability

### Metrics
- **Infrastructure**: [CPU, memory, requests/sec]
- **Application**: [Custom business metrics]
- **User experience**: [Load time, error rate]

### Logging
- **What we log**: [Events, errors]
- **What we don't**: [PHI, secrets, PII]
- **Retention**: [Duration]

### Alerting
- **Critical**: [What triggers immediate response]
- **Warning**: [What we monitor but doesn't page]

---

## Future Considerations

### Technical Debt
1. **[Item]**: [What needs refactoring, why, when]

### Scaling Challenges
1. **[Challenge]**: [When it becomes a problem, solution approach]

### Platform Evolution
- **When we'll need [X]**: [Condition, solution]
```

---

## .cursorrules: Cursor-Specific Patterns

This file tells Cursor how to write code for your project. It's separate from PRD/context because it's tool-specific.

### .cursorrules Template

```
# [Product Name] - Cursor Development Rules

## Project Overview
[One-line description]
Tech stack: [Frontend, backend, database]

## Code Quality Standards
- TypeScript strict mode; prefer explicit types over `any`
- ESLint and Prettier before every commit
- Meaningful names; self-documenting code; comments for complex logic only

## Project Structure
Folder organization:
src/
├── components/   # Reusable UI
├── screens/      # Full screens (or pages/ for web)
├── services/     # API clients, business logic
├── hooks/        # Custom React hooks
├── utils/        # Pure functions
├── types/        # Shared TypeScript types
└── config/       # App configuration

## Error Handling
- Try-catch for all async operations
- User-friendly error messages (never expose stack traces)
- Log errors with context (but never log [PHI/PII/secrets])

## Security and Compliance
[Domain-specific rules - paste from CONSTRAINTS.md]

Example for healthcare:
- Never log PHI (names, DOB, medical data, identifiers)
- All PHI must be encrypted at rest and in transit
- Implement audit logging for all PHI access
- Explicit user consent before data collection
- Data minimization (only collect what's necessary)

## API Patterns
- Use React Query for all server state
- Handle loading and error states explicitly
- Implement retry logic for transient failures
- Cache responses appropriately (see ARCHITECTURE.md)

## Testing
- Unit tests for business logic and utilities
- Integration tests for API endpoints
- E2E tests for critical user flows (see ARCHITECTURE.md)
- Mock external services consistently (see jest.setup.js)

## Git Conventions
- Conventional commits: type(scope): description
  - feat: New feature
  - fix: Bug fix
  - docs: Documentation only
  - style: Formatting, no code change
  - refactor: Code change that neither fixes bug nor adds feature
  - test: Adding tests
  - chore: Maintain/config
- Atomic commits (one logical change per commit)
- Never commit secrets, .env, or generated files

## Documentation
- README: How to run, deploy, contribute
- Code comments: Why, not what (code should be self-explanatory)
- JSDoc for public APIs
- Update ARCHITECTURE.md when making architectural changes
```

---

## Handoff Checklist

Use this before moving from Claude to Cursor:

```markdown
## Knowledge Handoff Checklist

### Required Files
- [ ] `docs/PRD.md` - Product requirements (complete, structured)
- [ ] `docs/CONTEXT.md` - Domain knowledge and background
- [ ] `docs/CONSTRAINTS.md` - Non-negotiable technical/compliance requirements
- [ ] `.cursorrules` - Coding patterns and standards
- [ ] `README.md` - Quick reference, how to run

### Optional but Recommended
- [ ] `docs/ARCHITECTURE.md` - Key technical decisions (if any made)
- [ ] `docs/USER_RESEARCH.md` - Research synthesis (if relevant during dev)
- [ ] `env.template` - Environment variables (with placeholder values)

### Content Quality
- [ ] PRD includes specific user segments (not "users")
- [ ] Success metrics are quantifiable
- [ ] MVP scope is explicitly defined
- [ ] Out-of-scope items are listed with reasoning
- [ ] User flows include edge cases
- [ ] Technical constraints are specific (not "fast" but "<2s load time")
- [ ] Compliance requirements are explicit (if applicable)

### Cursor Setup
- [ ] Project opened in Cursor
- [ ] All docs files created in project root or docs/ directory
- [ ] .cursorrules file in project root
- [ ] Test prompt: "Summarize the product requirements" (Cursor should reference PRD)

### Context Validation
Test Cursor's understanding with these prompts:
- [ ] "What problem does this product solve?"
- [ ] "What are the compliance requirements?"
- [ ] "What's explicitly out of scope for MVP?"
- [ ] "What technical constraints must we respect?"

If Cursor can't answer these from your docs, add more context.
```

---

## Example: Full Handoff Package

### Minimal Example (TakeCost)

**docs/PRD.md**:
```markdown
# TakeCost AutoTake - Product Requirements

## Product Overview
**One-line**: AI-powered construction estimation that reduces bid prep time from 8 hours to <2 hours.

**Problem**: General contractors lose bids because they submit late, not because prices are wrong.

**Solution**: Computer vision + AI to extract measurements from blueprints and generate estimates automatically.

## Validated Assumptions
1. **Speed > Accuracy**: Contractors prioritize fast estimates. Evidence: 15/15 contractors in concierge test said speed was #1 value.
2. **90% accuracy is sufficient**: Contractors manually review estimates anyway. Evidence: Average adjustment was 8% from our AI output.

## MVP Scope
**Core Features**:
1. PDF upload → measurement extraction (Computer vision with Scale AI)
2. Material pricing lookup (integrate TakeCost existing database)
3. Estimate generation (structured output with line items)

**Out of scope**: Multi-user collaboration, mobile app, PDF editing

## Technical Requirements
- Performance: Process blueprint <30 seconds
- Accuracy: 90%+ measurement extraction (validated in concierge)
- Compliance: None (construction bidding not regulated)

## Success Metrics
- Estimation time: <2 hours (vs 8 hours manual)
- Usage: 70% of users complete estimates using AutoTake
- Accuracy: Win rate within 5% of manual estimates
```

**docs/CONSTRAINTS.md**:
```markdown
# TakeCost AutoTake - Constraints

## Technical Constraints
- Must integrate with existing TakeCost material pricing database
- PDF processing must handle scanned documents (OCR required)
- Cannot use Google Cloud (client uses AWS)

## Performance
- Blueprint processing: <30 seconds
- API response: <500ms (after CV processing)

## Code Quality
- TypeScript strict mode
- No `any` types
- 80% test coverage minimum
```

**.cursorrules**:
```
# TakeCost AutoTake - Development Rules

## Project Overview
AI-powered construction estimation tool using computer vision.
Stack: React + TypeScript, AWS Bedrock (Claude), Scale AI (CV), PostgreSQL

## Code Quality
- TypeScript strict mode; no `any` types
- Explicit error handling for CV and AI operations
- Comments for AI prompt engineering logic only

## Error Handling
- CV failures → graceful degradation (let user upload measurements)
- AI failures → retry with exponential backoff
- Never expose Scale AI or Bedrock errors to users

## API Patterns
- React Query for all API calls
- Handle CV processing status (pending → processing → complete)
- Cache material pricing (TTL: 24 hours)

## Testing
- Unit tests for measurement calculation logic
- Integration tests for CV → estimate pipeline
- Mock Scale AI and Bedrock in tests
```

---

## Summary: Knowledge Handoff

**What you create**:
1. **PRD.md** - Product requirements (structured for AI)
2. **CONTEXT.md** - Domain knowledge and background
3. **CONSTRAINTS.md** - Non-negotiable requirements
4. **.cursorrules** - Coding patterns
5. **ARCHITECTURE.md** - Technical decisions (as you make them)

**Time investment**: 4-8 hours to package discovery work

**Why it matters**: Cursor is only as effective as the context you provide. Good handoff means Cursor makes correct assumptions about architecture, security, compliance, and user needs.

---

**Next**: [Part 3: Infrastructure Setup in Cursor](./Part_3_Infrastructure_Setup.md)