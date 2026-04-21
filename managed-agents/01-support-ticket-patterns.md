# Managed Agent 1: Support Ticket Pattern Analysis

**Monday at 6 AM. Reads the past 7 days of support tickets. Finds recurring themes. Maps them to your roadmap. Posts ranked report to Slack before standup.**

Most teams prioritize off the loudest tickets, not the most common. The actual pattern across 200 tickets is invisible unless someone reads every one manually.

## What it produces

> **Support Pattern Report — Week of Apr 21**
>
> | Theme | Count | On Roadmap? |
> |---|---|---|
> | SSO setup confusion | 23 | Yes |
> | Dashboard performance | 18 | No |
> | CSV export missing | 14 | No |
> | Mobile redesign feedback | 11 | Unknown |
>
> Top 3 themes summarized in one sentence each using the actual words customers used.
>
> Full ticket list available on request.

## Who builds this

**Starter version:** this agent uses **web browsing + search** by default. That means it scans public complaints on Reddit, G2, Product Hunt, and support forums — not your private ticketing system. A PM can configure it solo in 30 minutes.

**Upgrade version:** to read your *private* Zendesk / Intercom / Freshdesk tickets, your engineer wires an MCP connection. Adds ~1 day of eng work but covers the tickets that never leave your help desk.

Pick based on where your signal actually lives. Consumer product? Reddit and G2 cover it. Enterprise product with NDA-bound customers? You need the MCP upgrade to see the real patterns.

## What to hand your engineer

1. This file
2. The agent ID from the Claude console (you'll generate it below)
3. Access to your support system
4. `managed-agents/engineer-handoff-brief.md` — the six things they need to define

## Setup

**Step 1.** Go to [platform.claude.com](https://platform.claude.com) → Managed Agents → Quickstart.

**Step 2.** Paste this directly into the "Describe your agent" box:

```
An agent that analyzes support ticket trends for [COMPANY],
a [ONE LINE: what your product does].

Every Monday at 6 AM, it searches for recent user complaints,
forum posts, and review site activity about [YOUR PRODUCT
CATEGORY] from the past 7 days.

It identifies recurring pain themes that appear 3 or more
times and ranks them by frequency. For each theme it notes
the theme name in the customer's own language, ticket count,
and whether it maps to any of these roadmap items:
[LIST YOUR CURRENT ROADMAP ITEMS].

It posts a Slack report to [CHANNEL ID]:

Support Pattern Report — Week of [date]
Theme | Count | On Roadmap?
[theme] | [n] | Yes / No / Unknown

Top 3 themes summarized in one sentence each using the
actual words customers used.
Final line: "Full ticket list available on request."

If fewer than 10 complaints are found, it posts:
"Low volume — [X] tickets. Not enough for pattern analysis."
```

**Step 3.** Click **Generate**. Review the YAML. Click **Create agent**.

**Step 4.** Copy the agent ID. Hand it to your engineer with:
- Access to your support system (Zendesk / Intercom / etc. MCP credentials)
- Slack MCP credentials (scoped to the target channel only)
- The `engineer-handoff-brief.md` file from this repo

## Iteration

You can tune the prompt inside the Managed Agent interface without redeploying. Hit the three-button menu next to **Edit** → **Guided Edit**. Claude walks you through prompt changes conversationally.

## What to expect

- **Week 1 report:** will be noisy. Ticket categorization from raw text takes tuning.
- **Week 2-3:** adjust the prompt when a theme is too broad ("UX issues") or too narrow ("button on /settings page is 2px off").
- **Week 4:** you have a feedback loop that surfaces what you were previously blind to.

## Guardrails to discuss with engineering

- **PII in tickets.** Ticket content often contains user names, emails, account IDs. Confirm this routes through your existing data handling policy.
- **Customer quotes in Slack.** Don't post direct quotes that identify individual customers in public channels. Use paraphrases or internal channels only.
- **Audit trail.** Every agent tool call is logged. Point your security team to the Sessions view.
