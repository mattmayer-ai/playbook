# Product Development Playbook

**Version**: 1.0  
**Last Updated**: February 2026

A systematic approach to product development from discovery through scaling, designed for rapid setup with AI coding assistants.

---

## Overview

This playbook documents the methodology I've developed over 15 years building products in aviation (Air Canada), defense (RaceRocks), and enterprise software (Swift Racks). It separates discovery (Claude/ChatGPT) from implementation (Cursor) and emphasizes rapid validation over exhaustive research.

**The workflow**:
1. **Rapid discovery in Claude** (4-8 hours) - Pick ONE validation method, write PRD
2. **Knowledge handoff** (4-8 hours) - Package discovery for AI consumption
3. **Infrastructure setup in Cursor** (4-6 hours) - Rapid project configuration
4. **Start building** (same day) - Begin feature development with context

**Total time to first code: 12-22 hours** (not weeks)

---

## Who This Is For

**Product leaders** who need repeatable discovery and delivery rhythms.

**Founders** navigating validation to product-market fit.

**Cross-functional teams** who want clear artifacts that connect insight to implementation.

**My students at Schulich School of Business** who need practical frameworks that bridge theory and execution.

If you're measured by shipped value and learning velocity—not slide decks—this is relevant.

---

## Core Principles

**Speed of movement is linked to speed of data insights.** Four hours of focused discovery beats weeks of analysis paralysis.

**Evidence over ego.** Quick experiments (4-8 hours) beat assumptions. The 697 complaints analysis was thorough, but most projects need rapid validation, not exhaustive research.

**Customer-first thinking.** Talk to 3-5 users or run a quick experiment. Don't build in isolation.

**Standardization reduces cognitive overhead.** Same structure every project means less time deciding, more time building.

**Configuration debt compounds.** Setting up TypeScript, linting, and testing from day one is faster than retrofitting later.

**Rapid validation, then iterate.** Get to working code fast. Full validation comes after MVP, not before.

---

## The Playbook

### [Part 1: Discovery in Claude](./Part_1_Discovery_in_Claude.md)

**Purpose**: Do just enough discovery to write a solid PRD before coding.

**What you produce**:
- Discovery output: User interviews OR industry research OR quick experiment OR problem research
- Structured PRD ready for Cursor consumption

**Time**: 4-8 hours (not weeks)

**Approach**: Pick ONE validation method based on what you're uncertain about:
- **User interviews** (3-5 people, 30 min each) - if you need to understand pain points
- **Industry research** (AI-assisted) - if you need market/competitive context  
- **Quick experiment** (technical validation) - if you need to test feasibility
- **Problem research** (AI-assisted) - if you're starting from scratch

**Output**: Rapid PRD with problem statement, MVP scope, success metrics

### [Part 2: Knowledge Handoff (Claude → Cursor)](./Part_2_Knowledge_Handoff.md)

**Purpose**: Package discovery output for implementation.

**What you create**:
- PRD.md (product requirements)
- CONTEXT.md (domain knowledge)
- CONSTRAINTS.md (technical/compliance limits)
- ARCHITECTURE.md (key decisions)
- .cursorrules (coding patterns)

**Time**: 4-8 hours

**Why it matters**: Cursor is only as effective as the context you provide. Good handoff means correct assumptions about architecture, security, compliance, and user needs.

### [Part 3: Infrastructure Setup in Cursor](./Part_3_Infrastructure_Setup.md)

**Purpose**: Rapidly configure projects for scalable development.

**What you set up**:
- Repository (Git, .gitignore)
- TypeScript (strict mode, path aliases)
- Code quality (ESLint, Prettier)
- Folder structure (standardized)
- Environment variables (template pattern)
- Testing (Jest, coverage)

**Time**: 4-6 hours

**Key frameworks**:
- Platform choice (web vs mobile)
- Backend choice (BaaS vs custom)
- Database choice (document vs relational)
- State management (server vs client)
- Compliance patterns (HIPAA, PCI-DSS)

### [Part 4: Iteration and Scaling](./Part_4_Iteration_and_Scaling.md)

**Purpose**: Handle pivots, refactoring, and infrastructure evolution.

**What you learn**:
- When to pivot vs kill (decision framework)
- How to execute pivots (keep validated learnings)
- Refactor vs start fresh (decision criteria)
- When to scale (performance, cost, reliability signals)
- Migration patterns (BaaS → AWS, monolith → services)

**Key case studies**:
- TakeCost: Accuracy → Speed pivot (85% adoption)
- EdPal: VR → AI pivot (complete restart)
- Air Canada: BaaS → Custom backend (gradual migration)

---

## Appendices

### [Appendix A: Cursor Setup with Mission-Based Organization](./Appendix_A_Cursor_Missions.md)

**When to use**: Large projects (10+ features) that need clear organizational structure for AI assistants.

**What you'll learn**:
- Mission-based organization pattern
- How to structure `docs/missions/` directory
- Creating mission index (MISSIONS_QUICK_GUIDE.md)
- Detailed mission specifications
- Lightweight .cursorrules that reference missions

**Benefits**:
- Faster Cursor context navigation
- Clear feature boundaries
- Better AI assistance at scale
- Easier onboarding for new developers

**Setup time**: 4-6 hours for initial mission structure

### [Appendix B: MCP Configuration for Rapid Development](./Appendix_B_MCP_Configuration.md)

**When to use**: Need Cursor to interact with external systems (databases, Docker, GitHub) or enhanced reasoning.

**What you'll learn**:
- Essential MCPs for product development
- Docker MCP (container debugging)
- GitHub MCP (issue/PR context)
- Sequential-thinking MCP (complex reasoning)
- PostgreSQL MCP (database inspection)
- Security best practices

**Configuration examples**:
- Minimal setup (Docker + Sequential-thinking)
- Full development setup (all 4 MCPs)
- Environment variable management

**Setup time**: 15-30 minutes for basic config

**ROI**: 30-60 minutes saved daily through reduced context switching

---

## Quick Start

### If you have an idea but no validation:

Start with **[Part 1: Discovery in Claude](./Part_1_Discovery_in_Claude.md)**

**Rapid process (4-8 hours)**:
1. Pick ONE validation method (1 hour)
   - User interviews OR industry research OR quick experiment OR problem research
2. Execute discovery (2-5 hours)
   - AI-assisted research, quick interviews, or technical test
3. Write PRD (1-2 hours)
   - Structure findings for Cursor

**Don't overthink it.** Four hours of focused discovery beats weeks of analysis paralysis. Build fast, learn fast.

### If you have a validated PRD:

Start with **[Part 2: Knowledge Handoff](./Part_2_Knowledge_Handoff.md)**

Create the knowledge package:
1. PRD.md (use the template)
2. CONTEXT.md (domain knowledge)
3. CONSTRAINTS.md (technical limits)
4. .cursorrules (coding patterns)

Then proceed to **[Part 3: Infrastructure Setup](./Part_3_Infrastructure_Setup.md)**.

### If you're mid-project and need to pivot:

Start with **[Part 4: Iteration and Scaling](./Part_4_Iteration_and_Scaling.md)**

Follow the pivot framework:
1. Identify what to keep (validated learnings)
2. Update documentation first
3. Feature flag the pivot
4. Measure the pivot

---

## Supporting Documents

### Analysis and Context

**[Playbook Analysis](./Playbook_Analysis.md)** - What works, what doesn't, what's missing in existing approaches

### Technical Guides

**[Project Setup Technical Guide](./Project_Setup_Technical_Guide.md)** - My standard approach to project setup (tool-agnostic)

### Product Innovation

**[Product Innovation Playbook](./Product_Innovation_Playbook_Rewritten.md)** - The conceptual framework that precedes technical implementation

### Cursor Enhancement

**[Appendix A: Mission-Based Organization](./Appendix_A_Cursor_Missions.md)** - Advanced Cursor setup for large projects (10+ features)

**[Appendix B: MCP Configuration](./Appendix_B_MCP_Configuration.md)** - Configure Model Context Protocol for Docker, GitHub, databases, and enhanced reasoning

### Quick Reference

**[Discovery Prompts Quick Reference](./Discovery_Prompts_Quick_Reference.md)** - All AI prompts in one place for rapid copy-paste

---

## Real-World Applications

### Aviation (Air Canada, 2010-2018)
- Analyzed 697 pilot complaints to understand real needs
- Built offline iPad training platform
- Delivered $1.5M annual savings, 70% friction reduction

### Defense (RaceRocks, 2018-2024)
- Developed world's first RAS naval simulator
- Zero-tolerance reliability requirements
- Delivered $20M+ operational savings

### Enterprise Software (Swift Racks, 2024-Present)
- Leading AI platform development (CNS, TakeCost, EdPal)
- 85% efficiency improvements through AI
- $1.8M recurring revenue growth

### Education (Schulich School of Business)
- Teaching product management frameworks
- Students report 85%+ industry placement rate
- Frameworks used in real-world job interviews

---

## Key Lessons Learned

**From Air Canada**: Speed of movement is linked to speed of data insights. The 697 complaints analysis was thorough, but most projects need rapid validation (4-8 hours), not exhaustive research.

**From RaceRocks**: Zero-tolerance reliability is transferable. Compliance frameworks from regulated industries create discipline even in fast-moving projects.

**From Swift Racks**: Customer-first thinking beats tech novelty. Quick experiments (2-4 hours) reveal what users actually need vs what they say they need.

**From Schulich**: Teaching forces clarity. Frameworks must be simple enough to explain in one class session—otherwise they won't get used.

---

## When to Deviate

This playbook provides frameworks, not rules. Deviate when:

1. **Client has existing infrastructure** - Match their stack and conventions
2. **Regulated industry requires specific tools** - Use approved vendors
3. **Performance constraints** - Optimize for specific bottlenecks
4. **Team expertise** - Leverage team's strengths over my preferences

**The principle holds**: Standardize what you can. Deviate deliberately, not accidentally.

---

## Contributing

This playbook evolves as I learn. Current version reflects patterns that worked in aviation (8 years), defense (6 years), and enterprise software (current).

Updates happen when:
- New patterns prove valuable across multiple projects
- Technology shifts require updated frameworks
- Student feedback reveals unclear sections

---

## About Me

I'm a product leader with 15+ years shipping software across aviation, defense, and enterprise SaaS. I teach Product Management at Schulich School of Business.

**Technical fluency**: AWS Bedrock, Claude Sonnet multi-agent orchestration, RAG implementation, computer vision, Spring Boot, Next.js, React

**Strategic judgment**: Build vs buy frameworks, compliance architecture, governance frameworks, cross-functional coalition building

**Contact**: [LinkedIn](https://linkedin.com/in/mattmayer) | matt@example.com

---

## License

This playbook is provided as-is for educational and professional use. Adapt it to your context.

---

*Last modified: February 2026*