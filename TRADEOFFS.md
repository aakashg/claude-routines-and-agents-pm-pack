# Tradeoffs — What Breaks, What Costs, When Not to Use This

**Every AI repo over-promises. This is the honest version.**

---

## What will cost you more than you expect

| Thing | Why | Mitigation |
|---|---|---|
| **Managed Agents token spend at scale** | Sonnet 4.6 is $3/$15 per MTok. An agent reading hundreds of tickets weekly is cheap. An agent reading every ticket in real-time is not. | Start with weekly scans, not real-time. Measure before scaling cadence. |
| **Run log debugging time** | When a Routine "doesn't work," 80% of the time it's a silent partial failure (one URL failed, one connector timed out). Reading logs takes practice. | Build a muscle: every failed run, open the log *first*. Don't reread the prompt. |
| **Prompt maintenance** | Categories drift. Your competitors change names. Your OKRs shift quarterly. | Quarterly prompt review is mandatory, not optional. Calendar it. |
| **False positives fatigue** | The first week of sentiment/pricing Routines will cry wolf. | Tighten thresholds (3+ → 5+ mentions) after a week. |

## What will break

**Routines:**

- **JS-heavy pages, login walls, CAPTCHAs.** Competitor marketing sites are often gated or bot-protected. The Routine will name the failing URL in Slack — swap it for changelog/G2/pricing blog.
- **OAuth scopes set too narrow.** #1 cause of empty Gmail briefs. Reconnect with full read access.
- **Notion page permissions.** If the page isn't shared with the Claude integration, writes fail silently.
- **Slack channel archived.** If you archive the channel the Routine posts to, the Routine keeps running and burning your daily limit.
- **Silent stateless failures.** Each run is fresh. If you don't write yesterday's state to Notion and re-read it, the Routine re-discovers "new" things every run.

**Managed Agents:**

- **MCP token expiry.** Credentials in the vault expire. Set calendar reminders.
- **Rate limits on the underlying service.** G2, Zendesk, Jira all have rate limits. An agent hammering them will 429 and the failure shows up as "no data" in your Slack report.
- **Prompt injection via user content.** If the agent reads user-generated content (tickets, G2 reviews, transcripts), a malicious/mischievous user can inject instructions. Always scope write permissions narrowly — an agent that can read tickets but only *post to one Slack channel* has a small blast radius.
- **Infinite loops.** An agent that writes to Notion and reads from Notion can, with a bad prompt, detect its own writes as "new changes" and loop. Explicit "ignore edits from this agent account" in the prompt.

## When NOT to use this

**Don't use Routines / Managed Agents for:**

- **Financial records, compliance audits, or anything that requires determinism.** Same prompt, same input → slightly different output. That's fine for judgment work, fatal for a ledger.
- **Real-time latency-critical paths.** Session startup adds seconds. Not a chatbot.
- **Regulated data without legal sign-off.** HIPAA, PCI-DSS, and some GDPR scenarios require on-premise. Managed Agents are cloud-only today.
- **Replacing human judgment on hiring, firing, or compensation.** Obvious, but worth saying.
- **Anything where you can't tolerate a 1-2% wrong-output rate.** The error rate is low, not zero.

## Cost estimation

**These are order-of-magnitude estimates based on typical token usage, not measured invoice data. Measure your own in week 1 — your mileage will vary by connector usage and prompt length.**

Rough numbers for budget discussions:

| Use case | Runs/week | Avg tokens/run | Weekly cost (est.) |
|---|---|---|---|
| Morning meeting brief (personal Routine) | 5 | ~15k in, ~2k out | ~$0.20 |
| Competitor pricing monitor | 7 | ~30k in, ~1k out | ~$0.30 |
| Weekly user sentiment | 1 | ~100k in, ~3k out | ~$0.35 |
| Support ticket agent (team) | 1 | ~200k in, ~5k out | ~$0.70 |
| Competitive intelligence agent (team) | 1 | ~150k in, ~5k out | ~$0.55 |
| Meeting transcript agent | ~20 meetings | ~20k in, ~3k out each | ~$1.50 |
| OKR pulse agent | 1 | ~50k in, ~2k out | ~$0.20 |

Total for all seven, if fully adopted: **under $5/week per team**. Scale concerns kick in at ~100x this — real-time, high-volume use cases.

## What the repo does NOT cover

- Multi-agent orchestration (research preview)
- Persistent cross-session memory (research preview)
- On-premise / self-hosted deployment (not available)
- Custom model fine-tuning for domain-specific tasks
- Non-English language use cases (works, but not specifically tuned)

---

*If you hit a failure mode not listed here — add it and send a PR. This doc is most useful when it grows from real experience.*
