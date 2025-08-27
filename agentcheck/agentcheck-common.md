# AgentCheck Common Utilities

## SEMANTIC ANALYSIS GUIDELINES

All AgentCheck subagents should use Claude's semantic understanding rather than bash commands for analysis:

### Change Detection
Instead of bash commands, use Claude tools to:
- **Read tool**: Examine specific files that have been modified
- **Glob tool**: Find files by patterns when searching for related code
- **Grep tool**: Search for specific patterns across the codebase
- **Git context**: Use provided git status and branch information

### Task Context Understanding
Analyze task context semantically:

**Branch Pattern Recognition:**
- `feature/*`, `feat/*` → Feature development
- `fix/*`, `hotfix/*`, `bugfix/*` → Bug fixes  
- `refactor/*`, `refact/*` → Code refactoring
- `docs/*`, `doc/*`, `documentation/*` → Documentation
- `test/*`, `tests/*` → Testing
- Keywords: `*create*`, `*add*`, `*implement*` → Feature work
- Keywords: `*fix*`, `*bug*`, `*issue*` → Bug fixes
- Keywords: `*refactor*`, `*cleanup*`, `*improve*` → Refactoring

**Task ID Extraction:**
- Look for patterns like `PROJ-123`, `TASK-456`, `BUG-789` in branch names
- Extract meaningful task context from descriptive branch names

### File Analysis Approach
1. **Focus on Changed Files**: Only analyze files that have been modified
2. **Use Semantic Understanding**: Understand code intent, not just syntax
3. **Consider File Relationships**: How changes affect related components
4. **Context-Aware Analysis**: Adapt feedback based on change type and scope

## CHANGE-FOCUSED ANALYSIS PRINCIPLES

All AgentCheck subagents should follow these principles:

1. **Semantic File Analysis** - Use Read tool to understand file contents and changes
2. **Focus on Modified Code** - Concentrate feedback on new or changed lines
3. **Understand Change Intent** - Consider why changes were made, not just what changed
4. **Task Context Awareness** - Align analysis with the intended task type
5. **Provide Actionable Feedback** - Include examples and concrete improvements
6. **Educational Approach** - Help developers learn and improve their practices

## CONTEXT AWARENESS

Before analyzing, understand the change context:

- **Feature branches** (`feature/*`): Focus on completeness, integration, and user experience
- **Bug fix branches** (`fix/*`, `bug/*`): Focus on correctness, minimal scope, and regression prevention
- **Refactor branches** (`refactor/*`): Focus on behavioral equivalence and code improvement
- **Documentation branches** (`docs/*`): Focus on accuracy, completeness, and clarity
- **Test branches** (`test/*`): Focus on coverage, quality, and reliability

## REPORT HANDLING

All subagents MUST generate their reports and pass them to the main agent for saving:

### Report Generation
Each subagent should generate a report with this structure:

**Timestamp Format**: `YYYYMMDD-HHMMSS`
**Report Name**: `{agent-name}-{timestamp}.md`

### Report Structure
```markdown
# {Agent Name} Report
**Timestamp**: {ISO datetime}
**Branch**: {current branch}
**Agent**: {agent-name}

## Analysis Summary
[Brief summary of findings]
```

### Report Delivery
Instead of saving reports directly, subagents should:
1. Generate the complete report content
2. Return the report to the main agent with the suggested filename
3. Let the main agent handle the actual file creation and saving

This ensures centralized report management and consistent file handling.

## ANALYSIS WORKFLOW

Each subagent should follow this pattern:

1. **Understand Context**: Branch name, task type, scope of changes
2. **Analyze Changed Files**: Use Read tool to examine modified files
3. **Apply Domain Expertise**: Use agent-specific knowledge (security, logic, style, etc.)
4. **Generate Report**: Create complete report content with suggested filename
5. **Return to Main Agent**: Pass the report content and filename back to the main agent
6. **Provide Targeted Feedback**: Focus on issues within the agent's domain