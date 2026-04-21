# Managed Agent 4: Weekly OKR Pulse Check

**Monday at 6 AM. Reads all active initiatives across your project management tool. Maps them to OKRs. Flags stalled and orphaned work. Posts a health report to Slack before planning.**

OKRs get reviewed properly once a quarter. In between, the honest answer to "how are we tracking?" is "I think we're okay." That's not a number. It's a guess.

## What it produces

> **OKR Pulse — Week of Apr 21**
>
> **KR 1: Activation rate 27% → 40% — On Track**
> Active: Onboarding v2 redesign, Signup flow A/B test
> Stalled: First-run checklist (14 days, no commits)
>
> **KR 2: NPS 38 → 45 — At Risk**
> Active: Support response time initiative
> Stalled: —
>
> **KR 3: Enterprise integrations 0 → 3 — No Active Work**
> Active: —
> Stalled: —
>
> **Orphaned Work** (no OKR connection)
> - Dashboard mobile redesign — Owner: Design team
> - Pricing page refresh — Owner: Marketing
>
> Full initiative breakdown available on request.

## Who builds this

Engineer-wired. Needs Linear / Jira / Asana MCP (read) + Slack MCP.

## Setup

**Step 1.** Go to [platform.claude.com](https://platform.claude.com) → Managed Agents → Quickstart.

**Step 2.** Paste this into "Describe your agent":

```
An agent that tracks OKR health for [COMPANY]'s [TEAM NAME] team
every Monday at 6 AM.

It reads all active initiatives and their last update dates from
[PROJECT MANAGEMENT TOOL: Linear / Jira / Asana page URL] and maps
them against the current quarter's OKRs:

  [LIST EACH KEY RESULT: e.g. "Increase activation rate from X% to
  Y% by [date]"]
  [KR 2]
  [KR 3]
  [KR 4]

For each KR it flags:
– Status: On Track, At Risk, or No Active Work
– Initiatives currently driving this KR (by name)
– Initiatives stalled 14+ days (no commits, no status update, no
  ticket movement)

It also flags orphaned work: any active initiative that does not
map to a listed KR.

It posts a Slack report to [CHANNEL ID] in this format:

  *OKR Pulse — Week of [date]*

  KR 1: [name] — [Status]
    Active: [initiative names]
    Stalled: [initiative names + days stalled]

  (repeat per KR)

  *Orphaned Work* (no OKR connection)
  – [initiative name] — Owner: [name]

  Final line: "Full initiative breakdown available on request."

If no initiatives are found in the project management tool, it
posts: "OKR pulse failed — no initiatives readable from
[TOOL NAME]. Check connector permissions."
```

**Step 3.** Click **Generate** → review YAML → **Create agent**.

**Step 4.** Copy the agent ID. Hand to engineering.

## Iteration

**Update the OKR list at the start of each quarter.** The agent has no memory of what your OKRs used to be — just edit the system prompt.

**First few weeks:** will surface orphaned work that surprises you — initiatives that felt connected to a goal but don't hold up to explicit mapping. That's the most valuable output. Decide per item: kill, reframe as a KR, or accept as necessary non-goal work.

## Guardrails to discuss with engineering

- **Read-only permissions.** This agent never needs to write to your PM tool. Scope tightly.
- **Initiative "stalled" signal.** 14 days is a default. If you have long-running initiatives that move in batches, tune to 30 days or track commit activity via the GitHub MCP instead.
- **Don't auto-escalate.** Resist the temptation to have the agent DM the initiative owner. Use the Slack report as the human conversation starter.
