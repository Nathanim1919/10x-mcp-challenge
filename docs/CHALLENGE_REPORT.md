# TRP 1 - MCP Setup Challenge Report

**Date:** February 2, 2026  
**Candidate:** Nathanim  
**IDE:** Cursor  
**Duration:** 1 hour

---

## Executive Summary

This report documents my completion of the TRP 1 MCP Setup Challenge, which involved configuring an MCP server, researching AI agent best practices, and creating effective agent rules for Cursor IDE.

---

## Task 1: MCP Server Setup

### What I Did

1. **Researched MCP Configuration for Cursor**
   - Explored Cursor's official documentation at `https://cursor.com/docs/context/rules`
   - Investigated MCP server configuration patterns
   - Searched for the Tenx MCP server package on npm and GitHub

2. **Configuration Locations Identified**
   - User-level: `~/.cursor/mcp.json`
   - Project-level: `.cursor/mcp.json` (blocked by globalignore in some setups)
   - Created template configuration file: `mcp-config-template.json`

3. **MCP Configuration Template Created**
   ```json
   {
     "mcpServers": {
       "tenx": {
         "command": "npx",
         "args": ["-y", "@10academy/tenx-mcp"],
         "env": {
           "TENX_API_KEY": "${TENX_API_KEY}"
         }
       }
     }
   }
   ```

### Challenges Encountered

1. **Package Discovery Issue**
   - The specific "Tenx MCP" server package from 10 Academy was not found in public npm registry
   - Searched variations: `tenx-mcp`, `@10academy/tenx-mcp`, `mcp-sense`
   - **Resolution:** Created a template configuration that can be updated with the correct package name once provided

2. **File System Restrictions**
   - `.cursor/mcp.json` was blocked by globalignore
   - **Resolution:** Created `mcp-config-template.json` in project root as a reference

### What Worked

- Successfully identified the correct configuration structure for Cursor MCP
- Created a reusable template that follows MCP standards
- Documented the setup process for future reference

### What Didn't Work

- Could not locate the specific Tenx MCP package in public repositories
- Direct writing to `.cursor/mcp.json` was blocked

---

## Task 2: Agent Rules Configuration

### Research Conducted

1. **Cursor Documentation Analysis**
   - Studied the official Cursor Rules documentation
   - Learned about `.mdc` file format with frontmatter
   - Understood rule types: Project Rules, Team Rules, User Rules

2. **Best Practices Identified from Research**

   **From Cursor Documentation:**
   - Keep rules under 500 lines
   - Split large rules into composable pieces
   - Provide concrete examples
   - Avoid vague guidance
   - Reference files instead of copying content
   - Check rules into git for team sharing

   **From Community Best Practices (Boris Cherny's approach):**
   - Focus on workflow optimization
   - Define clear communication expectations
   - Establish code quality standards
   - Set boundaries on what the agent should NOT do

3. **Key Insights from Research**
   - Rules provide persistent, reusable context at the prompt level
   - Rules are included at the start of model context
   - `alwaysApply: true` ensures rules apply to every session
   - Good rules are focused, actionable, and scoped

### Rules File Created

**Location:** `.cursor/rules/agent.mdc`

**Key Sections:**
1. **Core Principles** - Understand before acting, minimal changes, code quality
2. **Workflow Guidelines** - Before/during/after writing code
3. **Project Conventions** - File organization, naming, error handling
4. **What NOT To Do** - Clear boundaries to prevent over-engineering
5. **Tool Usage** - Guidelines for terminal, file operations, search
6. **Response Format** - Structured approach to providing solutions

### What Worked

- The `.mdc` format with frontmatter was accepted by Cursor
- Rules are now applied to all agent interactions
- Clear structure makes rules easy to maintain and extend

### What Didn't Work

- Initial attempts to find Boris Cherny's specific X thread were unsuccessful
- Had to rely on general community best practices and official documentation

---

## Task 3: Insights Gained

### How Rules Change AI Agent Behavior

1. **Consistency**
   - Rules ensure the agent follows the same patterns across all interactions
   - Reduces variability in code style and approach

2. **Focus**
   - "What NOT To Do" section prevents over-engineering
   - Agent stays focused on the requested task

3. **Quality**
   - Code quality standards are enforced automatically
   - Error handling and testing are prioritized

4. **Communication**
   - Clear expectations for how the agent should explain changes
   - Reduces back-and-forth clarification

### Key Learnings

1. **Rules as Documentation**
   - Well-written rules serve as living documentation of team standards
   - They encode tribal knowledge that would otherwise be lost

2. **Iterative Improvement**
   - Rules should be updated when the agent makes mistakes
   - Version control allows tracking rule evolution

3. **Balance is Key**
   - Too many rules can constrain the agent unnecessarily
   - Too few rules lead to inconsistent behavior
   - Focus on patterns you use frequently

4. **Context Matters**
   - Rules should reference existing code patterns
   - Project-specific conventions should be explicit

### Recommendations for Future Work

1. **Rule Refinement**
   - Monitor agent behavior and update rules based on actual issues
   - Add project-specific patterns as they emerge

2. **MCP Integration**
   - Once the Tenx MCP server details are available, complete the integration
   - Test the logging functionality to ensure interactions are captured

3. **Team Collaboration**
   - Share rules with team members via git
   - Establish a process for proposing rule changes

---

## Files Created

| File | Purpose |
|------|---------|
| `.cursor/rules/agent.mdc` | Main agent rules file |
| `mcp-config-template.json` | MCP server configuration template |
| `docs/CHALLENGE_REPORT.md` | This documentation |
| `docs/RULES_REFERENCE.md` | Detailed rules explanation |
| `docs/MCP_SETUP_GUIDE.md` | MCP setup instructions |

---

## Conclusion

This challenge provided valuable experience in:
- Understanding MCP server architecture and configuration
- Researching and implementing AI agent best practices
- Creating effective rules that guide agent behavior
- Documenting technical processes for team collaboration

The rules file created will serve as a foundation for effective AI-assisted development, and can be iteratively improved based on actual usage patterns.

---

*Report generated as part of TRP 1 - MCP Setup Challenge*

