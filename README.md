# AgentCheck

**Local AI code review agents for Claude Code**

Run specialized agents against your **staged changes** before you commit. AgentCheck utilizes your real project context (docs, architecture, and conventions) and local development ecosystem (connected MCP tools and resources) to deliver tight, actionable feedback.

---

## Highlights

- ✅ **Local code review** — catch issues during development, not in post‑PR reviews  
- 🧠 **Full codebase context** — uses your docs, ADRs, and team methodology  
- 🔧 **Open source & customizable** — tune each agent to your stack and standards  
- 🖥️ **Local flow** — runs where you code; how you code; no separate review platform
- 💸 **No subscription fees**

---

## Quick Start

### 1) Install into your repo

```bash
# In your project root
git clone https://github.com/devlyai/AgentCheck.git .claude-temp
cp -r .claude-temp/agentcheck .claude/
cp -r .claude-temp/agents .claude/
rm -rf .claude-temp
echo ".claude/agentcheck/reports/" >> .gitignore
```

This adds:

```
.claude/
  agentcheck/     # context and outputs
  agents/         # the review agents (prompts + logic)
```

### 2) Initialize project context

Ask Claude Code to analyze your project and customize the agent templates:

```
"Initialize AgentCheck context for this project"
```

This analyzes your codebase and generates project-specific context files in `.claude/agentcheck/project-context/`.

### 3) Register the task in your Claude Code notes

Add to your `AGENTS.md` / `CLAUDE.md`:

```markdown
## AgentCheck — Local AI Code Review

Before committing ask Claude Code to "Run AgentCheck analysis"

The agents (logic-reviewer, security-checker, guidelines-compliance,
style-compliance, product-reviewer) analyze **staged changes** and write reports to:
`.claude/agentcheck/reports/`.
```

---

## What You Get

* **Diff‑aware reviews** focused on what you changed
* **Prioritized findings**: 🔴 Critical · 🟠 High · 🟡 Medium · 🔵 Low
* **Concrete fixes**: suggestions you can apply immediately
* **Project‑specific context**: agents learn from your docs and past decisions

### AgentCheck in Action

**All agents running in parallel:**
<img width="553" height="306" alt="482244166-603ab9c5-eb9c-49cd-af3c-06b3d300eb5b" src="https://github.com/user-attachments/assets/83caf100-f3e4-4694-845c-3721fbea9981" />

**Comprehensive analysis results:**
<img width="1183" height="292" alt="482268710-3087fa79-e57b-46d6-89c7-9093e2b73ab6" src="https://github.com/user-attachments/assets/461c981f-8bec-4b1f-b8cb-2977369a405d" />


---

## Agents List

| Agent                     | Focus                                | Typical Findings                                                 |
| ------------------------- | ------------------------------------ | ---------------------------------------------------------------- |
| **logic-reviewer**        | Correctness, edge cases, regressions | Broken invariants, unsafe refactors, missing tests               |
| **security-checker**      | Vulnerabilities & secrets            | Injections, insecure defaults, hardcoded creds, dangerous deps   |
| **guidelines-compliance** | Team standards & methodology         | Violations of ADRs, naming/domain rules, missing docs            |
| **style-compliance**      | Consistency & readability            | Lint parity, formatting drifts, dead code, unclear APIs          |
| **product-reviewer**      | User impact & behavior changes       | UX regressions, backward compatibility, telemetry/analytics gaps |

Reports are written to `.claude/agentcheck/reports/` and grouped by agent.

---

## How It Works

1. **Collects context**: project docs, ADRs, coding standards, and your Claude Code MCPs
2. **Analyzes staged diffs** per agent specialization
3. **Ranks issues** and proposes concrete, minimal‑diff fixes
4. **Continuously adapts** by generating and refining project‑specific context files

---

## Tuning & Noise Reduction

AgentCheck is designed to **get quieter and smarter** over time.

* **Edit agent prompts** in `.claude/agents/*` to encode team standards and false‑positive rules
* **Add project context**: link to docs/architecture, ADRs, and service READMEs the agents should prefer
* **Leverage MCPs**: your Claude Code MCP tools (project management, knowledge management, local resources, context manager) give agents deeper context
* **Team calibration**: as prompts evolve, human CR comments will have higher focus on design and be more impactful.

**Goal:** human code reviews faster and more useful — not a daily frustration.

---

## Troubleshooting

* **No reports generated** → Ensure your agent has relevant permissions and paths configured correctly.
* **Too many false positives** → Tighten prompts in `.claude/agents/*` and add links to your canonical docs.
* **Agent misses context** → Point agents to the right docs/ADRs; ensure your MCPs are available in Claude Code.

---

## FAQ

**Does it block commits?**
AgentCheck itself doesn’t block anything; you choose to run it before committing.

---

## Contributing

PRs and issues welcome! If you extend an agent (new checks, better prompts, project context helpers), include a short rationale and examples.

---

## License

MIT — adapt and evolve for your team’s needs.

Attribution: AgentCheck is not affiliated with Anthropic. “Claude” and “Claude Code” are trademarks of their respective owners.
