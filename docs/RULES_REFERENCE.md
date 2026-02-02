# Agent Rules Reference Guide

This document provides a detailed explanation of the agent rules configured in `.cursor/rules/agent.mdc`.

## File Format

Cursor rules use the `.mdc` (Markdown with Configuration) format, which combines YAML frontmatter with Markdown content.

### Frontmatter Structure

```yaml
---
description: Brief description of what the rule does
alwaysApply: true|false
glob: "**/*.ts"  # Optional: file patterns to match
---
```

**Properties:**
- `description`: Helps the agent decide if the rule should be applied (when not always applied)
- `alwaysApply`: When `true`, rule applies to every chat session
- `glob`: File patterns that trigger the rule (e.g., `**/*.tsx` for React files)

## Rule Sections Explained

### 1. Core Principles

These are the foundational guidelines that shape all agent behavior:

#### Understand Before Acting
```
- Always read and understand the relevant code before making changes
- Ask clarifying questions when requirements are ambiguous
```

**Why:** Prevents the agent from making changes based on assumptions. This is crucial because LLMs can confidently generate incorrect code if they don't have full context.

#### Minimal, Focused Changes
```
- Make the smallest change that solves the problem
- Avoid over-engineering or adding unnecessary abstractions
```

**Why:** Reduces the risk of introducing bugs and keeps code maintainable. Over-engineering is a common AI tendency that this rule explicitly prevents.

### 2. Workflow Guidelines

Structured approach to code changes:

#### Before Writing Code
1. Understand the full context
2. Identify affected files
3. Consider edge cases
4. Plan the approach

**Why:** Planning prevents rework and ensures comprehensive solutions.

#### While Writing Code
1. Write tests alongside implementation
2. Handle errors gracefully
3. Follow DRY principles
4. Use existing utilities

**Why:** Maintains code quality during implementation.

#### After Writing Code
1. Verify changes work
2. Check for linting errors
3. Ensure no regressions
4. Summarize changes

**Why:** Ensures completeness and provides clear communication.

### 3. Project Conventions

Project-specific standards that ensure consistency:

#### Naming Conventions
| Type | Convention | Example |
|------|------------|---------|
| Variables/Functions | camelCase | `getUserData` |
| Classes/Components | PascalCase | `UserProfile` |
| Constants | SCREAMING_SNAKE_CASE | `MAX_RETRIES` |

#### Error Handling
- Never silently swallow errors
- Provide actionable error messages
- Log errors appropriately

### 4. What NOT To Do

Explicit boundaries prevent common AI mistakes:

| Don't | Why |
|-------|-----|
| Add unrequested features | Scope creep, maintenance burden |
| Create documentation unless asked | Unnecessary file creation |
| Refactor working code | Risk of introducing bugs |
| Use deprecated APIs | Future compatibility issues |
| Ignore project conventions | Inconsistent codebase |

### 5. Tool Usage Guidelines

Specific instructions for using Cursor's tools:

#### Terminal Commands
- Use non-interactive flags (`--yes`, `-y`)
- Run long processes in background
- Check if services are running first

#### File Operations
- Use dedicated file tools (not shell commands)
- Preserve file permissions
- Make atomic changes

#### Search and Navigation
- Semantic search for understanding
- Grep for exact matches
- Read files before editing

## Customization Guide

### Adding Project-Specific Rules

Create additional rule files in `.cursor/rules/`:

```
.cursor/rules/
├── agent.mdc          # Core rules (always apply)
├── typescript.mdc     # TypeScript-specific rules
├── react.mdc          # React component rules
└── testing.mdc        # Testing conventions
```

### Example: TypeScript-Specific Rule

```yaml
---
description: TypeScript coding standards
glob: "**/*.ts"
---

# TypeScript Rules

## Type Safety
- Always use explicit types for function parameters
- Avoid `any` type - use `unknown` if type is uncertain
- Use type guards for runtime type checking

## Imports
- Use absolute imports with path aliases
- Group imports: external, internal, types
- No circular dependencies
```

### Example: React Component Rule

```yaml
---
description: React component conventions
glob: "**/*.tsx"
---

# React Component Rules

## Component Structure
1. Imports
2. Types/Interfaces
3. Component definition
4. Styles (if applicable)
5. Export

## Hooks
- Custom hooks in `hooks/` directory
- Prefix with `use`
- Return typed values
```

## Best Practices for Rules

### Do
- Keep rules focused and specific
- Provide concrete examples
- Reference existing code patterns
- Update rules when issues arise
- Version control your rules

### Don't
- Copy entire style guides
- Document every possible command
- Add edge case instructions
- Duplicate codebase content

## Measuring Rule Effectiveness

Track these metrics to evaluate your rules:

1. **Consistency**: Are agent responses following the same patterns?
2. **Accuracy**: Are fewer corrections needed?
3. **Efficiency**: Is less back-and-forth required?
4. **Quality**: Is the generated code meeting standards?

## Updating Rules

When to update:
- Agent makes a repeated mistake
- New project conventions are established
- Team feedback indicates confusion
- Technology stack changes

How to update:
1. Identify the specific issue
2. Add or modify the relevant rule
3. Test with similar prompts
4. Commit the change with clear message

---

*This reference is part of the TRP 1 MCP Setup Challenge documentation.*

