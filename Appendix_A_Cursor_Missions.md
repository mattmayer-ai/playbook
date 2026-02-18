# Appendix A: Cursor Setup with Mission-Based Organization

**When to use this pattern**: Large projects with multiple features, domains, or workstreams that need clear organizational structure for AI assistants.

---

## Why Mission-Based Organization

As projects grow, `.cursorrules` becomes a massive file. Cursor struggles with:
- Finding relevant context in 500+ line files
- Understanding which rules apply to current work
- Switching between different feature areas

**Mission-based organization solves this**: Break your project into discrete "missions" (features, domains, workstreams). Each mission gets its own reference file. Cursor can quickly navigate to relevant context.

**Example**: Instead of scrolling through one giant `.cursorrules`, you have:
- Mission 1: User onboarding flow
- Mission 2: Chat system
- Mission 3: Memory system
- Mission 4: Goal tracking
- etc.

---

## How to Set Up Mission-Based Organization

### Step 1: Create Mission Files

Create a `docs/missions/` directory:

```
project-root/
├── docs/
│   ├── missions/
│   │   ├── MISSIONS_QUICK_GUIDE.md    # Index of all missions
│   │   ├── mission_01_onboarding.md   # Detailed mission spec
│   │   ├── mission_02_chat.md
│   │   ├── mission_03_memory.md
│   │   └── ...
│   ├── PRD.md
│   └── ARCHITECTURE.md
├── .cursorrules
└── README.md
```

### Step 2: Create Mission Index (MISSIONS_QUICK_GUIDE.md)

This is the reference file Cursor checks first.

**Template**:
```markdown
# Project Missions — Quick Reference

Use this when you need to know which mission applies. Each mission has a short "when to use" and keywords.

---

## Mission 1: [Feature/Domain Name]
- **When to use:** [Specific trigger - e.g., "Support user onboarding, first-time experience"]
- **Keywords:** [Searchable terms - e.g., "onboarding, first-time user, tutorial, signup flow"]
- **Files:** [Relevant code locations - e.g., "src/features/onboarding/*, src/screens/Tutorial*"]

---

## Mission 2: [Feature/Domain Name]
- **When to use:** [Specific trigger]
- **Keywords:** [Searchable terms]
- **Files:** [Relevant code locations]

---

[Continue for all missions]
```

**Example from uploaded file**:
```markdown
## Mission 2: Post-Onboarding Chat & Advanced Orchestration
- **When to use:** Support general chat, contextual launches, notifications, chat history, goal adjustment, discovery-to-goal pipeline, goal cultivation.
- **Keywords:** general chat, contextual chat, notifications, chat history, goal adjustment, premium synthesis, discovery-to-goal, goal cultivation, context-aware conversation.
```

### Step 3: Create Detailed Mission Specs

For each mission, create a detailed spec file.

**Template** (`mission_XX_[name].md`):
```markdown
# Mission [N]: [Feature/Domain Name]

**Purpose**: [What this mission covers - 1-2 sentences]

**Status**: [Active / In Development / Planned]

---

## Overview

[Detailed description of what this mission encompasses]

---

## Key Components

**Files**:
- `src/features/[domain]/*`
- `src/screens/[screens]/*`
- `src/services/[services]/*`

**Responsibilities**:
- [What this mission handles]
- [Key functionality]
- [Integration points with other missions]

---

## Technical Requirements

**Dependencies**:
- [External services, APIs]
- [Internal services from other missions]

**Performance**:
- [Specific requirements for this mission]

**Data Models**:
```typescript
interface [KeyModel] {
  // Key data structures for this mission
}
```

---

## Implementation Patterns

**Standard approach**:
[How features in this mission should be built]

**Error handling**:
[Mission-specific error patterns]

**Testing requirements**:
[What tests are required for this mission]

---

## Integration Points

**Depends on**:
- Mission X: [What it provides]
- Mission Y: [What it provides]

**Provides to**:
- Mission Z: [What this exposes]

---

## Common Tasks

### Task: [Common scenario]
**Trigger**: [When this happens]
**Files to check**: [Where to look]
**Typical changes**: [What usually needs updating]

### Task: [Another scenario]
[Same structure]

---

## Troubleshooting

**Issue**: [Common problem]
**Cause**: [Why it happens]
**Solution**: [How to fix]

---

## References

- [Related PRD sections]
- [Architecture decisions]
- [External documentation]
```

### Step 4: Update .cursorrules to Reference Missions

**Instead of this** (everything in one file):
```
# Project Rules

## Chat System
- Use streaming for responses
- Handle SSE disconnects
- Store history in PostgreSQL
[50 more lines about chat]

## Memory System
- Extract entities on every message
- Store in memory table
- Use embeddings for recall
[50 more lines about memory]

## Goal System
[100 more lines about goals]

[500 total lines...]
```

**Do this** (lightweight with mission references):
```
# Project - Development Rules

## Overview
This project uses mission-based organization. See `docs/missions/MISSIONS_QUICK_GUIDE.md` for the mission index.

## How to Use Missions

When working on a feature or fixing a bug:
1. Check `docs/missions/MISSIONS_QUICK_GUIDE.md` to find relevant mission(s)
2. Read the detailed mission spec in `docs/missions/mission_XX_[name].md`
3. Follow patterns and requirements from that mission

## Global Standards

[Keep only truly global rules here]

### Code Quality
- TypeScript strict mode
- ESLint + Prettier
- No `any` types

### Testing
- Jest for unit tests
- React Testing Library for components
- See individual missions for domain-specific test requirements

### Error Handling
- All async operations wrapped in try-catch
- User-facing errors never expose stack traces
- Log errors with context (see mission specs for what NOT to log)

### Git
- Conventional commits: `type(scope): description`
- Reference mission number in commits: `feat(mission-02): add chat streaming`
- Atomic commits

## Mission-Specific Rules

For mission-specific patterns, testing requirements, integration points, and troubleshooting:
→ See `docs/missions/mission_XX_[name].md`

## Current Active Missions

[List currently active missions for quick reference]
- Mission 1: User Onboarding
- Mission 2: Chat System
- Mission 3: Memory System
- Mission 4: Goal Tracking
- [etc.]
```

---

## When to Use Missions

### Use mission-based organization when:

**Project has 10+ distinct features or domains**
Example: Authentication, chat, memory, goals, integrations, analytics, admin

**Multiple developers working on different areas**
Missions provide clear ownership and context boundaries

**Features have complex integration points**
Mission specs document dependencies and handoff points

**You're working with AI assistants heavily**
Cursor can quickly navigate to relevant context instead of searching one giant file

**Project will scale significantly**
Adding missions is easier than refactoring one massive rules file later

### DON'T use missions when:

**Project is small** (<5 features)
Just use a well-organized `.cursorrules` file

**Features are tightly coupled**
If everything touches everything, missions create more overhead than value

**You're the only developer**
Less benefit if you don't need coordination across teams

**Just starting MVP**
Wait until project structure stabilizes before creating missions

---

## Example: Referencing Missions in Cursor

**Scenario**: You're working on chat streaming and need to add error handling.

**Without missions** (search through `.cursorrules`):
```
You: "How should I handle streaming errors?"
Cursor: [searches 500-line .cursorrules file for error handling patterns]
Cursor: [might miss chat-specific patterns buried in the file]
```

**With missions** (targeted reference):
```
You: "I'm working on Mission 2 (Chat). How should I handle streaming errors?"
Cursor: [checks MISSIONS_QUICK_GUIDE.md]
Cursor: [finds Mission 2, reads mission_02_chat.md]
Cursor: [finds chat-specific error handling patterns]
Cursor: "Based on Mission 2 specs, streaming errors should..."
```

**In commits**:
```bash
git commit -m "feat(mission-02): add SSE reconnection logic

- Implement exponential backoff for SSE disconnects
- Store unsent messages in local queue
- Retry on connection restore
- Per Mission 2 error handling patterns"
```

---

## Mission Governance

### Creating New Missions

**When to create a new mission**:
- New major feature or domain
- Existing mission file exceeds 300 lines
- Feature has distinct integration patterns

**Process**:
1. Add entry to `MISSIONS_QUICK_GUIDE.md`
2. Create `mission_XX_[name].md` from template
3. Update `.cursorrules` to reference new mission
4. Update relevant mission files if there are new integration points

### Updating Missions

**When to update**:
- Architecture changes
- New integration points
- Common troubleshooting patterns emerge
- Technical requirements change

**Process**:
1. Update mission spec file
2. Update `MISSIONS_QUICK_GUIDE.md` if keywords or triggers change
3. Commit with `docs(mission-XX): [description]`

### Deprecating Missions

**When to deprecate**:
- Feature removed
- Missions consolidated

**Process**:
1. Mark as deprecated in `MISSIONS_QUICK_GUIDE.md`
2. Archive mission file to `docs/missions/archived/`
3. Update dependent missions

---

## Benefits We've Seen

From the uploaded example (34 missions for Coach Cedar project):

**Faster onboarding**: New developers can read relevant missions instead of entire codebase

**Better AI assistance**: Cursor gives more accurate suggestions when pointed to specific missions

**Clear ownership**: Each mission can have an owner/team responsible

**Easier refactoring**: Understand blast radius by checking mission integration points

**Better documentation**: Mission specs stay current because developers reference them constantly

**Improved commits**: Mission numbers in commits make changelog meaningful

---

## Template Files

See uploaded `MISSIONS_QUICK_GUIDE.md` for a real example from a 34-mission project (Coach Cedar).

Key elements:
- Clear "when to use" triggers
- Searchable keywords
- Direct file references where applicable
- Organized by number (Mission 1, Mission 2, etc.)

---

## Summary

**Mission-based organization is for**:
- Large projects (10+ features)
- Multiple developers
- Heavy AI assistant usage
- Complex integration patterns

**Provides**:
- Better Cursor context navigation
- Clear feature boundaries
- Documented integration points
- Easier onboarding

**Setup time**: 4-6 hours to create initial missions for existing project

**Maintenance**: Update mission specs as features evolve (ongoing)

**ROI**: Starts paying off immediately for Cursor usage, larger returns as project scales