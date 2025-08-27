# Contributing

## Improving Agents

To improve an agent:

1. Test the agent on real codebases
2. Identify false positives or missed issues
3. Update the agent's detection patterns
4. Submit a PR with examples

## Agent Structure

Each agent follows this pattern:

```markdown
---
name: agent-name
description: What this agent checks
tools: "*"
---

## DESCRIPTION
What the agent does and when to use it.

## OUTPUT FORMAT
🔍 **[filename]:[line]** • [CRITICAL/HIGH/MEDIUM]
**Problem**: [Issue description]
**Fix**: [Concrete solution]
```

## Testing Changes

Test your changes by:
1. Copy modified agent to a test project's `.claude/agents/`
2. Run via Claude Code Task tool
3. Verify the agent works correctly
4. Check that reports are actionable