# Security & Data Flow

**One page to show your security team. Covers what data leaves your boundary, where it goes, and the audit trail.**

---

## Data flow summary

| Component | Reads from | Writes to | Where data lives |
|---|---|---|---|
| **Routines** (cloud, Anthropic-managed) | Connectors you authorize (Gmail, Calendar, Notion, Slack, web) | Connectors you authorize (Slack, Notion, Gmail drafts) | Anthropic cloud infrastructure. Session logs retained per Anthropic's terms. |
| **Managed Agents** (cloud, Anthropic-managed) | MCP servers you authorize (Zendesk, Jira, Linear, Notion, Slack, web) | MCP servers with write scope you authorize | Same as above. Per-user isolated sessions. |
| **MCP servers** (hosted by service providers or self-hosted) | Depends on which servers | Depends on which servers | Depends on provider (Notion → Notion, Slack → Slack, etc.) |

**Boundaries crossed:**
- Your corpus of tickets / transcripts / emails → Anthropic API → Claude model → response → your destination (Slack channel, Notion page)
- Nothing persists on the client (no laptop local storage)
- Session logs are retained in your Claude Console (Sessions view)

## What to review with your security team

1. **Anthropic's data handling policies** — [anthropic.com/privacy](https://anthropic.com/privacy). Confirm alignment with your DPA requirements.
2. **Per-connector scope.** Each MCP connection is scoped. Review tokens: are they read-only where possible? Scoped to target channel/page only?
3. **Session log retention.** How long Anthropic retains session event logs. Whether your contract overrides the default.
4. **Prompt injection via user content.** If agents read user-generated text (tickets, reviews), understand that malicious input could try to manipulate the agent. Mitigation: narrow write scopes.
5. **Audit log export.** Sessions view shows every tool call. Pipe to your SIEM if required.

## Sensitivity tiers — which agents to review most carefully

| Agent / Routine | Sensitivity | Why |
|---|---|---|
| Morning meeting brief | **Medium** | Reads Gmail (may contain confidential threads). Writes to your personal DM only. |
| Competitor pricing monitor | **Low** | Public pages in, Slack out. No PII. |
| Weekly user sentiment | **Low-medium** | Public sources only. No customer data. |
| Support ticket pattern analysis | **High** | Contains customer PII. Review data handling carefully. |
| Competitive intelligence (team) | **Low** | Public pages. Notion/Slack out. |
| Meeting transcript backlog | **High** | Transcripts may contain customer calls, legal discussions, compensation talk. Channel-level routing required. |
| OKR pulse | **Medium** | Reads project management tool. May include confidential roadmap. Internal channel only. |

## Compliance notes

- **HIPAA:** Cloud-only today. Not appropriate for PHI without BAA review.
- **SOC 2:** Anthropic maintains SOC 2 Type II. Request current report through your account team.
- **GDPR:** Data processing agreement available through enterprise contract.
- **FedRAMP:** Not available.
- **Data residency:** US-hosted only at publication time. Check current availability if you have EU data residency requirements.

## The security checklist (from engineer-handoff-brief.md)

- [ ] Credentials in the vault, not the prompt
- [ ] MCP tokens scoped narrowly (channel-only, page-only, read-only)
- [ ] PII handling policy signed off for any agent touching customer data
- [ ] Audit log forwarding to SIEM configured if required
- [ ] No write access by default — add only where needed
- [ ] Per-day invocation cap in your own code (don't rely on platform limits)
- [ ] Explicit failure modes in the prompt (post to Slack, don't fail silently)

## Prompt injection mitigation

If any agent reads user-generated content (support tickets, reviews, transcripts), read [prompt-injection-mitigation.md](./prompt-injection-mitigation.md). Covers instruction delimiting, output validation, canary tokens, anomaly detection, and per-agent sensitivity levels.

## What to send your security team

Attach these files when asking for approval:
1. This `SECURITY.md`
2. [`prompt-injection-mitigation.md`](./prompt-injection-mitigation.md)
3. The specific agent file you're deploying (e.g. `managed-agents/01-support-ticket-patterns.md`)
4. [`managed-agents/engineer-handoff-brief.md`](./managed-agents/engineer-handoff-brief.md)
