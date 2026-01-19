# How to Use the Focused Documentation Skill

This skill activates automatically for any documentation task. No special invocation needed - just ask for documentation help.

## Example Invocations

### Example 1: New Project Documentation

**Request**:
"Create a documentation structure for a new user authentication service. Include: system purpose, functional requirements, architecture design, and security constraints."

**What You'll Get**:
```
docs/
├── README.md                    (Project documentation overview)
├── overview/
│   ├── README.md                (Main overview - why this service exists)
│   └── scope.md                 (What's included/excluded)
├── requirements/
│   ├── README.md                (Requirements overview)
│   ├── functional.md            (What the system must do)
│   ├── security.md              (Security requirements)
│   └── constraints.md           (Limitations)
└── architecture/
    ├── README.md                (Architecture overview)
    ├── components.md            (System components)
    └── security-design.md       (Security architecture)
```

---

### Example 2: Restructure Existing Documentation

**Request**:
"This README is over 3000 lines and covers everything from architecture to deployment. Break it into focused, single-responsibility files with a clear directory structure."

**What You'll Get**:
- Analysis of current documentation structure
- Proposed new file organization using README.md pattern
- Individual .md files with clear responsibilities
- Each directory has README.md as main content
- NO internal links - structure is self-explanatory through names
- Natural language descriptions without code pollution

---

### Example 3: Requirements Documentation

**Request**:
"Create modular requirements documentation for an e-commerce checkout system. Separate functional requirements, non-functional requirements, payment processing rules, and compliance constraints into individual files."

**What You'll Get**:
```
docs/requirements/
├── README.md                    (Requirements overview)
├── functional/
│   ├── README.md                (Functional requirements overview)
│   ├── cart-management.md
│   ├── payment-processing.md
│   └── order-fulfillment.md
├── non-functional/
│   ├── README.md                (Non-functional requirements overview)
│   ├── performance.md
│   ├── availability.md
│   └── security.md
└── compliance/
    ├── README.md                (Compliance requirements overview)
    ├── pci-dss.md
    └── data-privacy.md
```

---

### Example 4: Architecture Documentation

**Request**:
"Document our microservices architecture—describe the service boundaries, communication patterns, and data flow. Focus on the conceptual design."

**What You'll Get**:
```
docs/architecture/
├── README.md                    (Architecture overview)
├── services/
│   ├── README.md                (Services overview)
│   ├── user-service.md
│   ├── order-service.md
│   └── payment-service.md
├── communication/
│   ├── README.md                (Communication patterns overview)
│   ├── sync-patterns.md
│   └── async-patterns.md
└── data-flow/
    ├── README.md                (Data flow overview)
    └── event-sourcing.md
```

All in natural language without implementation code.

---

### Example 5: Decision Documentation (ADRs)

**Request**:
"Create an Architecture Decision Record for why we chose PostgreSQL over MongoDB for our primary database. Include context, options considered, decision rationale, and consequences."

**What You'll Get**:

File: `docs/decisions/database-selection.md`
```markdown
# Database Technology Selection

**Purpose**: Documents the decision to use PostgreSQL as the primary database.

**Audience**: Engineering team, future maintainers

---

**Status**: Approved
**Date**: 2026-01-19
**Decision Makers**: Engineering Team

## Context

[Natural language description of the situation requiring a decision]

## Options Considered

### PostgreSQL
- Strengths: ...
- Weaknesses: ...

### MongoDB
- Strengths: ...
- Weaknesses: ...

## Decision

[Natural language explanation of why PostgreSQL was chosen]

## Consequences

**Positive**:
- [List of benefits]

**Negative**:
- [List of trade-offs]
```

Note: No "Related" links section - related decisions are co-located in `docs/decisions/` directory.

---

## What to Provide

When requesting documentation, just describe what you need. The skill activates automatically.

**Minimum Information**:
- What needs to be documented (project, feature, system, process, decision)
- Key topics to cover

**Helpful Additional Context**:
- Target audience (developers, stakeholders, AI tools)
- Existing documentation (to avoid duplication)
- Specific constraints (compliance, organizational standards)
- Project type or domain
- Complexity level (small/medium/large project)

**Don't Worry About**:
- Exact file names (the skill will suggest appropriate names)
- Directory structure (the skill will propose an optimal hierarchy using README.md pattern)
- Writing style (the skill follows best practices automatically)
- Mentioning "focused" or invoking the skill - it applies automatically

---

## What You'll Get

**Documentation Structure**:
- Well-organized directory hierarchy
- README.md as main content in each directory
- Meaningful file and folder names (no links needed)
- Single-responsibility files
- Navigable by browsing the file tree alone

**Documentation Content**:
- Purpose statement for each file
- Natural language descriptions (no code snippets)
- Concise, scannable paragraphs (3-5 sentences)
- Bullet lists for clarity
- Tables for comparisons and specifications
- NO internal links between files

**Documentation Quality**:
- AI tool optimized (focused context, efficient retrieval)
- Modular and composable (easy to extend)
- Purpose-driven (not template-based boilerplate)
- Maintainable (clear boundaries, easy updates)
- Link-free (no stale references to maintain)

---

## Tips for Best Results

1. **Be specific about scope** - "Authentication requirements" is better than "All requirements"

2. **Mention your audience** - Documentation for developers differs from documentation for executives

3. **Specify if restructuring** - Let Claude know you have existing docs that need reorganization

4. **Indicate project size** - Small projects need simpler structures than large enterprise systems

5. **Iterate incrementally** - Start with structure, then refine individual files

6. **Trust the naming** - If you can't find something by browsing directory/file names, the names need improvement

---

## Common Use Cases

**Project Kickoff**:
"Create initial documentation structure for a new [project type] covering [key areas]"

**Documentation Cleanup**:
"Restructure this monolithic documentation into focused, modular files"

**Requirements Gathering**:
"Generate requirements documentation template for [domain/project]"

**Architecture Documentation**:
"Document the architecture of [system] focusing on [aspects] without code examples"

**Decision Logging**:
"Create an ADR for [decision] documenting context, options, and rationale"

**Workflow Documentation**:
"Document the [process/workflow] from [start] to [end] in natural language"

---

## What Makes This Skill Unique

Unlike traditional documentation approaches:

- **Auto-activating** - No need to invoke or mention the skill
- **No code pollution** - Pure natural language descriptions
- **No links** - Discoverability through file/directory names only
- **README.md pattern** - Each directory's main content in README.md
- **AI tool optimized** - Structured for efficient context retrieval
- **Single responsibility** - Each file has one clear purpose
- **Modular by design** - Easy to compose, extend, and maintain

This skill is perfect for creating documentation that both humans and AI coding assistants can easily navigate by browsing the file tree.
