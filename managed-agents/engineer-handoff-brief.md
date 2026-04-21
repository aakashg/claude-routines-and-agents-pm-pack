# Engineer Handoff Brief — Managed Agents

**Hand this to the engineer wiring a Managed Agent for the first time. It's the six things they need to define before shipping.**

---

## The six things to define before you start

| # | Item | Where it lives |
|---|---|---|
| 1 | **System prompt** — what the agent does and doesn't do | Agent config YAML |
| 2 | **Tool list** — allowed and denied (per-tool permission policy) | Agent config YAML |
| 3 | **Success criteria** — how we verify the output is usable | This doc, plus the PM's eval rubric |
| 4 | **MCP connections** — Slack, Notion, Jira, Zendesk, etc. | `mcp_servers` in YAML |
| 5 | **Trigger** — cron, webhook, or on-demand | Routine / Agent trigger config |
| 6 | **Review cadence** — who reads the output, when | Shared calendar or team ritual |

## The 3-component architecture (what you're actually building)

**1. The Agent** — the brain.
Model + system prompt + tools + per-tool permissions. Defined once, reused forever.

**2. The Environment** — the hands.
Cloud container (Python / Node / Go), network rules you define, lifecycle managed by Anthropic. Spins up, scales, tears down.

**3. The Session** — the log.
Append-only event log. Persists through disconnections. Checkpointed every step. Runs autonomously for hours.

## Built-in tools (zero setup)

- Bash
- File ops
- Web search
- Web browse
- Code exec
- MCP servers

## Pricing (as of publication)

- **$0.08 per session-hour** — idle time is free
- **$3 input / $15 output** per MTok (Sonnet 4.6)
- **~$0.01 for a 10-minute Sonnet run** — tokens dominate at scale

Budget accordingly. The OKR pulse running weekly is effectively free. A support ticket agent scanning thousands of tickets every Monday isn't.

## What's in public beta right now (Apr 2026)

- Long-running autonomous sessions ✅
- MCP + custom tool connections ✅
- Full audit trail + session tracing ✅
- Scoped permissions + credential vault ✅

## What's in research preview (don't spec features that depend on these yet)

- Multi-agent (agents spawning sub-agents)
- Memory across sessions
- Self-evaluation vs. success criteria
- Outcome-based iteration

## Security checklist

- [ ] **Credentials in the vault, not the prompt.** If the system prompt contains an API key, rewrite.
- [ ] **Scope MCP tokens narrowly.** Slack token → target channel only. Notion token → target database only. Jira token → read-only where possible.
- [ ] **PII handling.** If tickets / transcripts / emails contain PII, confirm your data handling policy covers it routing through Anthropic's API. Legal and security sign-off before first prod run.
- [ ] **Audit log forwarding.** Pipe the Sessions audit log to your SIEM. Every tool call is logged — use it.
- [ ] **No write access by default.** If the agent doesn't need to write, don't let it. Read-only tokens wherever possible.
- [ ] **Rate limits.** Put a per-day cap on agent invocations in your own code. Don't rely on Anthropic's to save you from a runaway webhook.
- [ ] **Failure modes posted, not silent.** Every agent in this repo has explicit fallback behavior ("If X fails, post Y to Slack"). Keep those. Silent failures are worse than loud ones.

## Testing before first prod run

1. Run the agent manually via the Claude console with a representative input
2. Inspect every tool call in the session log — does the agent touch anything it shouldn't?
3. Verify write targets (Notion page, Slack channel) — is it writing where expected?
4. Run it 3 times with the same input — is the output reasonably consistent?
5. Run it with deliberately malformed / missing input — does it fail gracefully or silently break?
6. Only then, schedule it.

## What the PM needs from you (so they can iterate)

1. **The agent ID** — so they can use Guided Edit in the console.
2. **Permission to edit the system prompt without a deploy.** PMs should tune the prompt. Engineers wire the infrastructure.
3. **A way to see the session log.** Share the link to the Sessions view in the console.
4. **An escape hatch.** One-line pause command or a kill switch URL if something goes sideways in prod.

## Common PM misconceptions your engineer should expect

The PM handed you this repo. They may also be carrying some assumptions worth correcting up front:

| Misconception | Reality |
|---|---|
| *"The prompt is the whole thing."* | The prompt is ~30% of the work. MCP wiring, permission scoping, audit integration, and input plumbing are the rest. |
| *"If we can just paste the YAML in the console, we're done."* | The console handles the agent. You still need to wire the trigger (webhook, cron, event), the credential vault, and the monitoring. |
| *"Security review is a rubber stamp."* | Especially if the agent touches customer data. Build the SECURITY.md review into the timeline, not as an afterthought. |
| *"Once it's shipped, it runs itself."* | Prompts decay (categories drift, competitors rename, OKRs change quarterly). Build a tuning cadence into the deploy. |
| *"It should never hallucinate."* | It will. The 3+ mention threshold and output validation exist because hallucination is bounded, not zero. Communicate this expectation. |

Spend 10 minutes on these in your kickoff. Saves two weeks of "why isn't it working the way I expected" later.

## What you need from the PM (so you can ship)

1. The markdown file from this repo with the brackets filled in
2. The exact Slack channel ID or Notion page URL for writes
3. The list of roadmap items / OKRs / competitors to reference
4. A clear definition of "good output" — sample runs they'd approve
5. Sign-off from security / legal if the agent touches customer data

---

*This brief pairs with the files in `/managed-agents/`. Each agent file has its own guardrails section. Read the one for the agent you're building.*
