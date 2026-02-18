# Innovation Playbook

**Version**: 1.0\
**Last Updated**: February 2026

A systematic approach to product development from discovery through scaling, designed for rapid setup with AI coding assistants.

***

## Overview

This playbook documents the methodology I've developed over 15 years building products in aviation (Air Canada), defense (RaceRocks), and enterprise software (Swift Racks). It separates discovery (Claude/ChatGPT) from implementation (Cursor) and emphasizes rapid validation over exhaustive research.

**The workflow:**

* **Rapid discovery** (2-8 hours) - Pick ONE validation method, write PRD
* **Knowledge handoff** (2-6 hours) - Package discovery for AI consumption
* **Infrastructure setup in Cursor** (2-4 hours) - Rapid project configuration
* **Start building** (same day) - Begin feature development with context

**Total time to first code: 6-18 hours** (not weeks)

***

## Who This Is For

* Product leaders who need repeatable discovery and delivery rhythms.
* Founders navigating validation to product-market fit.
* Cross-functional teams who want clear artifacts that connect insight to implementation.
* My students at Schulich School of Business who need practical frameworks that bridge theory and execution.

If you're measured by shipped value and learning velocity—not slide decks—this is relevant.

***

## Core Principles

* Speed of movement is linked to speed of data insights. Four hours of focused discovery beats weeks of analysis paralysis.
* Evidence over ego. Quick experiments (2-8 hours) beat assumptions. The 697 complaints analysis was thorough, but most projects need rapid validation, not exhaustive research.
* Customer-first thinking. Talk to 3-5 users or run a quick experiment. Don't build in isolation.
* Standardization reduces cognitive overhead. Same structure every project means less time deciding, more time building.
* Configuration debt compounds. Setting up TypeScript, linting, and testing from day one is faster than retrofitting later.
* Rapid validation, then iterate. Get to working code fast. Full validation comes after MVP, not before.

***

## The Playbook

### [Part 1: Discovery](innovation-playbook/part_1_discovery_in_claude.md)

Purpose: Do just enough discovery to write a solid PRD before coding.

What you produce:

* Discovery output: User interviews OR industry research OR quick experiment OR problem research
* Structured PRD ready for Cursor consumption

Time: 4-8 hours (not weeks)

Approach: Pick ONE validation method based on what you're uncertain about:

* User interviews (3-5 people, 30 min each) - if you need to understand pain points
* Industry research (AI-assisted) - if you need market/competitive context
* Quick experiment (technical validation) - if you need to test feasibility
* Problem research (AI-assisted) - if you're starting from scratch

Output: Rapid PRD with problem statement, MVP scope, success metrics

### [Part 2: Knowledge Handoff (Claude → Cursor)](innovation-playbook/part_2_knowledge_handoff.md)

Purpose: Package discovery output for implementation.

What you create:

* PRD.md (product requirements)
* CONTEXT.md (domain knowledge)
* CONSTRAINTS.md (technical/compliance limits)
* ARCHITECTURE.md (key decisions)
* .cursorrules (coding patterns)

Time: 4-8 hours

Why it matters: Cursor is only as effective as the context you provide. Good handoff means correct assumptions about architecture, security, compliance, and user needs.

### [Part 3: Infrastructure Setup in Cursor](innovation-playbook/part_3_infrastructure_setup.md)

Purpose: Rapidly configure projects for scalable development.

What you set up:

* Repository (Git, .gitignore)
* TypeScript (strict mode, path aliases)
* Code quality (ESLint, Prettier)
* Folder structure (standardized)
* Environment variables (template pattern)
* Testing (Jest, coverage)

Time: 4-6 hours

Key frameworks:

* Platform choice (web vs mobile)
* Backend choice (BaaS vs custom)
* Database choice (document vs relational)
* State management (server vs client)
* Compliance patterns (HIPAA, PCI-DSS)

### [Part 4: Iteration and Scaling](innovation-playbook/part_4_iteration_and_scaling.md)

Purpose: Handle pivots, refactoring, and infrastructure evolution.

What you learn:

* When to pivot vs kill (decision framework)
* How to execute pivots (keep validated learnings)
* Refactor vs start fresh (decision criteria)
* When to scale (performance, cost, reliability signals)
* Migration patterns (BaaS → AWS, monolith → services)

Key case studies:

* TakeCost: Accuracy → Speed pivot (85% adoption)
* EdPal: VR → AI pivot (complete restart)
* Air Canada: BaaS → Custom backend (gradual migration)

***

## Appendices

### [Appendix A: Cursor Setup with Mission-Based Organization](supporting-docs/appendix_a_cursor_missions.md)

When to use: Large projects (10+ features) that need clear organizational structure for AI assistants.

What you'll learn:

* Mission-based organization pattern
* How to structure `docs/missions/` directory
* Creating mission index (MISSIONS\_QUICK\_GUIDE.md)
* Detailed mission specifications
* Lightweight .cursorrules that reference missions

Benefits:

* Faster Cursor context navigation
* Clear feature boundaries
* Better AI assistance at scale
* Easier onboarding for new developers

Setup time: 4-6 hours for initial mission structure

### [Appendix B: MCP Configuration for Rapid Development](supporting-docs/appendix_b_mcp_configuration.md)

When to use: Need Cursor to interact with external systems (databases, Docker, GitHub) or enhanced reasoning.

What you'll learn:

* Essential MCPs for product development
* Docker MCP (container debugging)
* GitHub MCP (issue/PR context)
* Sequential-thinking MCP (complex reasoning)
* PostgreSQL MCP (database inspection)
* Security best practices

Configuration examples:

* Minimal setup (Docker + Sequential-thinking)
* Full development setup (all 4 MCPs)
* Environment variable management

Setup time: 15-30 minutes for basic config

ROI: 30-60 minutes saved daily through reduced context switching

***

## Quick Start

### If you have an idea but no validation:

Start with [Part 1: Rapid Discovery](innovation-playbook/part_1_discovery_in_claude.md)

Rapid process (4-8 hours):

{% stepper %}
{% step %}
### Pick ONE validation method (≈1 hour)

Choose one:

* User interviews
* Industry research
* Quick experiment
* Problem research
{% endstep %}

{% step %}
### Execute discovery (≈2–5 hours)

Run the chosen method: AI-assisted research, quick interviews, or a technical test.
{% endstep %}

{% step %}
### Write PRD (≈1–2 hours)

Structure findings for Cursor: problem statement, MVP scope, success metrics.
{% endstep %}
{% endstepper %}

Don't overthink it. Four hours of focused discovery beats weeks of analysis paralysis. Build fast, learn fast.

### If you have a validated PRD:

Start with [Part 2: Knowledge Handoff](innovation-playbook/part_2_knowledge_handoff.md)

Create the knowledge package:

* PRD.md (use the template)
* CONTEXT.md (domain knowledge)
* CONSTRAINTS.md (technical limits)
* .cursorrules (coding patterns)

Then proceed to [Part 3: Infrastructure Setup](innovation-playbook/part_3_infrastructure_setup.md).

### If you're mid-project and need to pivot:

Start with [Part 4: Iteration and Scaling](innovation-playbook/part_4_iteration_and_scaling.md)

Follow the pivot framework:

{% stepper %}
{% step %}
### Identify what to keep

Preserve validated learnings and data.
{% endstep %}

{% step %}
### Update documentation first

Reflect decisions in PRD, CONTEXT, and ARCHITECTURE docs.
{% endstep %}

{% step %}
### Feature flag the pivot

Deploy changes behind flags to control exposure.
{% endstep %}

{% step %}
### Measure the pivot

Track metrics to validate the new direction.
{% endstep %}
{% endstepper %}

***

## Supporting Documents

### Cursor Enhancement

[Appendix A: Mission-Based Organization](supporting-docs/appendix_a_cursor_missions.md) - Advanced Cursor setup for large projects (10+ features)

[Appendix B: MCP Configuration](supporting-docs/appendix_b_mcp_configuration.md) - Configure Model Context Protocol for Docker, GitHub, databases, and enhanced reasoning

### Quick Reference

[Discovery Prompts Quick Reference](supporting-docs/) - All AI prompts in one place for rapid copy-paste

***

## Real-World Applications

### Aviation (Air Canada, 2010-2018)

* Analyzed 697 pilot complaints to understand real needs
* Built offline iPad training platform
* Delivered $1.5M annual savings, 70% friction reduction

### Defense (RaceRocks, 2018-2024)

* Developed world's first RAS naval simulator
* Zero-tolerance reliability requirements
* Delivered $20M+ operational savings

### Enterprise Software (Swift Racks, 2024-Present)

* Leading AI platform development ([Swift CNS](https://swiftcns.ai/), [TakeCost,](https://takecost.com) [EdPal](https://edpal.ca/), [PaySight](https://paysight.ca/), LearnMate AI)
* 85% efficiency improvements through AI
* $1.8M recurring revenue growth

### Education (Schulich School of Business)

* Teaching product management frameworks
* Students report 85%+ industry placement rate
* Frameworks used in real-world job interviews

### Personal Projects

Beyond professional work, I build products that solve problems I care about:

* **AthleteAtlas** - Youth hockey development platform. Unified ecosystem connecting coaches, trainers, parents, and athletes through transparent progress tracking and dual-layer assessments.
* **CoachCedar** - Peronalized fitness coach combining industry expertise with personalized training plans. Validates the intersection of AI and human coaching wisdom.
* **Edison** - Experimentation and insights platform. Single source of truth for team experiments.
* **mwm chatbot** - A Fun personal AI assistant trained on my career corpus. Demonstrates RAG implementation; stood up in 48 hrs.

These projects let me experiment with emerging technologies (multi-agent AI, RAG, computer vision) while solving real problems. Building in public keeps me connected to users and validates that the frameworks I teach actually work outside enterprise contexts. **Product development isn't just my profession—it's how I learn, experiment, and stay sharp.**

* [AthleteAtlas](https://athleteatlas.io), [CoachCedar](https://coachcedar.com), [mwm chatbot](https://askmwm.web.app/), [Edison](https://edison-mvp.firebaseapp.com/)

***

## Key Lessons Learned

* **Keep your ear to the ground, listen to your end-users -** I logged 697 complaints personally at Air Canada because summaries hide truth. Dashboards aggregate the noise away, but real insights live in what users actually write. Keep your finger on the pulse.
* **Validate all assumptions -** We all have blinders. Talk to users. Go outside your organization. Your assumptions are probably wrong. Find out how wrong, adjust course.
* **Speed of insight drives speed of execution -** Choose rapid validation over exhaustive research. Most projects need 4-8 hours of focused discovery, not weeks. The faster you gather data, the faster you can move.&#x20;
* **Fail fast, learn faster -** TakeCost spent 2 years building for accuracy when users wanted speed. EdPal built VR when users needed AI lesson planning. Both pivoted successfully because we caught mistakes early and adjusted. Failure is fine. Slow failure is expensive.
* **Discipline from regulated industries transfers everywhere -** Zero-tolerance reliability in aviation and defense creates habits that serve you in fast-moving projects. Build for longevity from day one—it's easier than retrofitting later.
* **Serve outcomes, not technology -** I've recommended against AI when simpler solutions delivered better value. The technology should serve the outcome, not the other way around. Customer-first thinking always wins.
* **Clarity enables scale -** If you can't explain a framework in one class session, it won't get used. Complexity doesn't scale. Simplicity does.
* **Build for scale on day one -** Standardized infrastructure, TypeScript strict mode, clear architecture from the start. Retrofitting discipline is 10x harder and slower than starting with it.

***

## When to Deviate

This playbook provides frameworks, not rules. Deviate when:

* Client has existing infrastructure - Match their stack and conventions
* Regulated industry requires specific tools - Use approved vendors
* Performance constraints - Optimize for specific bottlenecks
* Team expertise - Leverage team's strengths over my preferences

The principle holds: Standardize what you can. Deviate deliberately, not accidentally.

***

## Contributing

This playbook evolves as I learn. Current version reflects patterns that worked in aviation (8 years), defense (6 years), and enterprise software (current).

Updates happen when:

* New patterns prove valuable across multiple projects
* Technology shifts require updated frameworks
* Student feedback reveals unclear sections

***

## About Me

I'm a product leader with 15+ years shipping software across aviation, defense, and enterprise SaaS. I teach Product Management at Schulich School of Business.

Technical fluency: AWS Bedrock, Claude Sonnet multi-agent orchestration, RAG implementation, computer vision, Spring Boot, Next.js, React

Strategic judgment: Build vs buy frameworks, compliance architecture, governance frameworks, cross-functional coalition building

Contact: [LinkedIn](https://linkedin.com/in/mattmayer) | mattmayer@hotmail.com

***

## License

This playbook is provided as-is for educational and professional use. Adapt it to your context.

***

_Last modified: February 2026_
