# Focused Documentation Skill

**Version**: 1.1.0
**Type**: Prompt-Only Skill (Auto-Activating)
**Category**: Documentation & Knowledge Management

## Overview

The `focused-docs` skill automatically applies to ALL documentation tasks. It creates structured, modular documentation that emphasizes clarity, conciseness, and AI tool compatibility. Documentation is organized with single-responsibility files, meaningful names, and purpose-driven sections—all without code snippet pollution or internal links.

## Key Features

- **Auto-Activating**: Applies automatically to any documentation task (no special invocation needed)
- **Modular Architecture**: Each documentation file has one clear responsibility
- **Natural Language Focus**: Describes requirements and architecture without code examples
- **NO Links**: Discoverability through file/directory names only (links become stale)
- **README.md Pattern**: Each directory's main content lives in `README.md`, with the directory name providing context
- **AI Tool Optimized**: Structured for efficient context retrieval by AI coding assistants
- **Purpose-Driven Sections**: Organized by documentation goals, not boilerplate templates

## Why This Skill?

Traditional documentation often includes:
- Code examples that become outdated quickly
- Links that break over time and create maintenance burden
- Monolithic files that confuse AI coding tools
- Redundant cross-references that pollute context

This skill solves these problems by:
- Using natural language descriptions of **WHAT** needs to be done
- Making documentation navigable through file/directory names alone
- Using the README.md pattern for clear hierarchical organization
- Keeping files focused with single responsibility

## What's Included

```
focused-docs/
├── SKILL.md                    # Main skill definition
├── HOW_TO_USE.md              # Usage examples and invocation patterns
├── README.md                  # This file - installation and overview
├── sample_input.json          # Example documentation request
└── expected_output.json       # Example documentation structure output
```

## Installation

### For Claude Code (User-Level - Recommended)

Install globally for use across all projects:

```bash
# Create skills directory if it doesn't exist
mkdir -p ~/.claude/skills/

# Copy the skill folder
cp -r /Users/takuma-private/Git/claude-code-skill-factory/generated-skills/focused-docs ~/.claude/skills/

# Verify installation
ls ~/.claude/skills/focused-docs
```

### For Claude Code (Project-Level)

Install for a specific project only:

```bash
# Navigate to your project
cd /path/to/your/project

# Create skills directory
mkdir -p .claude/skills/

# Copy the skill folder
cp -r /Users/takuma-private/Git/claude-code-skill-factory/generated-skills/focused-docs .claude/skills/

# Verify installation
ls .claude/skills/focused-docs
```

### For Claude Desktop App

1. Locate the generated ZIP file (created below)
2. Drag and drop `focused-docs.zip` into Claude Desktop
3. The skill will be automatically installed and available

### Verification

After installation, verify the skill is available:

```bash
# For user-level installation
cat ~/.claude/skills/focused-docs/SKILL.md | head -5

# For project-level installation
cat .claude/skills/focused-docs/SKILL.md | head -5
```

You should see the YAML frontmatter with `name: focused-docs`.

## Quick Start

The skill activates automatically for any documentation task. No special invocation needed.

### Example Requests

**1. New Project Documentation**
```
Create documentation for a user authentication microservice. Include:
system overview, functional requirements, security design, and integration points.
```

**2. Restructure Existing Docs**
```
This README is 2500 lines and covers everything. Break it into focused,
single-responsibility files with clear directory structure.
```

**3. Architecture Documentation**
```
Document our microservices architecture describing service boundaries,
communication patterns, and data flow.
```

**4. Decision Record**
```
Create an ADR for why we chose PostgreSQL over MongoDB, including context,
options considered, and consequences.
```

**5. Any README**
```
Help me write a README for this project.
```

## Documentation Principles

This skill follows these core principles:

1. **Single Responsibility**: Each file addresses one specific concern
2. **README.md Pattern**: Each directory's main content lives in `README.md` (directory name = topic)
3. **NO Links**: Discoverability through file/directory names only
4. **Natural Language**: Descriptions without code implementation
5. **Modular Structure**: Easy to compose, extend, and maintain
6. **AI Optimized**: Focused context for efficient AI tool retrieval

## File Organization Patterns

### Small Project
```
docs/
├── README.md              (Project documentation overview)
├── purpose.md
├── requirements.md
├── architecture.md
└── workflows.md
```

### Medium Project
```
docs/
├── README.md                    (Project documentation overview)
├── overview/
│   ├── README.md                (Main overview)
│   └── goals.md
├── requirements/
│   ├── README.md                (Requirements overview)
│   └── functional.md
├── architecture/
│   ├── README.md                (Architecture overview)
│   └── components.md
└── workflows/
    ├── README.md                (Workflows overview)
    └── user-workflows.md
```

### Large Project
```
docs/
├── README.md                    (Project documentation overview)
├── overview/
│   ├── README.md
│   └── [topic].md
├── requirements/
│   ├── README.md
│   ├── functional/
│   │   ├── README.md
│   │   └── [feature].md
│   └── non-functional/
│       ├── README.md
│       └── [quality].md
├── architecture/
│   ├── README.md
│   ├── components/
│   │   ├── README.md
│   │   └── [component].md
│   └── integrations/
│       ├── README.md
│       └── [integration].md
├── decisions/
│   ├── README.md
│   └── [decision-topic].md
└── workflows/
    ├── README.md
    └── [workflow].md
```

## What This Skill Does NOT Do

- Generate code examples or implementation snippets
- Create links between documentation files
- Create API documentation with code samples (use Swagger/OpenAPI)
- Generate inline code comments (use JSDoc, Sphinx, etc.)
- Write tutorial-style "how to code" documentation
- Create boilerplate templates without context

## Use Cases

**Perfect For**:
- Requirements documentation
- Architecture and design documentation
- Process and workflow documentation
- Architecture Decision Records (ADRs)
- Project overview and planning documentation
- Specification documents

**Not Ideal For**:
- API reference documentation (use Swagger/OpenAPI)
- Code documentation (use language-specific tools)
- Tutorial content with code examples
- Quick reference guides with code snippets

## Examples

See `HOW_TO_USE.md` in this directory for detailed examples of:
- New project documentation
- Restructuring existing documentation
- Requirements documentation
- Architecture documentation
- Decision records (ADRs)
- Workflow documentation

## Support & Customization

### Customizing the Skill

The skill is prompt-only, so you can easily customize it by:

1. Editing `SKILL.md` to add domain-specific guidelines
2. Adding file organization templates for your industry
3. Including organization-specific naming conventions
4. Adding compliance or regulatory documentation patterns

### Reporting Issues

If you encounter issues or have suggestions:
1. Check `SKILL.md` for usage guidelines
2. Review `HOW_TO_USE.md` for example invocations
3. Verify file naming follows kebab-case conventions
4. Ensure documentation requests are clear and specific

## Version History

**1.1.0** (2026-01-19)
- Added `alwaysApply: true` for automatic activation on all documentation tasks
- Added NO links policy - discoverability through file/directory names only
- Added README.md pattern - each directory's main content in README.md
- Updated all examples and templates to reflect new patterns

**1.0.0** (2026-01-19)
- Initial release
- Core documentation generation capabilities
- Natural language focus (no code snippets)
- Modular file structure
- AI tool optimization
- Sample input/output examples
- Installation guides for all Claude platforms

## License

This skill is part of the Claude Code Skills Factory and follows the repository's license terms.

## Related Skills

Consider combining with:
- **aws-solution-architect**: For AWS architecture documentation
- **prompt-factory**: For generating domain-specific documentation prompts
- **content-researcher**: For gathering background information for documentation

## Credits

Created with the Claude Code Skills Factory using the SKILLS_FACTORY_PROMPT template.

---

**Ready to use**: Install the skill and start creating focused, modular documentation optimized for both humans and AI coding assistants!
