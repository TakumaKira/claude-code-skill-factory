# /review Slash Command

Orchestrate parallel code review across requirements compliance, test coverage, and test execution with a single command.

## Features

- **Flexible Scope**: Review current changes, PRs, entire project, or specific directories
- **Parallel Execution**: Runs requirements and test-coverage reviewers simultaneously for speed
- **Sequential Test Execution**: Safely runs test diagnostics after analysis phase
- **Unified Report**: Synthesizes findings from three specialist agents into one actionable summary
- **Minimal Typing**: Just `/review` or `/review the PR` - no complex arguments needed

## Prerequisites

This command requires three specialist agents to be installed:

1. **requirements-compliance-reviewer** - `~/.claude/agents/requirements-compliance-reviewer.md`
2. **test-coverage-reviewer** - `~/.claude/agents/test-coverage-reviewer.md`
3. **test-runner-diagnostician** - `~/.claude/agents/test-runner-diagnostician.md`

See the [agents installation section](#installing-required-agents) below.

## Installation

### Option 1: Project-Level (Current Project Only)

```bash
# Copy command to your project
cp generated-commands/review/review.md /path/to/your-project/.claude/commands/

# Or create symlink
ln -s $(pwd)/generated-commands/review/review.md /path/to/your-project/.claude/commands/review.md
```

### Option 2: User-Level (All Projects)

```bash
# Copy command to user commands directory
cp generated-commands/review/review.md ~/.claude/commands/

# Restart Claude Code
```

## Usage

### Basic Usage (Current Changes)

```bash
/review
```

Reviews your uncommitted changes using `git diff`.

### PR Review

```bash
/review the PR
/review PR
/review current branch
```

Reviews all changes in the current branch compared to main.

### Full Project Review

```bash
/review the entire project
/review project
/review all
```

Reviews all source files in the project.

### Directory-Specific Review

```bash
/review src/auth/
/review backend/api/
```

Reviews only files in the specified directory.

---

## What It Does

The `/review` command orchestrates three specialist review agents:

### Phase 1: Parallel Analysis (Fast)

**Agent 1: Requirements Compliance Reviewer**
- Discovers requirement documents (PRD, specs, user stories)
- Maps requirements to implementation
- Reports compliance status: COMPLIANT, PARTIAL, NON-COMPLIANT

**Agent 2: Test Coverage Reviewer**
- Discovers existing test files
- Maps requirements to tests
- Suggests tests to **add**, **update**, or **remove**

Both agents run in parallel for maximum speed.

### Phase 2: Sequential Execution

**Agent 3: Test Runner & Diagnostician**
- Runs the test suite
- Diagnoses failures
- Traces root causes (without suggesting fixes)

Runs after parallel phase completes for system safety.

### Phase 3: Synthesis

Combines all findings into a unified report with:
- Requirements compliance summary
- Test coverage gaps
- Test execution results
- Prioritized action items

---

## Example Output

```markdown
## Code Review Summary

**Scope**: PR (15 files changed)
**Files Reviewed**: 15
**Date**: 2026-01-21

---

### Requirements Compliance

- Compliant: 8 (72%)
- Partial: 2 (18%)
- Non-Compliant: 1 (10%)

Key findings:
- Authentication flow matches PRD requirements
- Error handling partially implemented (missing edge cases)
- Rate limiting requirement not implemented

---

### Test Coverage

**Tests to Add**:
- Unit test for authentication token validation with expired tokens
- Integration test for user registration error scenarios
- E2E test for complete login-to-dashboard flow

**Tests to Update**:
- Update auth.test.ts to match new JWT structure

**Tests to Remove**:
- Remove duplicate OAuth tests in auth.spec.ts and oauth.test.ts

---

### Test Results

**Status**: 2 failures out of 47 tests

**Root Causes**:
- auth.test.ts:42 → Implementation expects 'token' field, test provides 'accessToken'
- validation.test.ts:88 → Test data uses old schema version

---

### Action Items (Prioritized)

1. **CRITICAL**: Implement rate limiting (requirement non-compliance)
2. **HIGH**: Fix 2 failing tests (root causes identified above)
3. **MEDIUM**: Add 3 missing tests for authentication edge cases
4. **LOW**: Remove duplicate OAuth test file
```

---

## Installing Required Agents

The `/review` command delegates to three specialist agents. Install them to `~/.claude/agents/`:

### Step 1: Create agents directory

```bash
mkdir -p ~/.claude/agents
```

### Step 2: Copy agent files

Copy these three agent files from this repository:

```bash
# If you have the agents in ~/.claude/agents/ already
# (they were created in Phase 1)

# Otherwise, copy from the repository:
cp path/to/requirements-compliance-reviewer.md ~/.claude/agents/
cp path/to/test-coverage-reviewer.md ~/.claude/agents/
cp path/to/test-runner-diagnostician.md ~/.claude/agents/
```

### Step 3: Verify installation

```bash
ls ~/.claude/agents/

# Expected output:
# requirements-compliance-reviewer.md
# test-coverage-reviewer.md
# test-runner-diagnostician.md
```

---

## Scope Detection Logic

The command intelligently detects your intent:

| Your Input | Detected Scope | Context Gathered |
|------------|----------------|------------------|
| `/review` (empty) | Current changes | `git status`, `git diff` |
| `/review PR` | PR branch | `git diff main...HEAD` |
| `/review the PR` | PR branch | `git diff main...HEAD` |
| `/review project` | Full project | All source files |
| `/review src/auth/` | Specific path | Files in directory + git diff for path |

---

## Advanced Usage

### Review specific features

```bash
/review src/features/authentication/
```

### Review backend only

```bash
/review backend/
```

### Review with context

The command automatically gathers relevant git context:
- Current branch name
- Recent commits
- Changed files
- Git diff output

No need to specify these manually.

---

## Troubleshooting

### "Agent not found" error

Ensure all three agents are installed to `~/.claude/agents/`:
- requirements-compliance-reviewer.md
- test-coverage-reviewer.md
- test-runner-diagnostician.md

### Tests don't run

The test-runner agent needs:
- A test framework (Jest, Pytest, etc.)
- Test command in `package.json` or test config files
- Bash permissions (already configured in command)

### No requirements found

The requirements-compliance-reviewer looks for:
- `documentation/foundation/prd.md`
- `docs/requirements/`
- `README.md` (feature specs)
- `REQUIREMENTS.md`, `SPEC.md`

Add requirements to one of these locations.

---

## Technical Details

### Parallel Execution Safety

- **Safe agents** (Read/Grep/Glob only): requirements-compliance-reviewer, test-coverage-reviewer
- **Sequential agent** (uses Bash): test-runner-diagnostician

The command runs safe agents in parallel, then sequential agents after.

### Git Commands Used

```bash
git status              # Current state
git diff               # Uncommitted changes
git diff main...HEAD   # PR changes
git log                # Recent commits
git branch             # Current branch
find                   # File discovery
```

All git commands have explicit Bash permissions in the command's YAML frontmatter.

---

## License

Part of the Claude Code Skills Factory - [MIT License](../../LICENSE)

## Contributing

Found an issue or have a suggestion? Open an issue in the repository.

---

**Version**: 1.0.0
**Last Updated**: January 2026
**Requires**: Claude Code with agent support, git repository
