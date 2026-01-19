---
name: focused-docs
description: Creates structured, modular documentation with single-responsibility files using natural language to avoid code snippet pollution for AI tools
alwaysApply: true
---

# Focused Documentation Builder

This skill automatically applies to ALL documentation tasks. Whenever creating, editing, or restructuring any documentation (.md files, README, specs, guides), follow these principles.

## Core Philosophy

**Structure over Snippets**: Documentation describes WHAT to do in clear natural language, not HOW with code examples. This prevents:
- Code snippet pollution that confuses AI coding tools
- Premature implementation details that become outdated
- Context noise that reduces AI tool efficiency

**Discoverability Through Names Only**: Documentation must be navigable purely through file and directory names.
- NO links between documents (links become stale and create maintenance burden)
- Directory names provide context for their contents
- File names clearly indicate single responsibility
- A reader should find what they need by browsing the file tree alone

**README.md as Directory Index**: Each directory's main content lives in `README.md`.
- Parent directory name provides the topic context
- README.md contains the overview/main content for that topic
- Supporting files in the same directory have single-responsibility names
- Example: `authentication/README.md` = main authentication docs, `authentication/oauth-flow.md` = OAuth-specific details

**Modular Architecture**: Each documentation file has one clear responsibility, making it easy for AI tools to:
- Locate relevant context quickly
- Understand scope boundaries
- Navigate documentation hierarchies efficiently

## Capabilities

- **Directory Structure Design**: Creates logical, scalable folder hierarchies from day one
- **File Naming Standards**: Generates meaningful, descriptive file names that communicate purpose
- **Single Responsibility Files**: Ensures each .md file addresses one specific concern
- **Purpose-Driven Sections**: Organizes content by documentation goals, not boilerplate templates
- **Natural Language Focus**: Describes requirements, architecture, and design without code examples
- **AI Tool Optimization**: Structures documentation for efficient context retrieval by AI assistants
- **Modular Composition**: Designs documentation that can be composed, referenced, and extended

## Input Requirements

To generate focused documentation, provide:

**Required Context**:
- **Documentation purpose**: What this documentation will be used for (project overview, architecture, requirements, etc.)
- **Target audience**: Who will read this (developers, stakeholders, AI tools, all of the above)
- **Scope**: What areas need to be documented (features, architecture, workflows, decisions, etc.)

**Optional Context**:
- **Project type**: Software, infrastructure, research, business process, etc.
- **Existing documentation**: What documentation already exists (to ensure non-duplication)
- **Special constraints**: Compliance requirements, organizational standards, specific terminology
- **Integration needs**: Links to external systems, APIs, or documentation

**Format Accepted**:
- Natural language description of documentation needs
- Bullet points of topics to cover
- Questions you want documentation to answer
- Existing documentation that needs restructuring

## Output Formats

The skill generates:

**Directory Structure** (README.md as index pattern):
```
docs/
├── README.md                (Project documentation overview)
├── overview/
│   ├── README.md            (Why this project exists - main overview)
│   ├── goals.md             (What we aim to achieve)
│   └── scope.md             (What's included/excluded)
├── architecture/
│   ├── README.md            (Architecture overview)
│   ├── principles.md        (Design principles)
│   ├── components.md        (System components)
│   └── interactions.md      (How components work together)
├── requirements/
│   ├── README.md            (Requirements overview)
│   ├── functional.md        (What the system must do)
│   ├── non-functional.md    (Performance, security, etc.)
│   └── constraints.md       (Limitations and boundaries)
└── decisions/
    ├── README.md            (Decision log overview)
    ├── database-selection.md
    └── api-framework.md
```

**Key Pattern**: Each directory has:
- `README.md` = main content for that topic (directory name tells you what it's about)
- Supporting `.md` files = single-responsibility details

**Documentation Files**:
- **Markdown format** (.md files)
- **Clear headings** (H1 for file title, H2 for major sections, H3 for subsections)
- **Concise paragraphs** (3-5 sentences maximum)
- **Bullet lists** (for requirements, features, options)
- **Tables** (for comparisons, specifications, criteria)
- **Natural language** (no code snippets, pseudocode only if essential)
- **NO LINKS** (file/directory names must be self-explanatory)

**Documentation Metadata**:
- File purpose statement at top
- Last updated date
- Status (draft, in-review, approved, archived)
- NO "Related documents" links - use co-location instead

## How to Use

This skill activates automatically for any documentation task. No special invocation needed.

**Example Requests** (skill applies automatically):

1. "Create documentation for a new microservices architecture project. Cover: system overview, service boundaries, communication patterns, and deployment strategy."

2. "Generate requirements documentation for an e-commerce platform. Include: user workflows, business rules, payment processing requirements, and security constraints."

3. "Restructure this monolithic README into modular documentation files organized by concern."

4. "Create architecture documentation that describes our system components and their interactions."

5. "I need to document our API design decisions."

6. "Help me write a README for this project."

## Documentation Principles

### 1. Single Responsibility Per File

**Good**:
- `authentication-requirements.md` - Only authentication requirements
- `api-design-principles.md` - Only API design principles
- `deployment-workflow.md` - Only deployment process

**Bad**:
- `technical-documentation.md` - Too broad, multiple concerns
- `everything-you-need-to-know.md` - Violates single responsibility

### 2. Meaningful File Names (Discoverability Without Links)

File and directory names must be self-explanatory. A reader navigates by browsing the tree, not clicking links.

**Good Patterns**:
- `[topic]/README.md` → `authentication/README.md` (main auth docs)
- `[topic]/[specific-concern].md` → `authentication/oauth-flow.md`
- `[topic]/[specific-concern].md` → `authentication/session-management.md`

**Bad Patterns**:
- `doc1.md`, `notes.md`, `misc.md` - Not descriptive
- `important-stuff.md` - Too vague
- Relying on links to explain what files contain

### 3. Purpose-Driven Sections

Each file starts with:
```markdown
# [Clear Title]

**Purpose**: [One sentence explaining why this file exists]

**Audience**: [Who should read this]

---

[Content organized by purpose, not template]
```

Note: NO "Related" links section. Related content should be co-located in the same directory or have obvious directory names.

### 4. Natural Language, No Code

**Instead of**:
```markdown
## Authentication Flow

```python
def authenticate(user, password):
    if validate(password):
        return create_token(user)
```
```

**Write**:
```markdown
## Authentication Flow

The system validates user credentials against the secure storage mechanism. Upon successful validation, it generates a time-limited authentication token with appropriate permission scopes. Failed attempts are logged and rate-limited to prevent brute force attacks.
```

### 5. Hierarchical Organization (README.md Pattern)

**Levels**:
1. **Top level** (`docs/README.md`) - Project documentation overview
2. **Category level** (`docs/architecture/README.md`) - Main content for that category
3. **Detail level** (`docs/architecture/data-flow.md`) - Specific single-responsibility topics

**Directory = Topic, README.md = Main Content**:
- `authentication/` directory tells you the topic
- `authentication/README.md` contains the main authentication documentation
- `authentication/oauth-flow.md` contains OAuth-specific details
- `authentication/jwt-tokens.md` contains JWT-specific details

**NO Cross-Reference Links**:
- Do NOT link between files
- Co-locate related content in the same directory
- Use clear directory/file names so readers can navigate by browsing

## Best Practices

### For Project Documentation

1. **Start with structure** - Design the directory hierarchy before writing content
2. **Define file boundaries** - Each file should answer specific questions
3. **Use consistent naming** - Establish naming conventions early
4. **Write for AI tools** - Keep context focused and scannable
5. **Update incrementally** - Small, focused updates to specific files

### For Requirements Documentation

1. **Separate concerns** - Functional, non-functional, constraints in separate files
2. **Use declarative language** - "The system shall..." not "The system should maybe..."
3. **Avoid implementation** - Describe WHAT, not HOW
4. **Include success criteria** - How will we know when it's complete?
5. **Track dependencies** - Note relationships between requirements

### For Architecture Documentation

1. **Describe components** - What they are, their responsibilities, their boundaries
2. **Explain interactions** - How components communicate, data flow, protocols
3. **Document principles** - The "why" behind design decisions
4. **Note trade-offs** - What was considered and why choices were made
5. **Keep current** - Update as architecture evolves

### For Decision Documentation

1. **Record context** - What was the situation?
2. **List options** - What alternatives were considered?
3. **Explain choice** - Why this option was selected
4. **Note consequences** - What are the implications?
5. **Date decisions** - When was this decided?

## File Organization Templates

### Small Project (< 10 files)

```
docs/
├── README.md              (Project documentation overview)
├── purpose.md             (Why this exists)
├── requirements.md        (What it must do)
├── architecture.md        (How it's designed)
└── workflows.md           (How it's used)
```

### Medium Project (10-30 files)

```
docs/
├── README.md                    (Project documentation overview)
├── overview/
│   ├── README.md                (Main overview content)
│   ├── goals.md
│   └── stakeholders.md
├── requirements/
│   ├── README.md                (Requirements overview)
│   ├── functional.md
│   ├── non-functional.md
│   └── constraints.md
├── architecture/
│   ├── README.md                (Architecture overview)
│   ├── components.md
│   ├── data-model.md
│   └── integrations.md
└── workflows/
    ├── README.md                (Workflows overview)
    ├── user-workflows.md
    └── admin-workflows.md
```

### Large Project (30+ files)

```
docs/
├── README.md                    (Project documentation overview)
├── overview/
│   ├── README.md                (Main overview)
│   ├── goals.md
│   ├── scope.md
│   └── stakeholders.md
├── requirements/
│   ├── README.md                (Requirements overview)
│   ├── functional/
│   │   ├── README.md            (Functional requirements overview)
│   │   ├── authentication.md
│   │   ├── authorization.md
│   │   └── data-management.md
│   ├── non-functional/
│   │   ├── README.md            (Non-functional requirements overview)
│   │   ├── performance.md
│   │   ├── security.md
│   │   └── scalability.md
│   └── constraints.md
├── architecture/
│   ├── README.md                (Architecture overview)
│   ├── principles.md
│   ├── components/
│   │   ├── README.md            (Components overview)
│   │   ├── api-layer.md
│   │   ├── business-logic.md
│   │   └── data-layer.md
│   ├── data-model.md
│   └── integrations/
│       ├── README.md            (Integrations overview)
│       ├── external-apis.md
│       └── third-party-services.md
├── decisions/
│   ├── README.md                (Decision log overview)
│   ├── database-choice.md
│   ├── api-framework.md
│   └── deployment-strategy.md
└── workflows/
    ├── README.md                (Workflows overview)
    ├── user-workflows/
    │   ├── README.md
    │   └── [specific-workflow].md
    └── admin-workflows/
        ├── README.md
        └── [specific-workflow].md
```

## Limitations

**This skill does NOT**:
- Generate code examples or implementation snippets
- Create API documentation with code samples (use API documentation tools instead)
- Generate inline code comments (use language-specific documentation generators)
- Write tutorial-style "how to code" documentation
- Create boilerplate template documentation without context

**This skill IS for**:
- Requirements documentation
- Architecture and design documentation
- Process and workflow documentation
- Decision logs and ADRs (Architecture Decision Records)
- Project overview and planning documentation
- Specification documents

**When NOT to use**:
- API reference documentation (use Swagger/OpenAPI instead)
- Code documentation (use JSDoc, Sphinx, etc.)
- Tutorial content with code examples
- Quick reference guides with code snippets
- Library documentation with usage examples

**Special Considerations**:
- Very technical audiences may prefer code examples (consider separate technical reference docs)
- Some compliance frameworks require specific documentation formats
- AI tools work best with documentation under 2000 lines per file
- Many README.md files with the same name is acceptable - directory names provide context
- IDE tab clutter with multiple "README.md" files is a known trade-off for this pattern
