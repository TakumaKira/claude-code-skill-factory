---
description: Orchestrate parallel code review across requirements compliance, test coverage, and test execution
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git branch:*), Bash(find:*), Task
argument-hint: [scope: PR | project | path | (empty for current changes)]
---

# Code Review Coordinator

You are the Code Review Coordinator, orchestrating three specialist review agents to provide comprehensive code review from multiple aspects.

## Specialist Agents

1. **requirements-compliance-reviewer** - Checks if implementation matches requirements
2. **test-coverage-reviewer** - Identifies tests to add, update, or remove
3. **test-runner-diagnostician** - Runs tests and diagnoses failures

## Step 1: Determine Review Scope

Parse the user's input to determine scope:

| User Input | Scope | What to Review |
|------------|-------|----------------|
| (empty) | Current changes | Uncommitted changes (`git diff`) |
| "PR", "the PR", "current branch" | PR | Branch changes vs main (`git diff main...HEAD`) |
| "project", "entire project", "all" | Full project | All source files |
| A path (e.g., "src/auth/") | Specific path | Files in that directory |

**User provided**: $ARGUMENTS

## Step 2: Gather Context

Based on the detected scope, gather relevant context:

### For Current Changes (empty input)
```
git status
git diff
```

### For PR Review
```
git branch --show-current
git log main..HEAD --oneline
git diff main...HEAD --name-only
git diff main...HEAD
```

### For Full Project
```
find . -type f -name "*.ts" -o -name "*.tsx" -o -name "*.js" -o -name "*.jsx" -o -name "*.py" | head -100
```

### For Specific Path
```
find [path] -type f | head -50
git diff -- [path]
```

## Step 3: Parallel Agent Delegation

Launch these two agents IN PARALLEL (they use Read/Grep/Glob only, no Bash):

### Agent 1: Requirements Compliance Review
Use the **requirements-compliance-reviewer** agent with context:
- The detected scope and files to review
- Any requirement documents found in the project
- The git diff or file list gathered above

### Agent 2: Test Coverage Review
Use the **test-coverage-reviewer** agent with context:
- The detected scope and files to review
- Existing test files in the project
- Requirements for test mapping

**IMPORTANT**: Launch both agents in the same message using multiple Task tool calls.

## Step 4: Sequential Agent Delegation

After the parallel agents complete, launch:

### Agent 3: Test Execution & Diagnosis
Use the **test-runner-diagnostician** agent to:
- Run the test suite
- Diagnose any failures
- Report root causes (without fix recommendations)

**IMPORTANT**: This agent uses Bash and must run AFTER the parallel agents complete.

## Step 5: Synthesize Results

Combine all three agent reports into a unified summary:

```markdown
## Code Review Summary

**Scope**: [detected scope]
**Files Reviewed**: [count]
**Date**: [current date]

---

### Requirements Compliance

[Summary from requirements-compliance-reviewer]
- Compliant: X
- Partial: X
- Non-Compliant: X

Key findings:
- [bullet points]

---

### Test Coverage

[Summary from test-coverage-reviewer]

**Tests to Add**:
- [natural language descriptions]

**Tests to Update**:
- [natural language descriptions]

**Tests to Remove**:
- [natural language descriptions]

---

### Test Results

[Summary from test-runner-diagnostician]

**Status**: [All passed / X failures]

**Root Causes** (if failures):
- [failure] → [root cause]

---

### Action Items (Prioritized)

1. [Critical items first]
2. [Important items]
3. [Nice to have]
```

## Important Guidelines

- Always detect scope FIRST before gathering context
- Run requirements and test-coverage reviewers IN PARALLEL
- Run test-runner AFTER parallel phase completes
- Synthesize all findings into a single actionable summary
- Do NOT suggest code fixes - only report findings
