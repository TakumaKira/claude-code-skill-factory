# Generated Slash Commands

Custom slash commands created using the Slash Command Factory. These commands provide specialized workflows and automation for specific tasks.

---

## 📋 Available Commands

### 1. /enhance-claude-md

**Purpose**: Initialize or enhance CLAUDE.md files with 100% native format compliance

**Features**:
- Multi-phase workflow: Discovery → Analysis → Task
- Interactive initialization for new projects
- Quality analysis for existing CLAUDE.md files
- Can invoke skill directly OR claude-md-guardian agent
- 100% native format compliance (project structure diagrams, setup instructions, etc.)

**Usage**:
```bash
/enhance-claude-md
```

**What it does**:
1. Checks if CLAUDE.md exists
2. **If not found**: Runs interactive initialization workflow
   - Explores repository structure
   - Detects project type, tech stack, team size
   - Creates customized CLAUDE.md after confirmation
3. **If found**: Analyzes quality and suggests improvements
   - Quality score (0-100)
   - Missing sections identified
   - Enhancement recommendations

**Documentation**: [enhance-claude-md/README.md](enhance-claude-md/README.md)

**Related Components**:
- **Skill**: [claude-md-enhancer](../generated-skills/claude-md-enhancer/) - Core generation capability
- **Agent**: [claude-md-guardian](../generated-agents/claude-md-guardian/) - Background maintenance

---

### 2. /marketing-research

**Purpose**: Comprehensive marketing research and analysis workflows

**Documentation**: [marketing-research/HOW_TO_USE.md](marketing-research/HOW_TO_USE.md)

---

### 3. /review

**Purpose**: Orchestrate parallel code review across requirements, test coverage, and test execution

**Features**:
- Flexible scope: current changes, PR, entire project, or specific directory
- Parallel execution of requirements and test-coverage reviewers
- Sequential test execution for safety
- Unified report synthesizing all findings

**Usage**:
```bash
/review                    # Review current changes
/review the PR             # Review current branch vs main
/review the entire project # Full project review
/review src/auth/          # Review specific directory
```

**What it does**:
1. **Detects scope** from your input (current changes, PR, project, or path)
2. **Gathers context** (git status, diff, changed files)
3. **Parallel Phase**: Runs requirements-compliance-reviewer + test-coverage-reviewer
4. **Sequential Phase**: Runs test-runner-diagnostician
5. **Synthesizes** all findings into unified report with action items

**Documentation**: [review/README.md](review/README.md)

**Required Agents**:
- **requirements-compliance-reviewer** - `~/.claude/agents/requirements-compliance-reviewer.md`
- **test-coverage-reviewer** - `~/.claude/agents/test-coverage-reviewer.md`
- **test-runner-diagnostician** - `~/.claude/agents/test-runner-diagnostician.md`

---

## 🚀 Installation

### Project-Level (Current Project Only)

```bash
# Copy command to your project
cp -r generated-commands/[command-name] /path/to/your/project/.claude/commands/

# Restart Claude Code
```

### User-Level (All Projects)

```bash
# Copy command to user commands directory
cp -r generated-commands/[command-name] ~/.claude/commands/

# Restart Claude Code
```

### Example

```bash
# Install enhance-claude-md command (user-level)
cp -r generated-commands/enhance-claude-md ~/.claude/commands/

# Restart Claude Code
# Command will be available as /enhance-claude-md
```

---

## 📁 Command Structure

Each command folder contains:

```
command-name/
├── command-name.md      # Command definition with YAML frontmatter
└── README.md            # Installation guide and documentation
```

**Required**:
- YAML frontmatter with `allowed-tools` and `description`
- Multi-phase pattern or simple task structure
- Comprehensive documentation

---

## 🛠️ Creating New Commands

Use the **Slash Command Factory** to generate new custom commands:

1. **Use the factory skill**:
   ```bash
   # Ensure slash-command-factory skill is installed
   cp -r generated-skills/slash-command-factory ~/.claude/skills/

   # Ask Claude
   "I need a slash command for [task description]"
   ```

2. **Follow the Q&A workflow**:
   - Command purpose and naming
   - Structure pattern (Simple/Multi-Phase/Agent-Style)
   - Bash permissions needed
   - Arguments usage

3. **Output location**: Commands are generated to `generated-commands/[command-name]/`

**Template**: [../documentation/templates/MASTER_SLASH_COMMANDS_PROMPT.md](../documentation/templates/MASTER_SLASH_COMMANDS_PROMPT.md)

**Skill**: [../generated-skills/slash-command-factory/](../generated-skills/slash-command-factory/)

---

## 📖 Official Patterns

Commands in this folder follow **official Anthropic patterns**:

### Simple Pattern
```markdown
## Context
[Background information]

## Task
[What to do]
```

### Multi-Phase Pattern
```markdown
## Phase 1: Discovery
[Gather information]

## Phase 2: Analysis
[Process information]

## Phase 3: Task
[Execute action]
```

### Agent-Style Pattern
```markdown
## Role
[Agent identity]

## Process
[Step-by-step workflow]

## Guidelines
[Best practices]
```

See [../documentation/references/](../documentation/references/) for official examples.

---

## ✅ Best Practices

1. **Naming**: Use kebab-case (2-4 words)
2. **Permissions**: Specify exact bash commands, never use wildcard `Bash`
3. **Arguments**: Use `$ARGUMENTS`, never `$1`, `$2`, `$3`
4. **Documentation**: Include comprehensive README.md
5. **Validation**: Test command before distribution

---

## 🔗 Related Resources

- **Factory Skill**: [../generated-skills/slash-command-factory/](../generated-skills/slash-command-factory/)
- **Templates**: [../documentation/templates/MASTER_SLASH_COMMANDS_PROMPT.md](../documentation/templates/MASTER_SLASH_COMMANDS_PROMPT.md)
- **Official Examples**: [../documentation/references/](../documentation/references/)
- **Project Guide**: [../CLAUDE.md](../CLAUDE.md)

---

**Version**: 1.0.0
**Last Updated**: January 2026
**Total Commands**: 3
