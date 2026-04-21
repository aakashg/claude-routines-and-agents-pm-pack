# Managed Agent 3: Meeting Transcript → Structured Backlog

**On demand. Receives a meeting transcript. Extracts every action item, decision, open question, and follow-up. Writes a structured Notion page. Posts a Slack summary.**

We all have a folder of meeting recordings we haven't gone back to in months. Commitments live in memory. Open questions get reopened two weeks later. The decision from Tuesday's product review disappears because the follow-up task was never written.

## What it produces

**A Notion page** titled "[Meeting Name] — [Date]":

```
## Action Items
- [ ] [action] — Owner: [name] — Due: [date]

## Decisions Made
- [one-sentence statement of what was decided]

## Open Questions
- [question] — Raised by: [name]

## Follow-ups
- [follow-up] — Date: [date]
```

**A Slack summary** in the same channel the same day:

> **Product Review — Apr 21:** 7 action items, 3 decisions, 2 open questions. [Notion link]

## Who builds this

Engineer-wired. The agent needs three things:
1. **Notion MCP (write access)** — to create the structured page
2. **Slack MCP** — to post the summary
3. **A way for transcripts to reach the agent** — three common mechanisms:

| Input mechanism | How it works | Effort to set up |
|---|---|---|
| **Otter/Fireflies webhook** | Both tools support posting transcripts to a custom URL on meeting end. Point it at the agent's API trigger. | 30 min per integration |
| **Zoom cloud recording + script** | Zoom can email transcripts. A small server script receives them and forwards to the agent. | ~2 hours |
| **Manual upload via shared Slack channel** | PMs paste transcripts into `#transcripts-intake`. An agent-trigger bot picks them up. | 1 day (need the bot) |

Pick whichever matches your meeting-recording tool. If you don't record meetings today, this agent is premature — start with the Cowork `01-local-transcript-digest.md` task instead, which reads what you already have.

## Setup

**Step 1.** Go to [platform.claude.com](https://platform.claude.com) → Managed Agents → Quickstart.

**Step 2.** Paste this into "Describe your agent":

```
An agent that converts meeting transcripts into structured Notion
pages for [COMPANY]'s [TEAM NAME] team.

When given a transcript, it extracts:

1. Every committed action item with owner name and deadline
2. Every decision the group reached
3. Every open question that was raised but not resolved, with
   who raised it
4. Every follow-up or next meeting agreed to, with date

It creates a Notion page in [NOTION MEETING NOTES DATABASE URL]
titled "[Meeting Name] — [Date]" with this structure:

  ## Action Items
  - [ ] [action] — Owner: [name] — Due: [date]

  ## Decisions Made
  - [one-sentence statement of what was decided]

  ## Open Questions
  - [question] — Raised by: [name]

  ## Follow-ups
  - [follow-up] — Date: [date]

It posts to Slack channel [CHANNEL ID]:
"[Meeting Name]: [N] action items, [N] decisions, [N] open
questions. [Notion link]"

If an action item has no clear owner in the transcript, it lists
the owner as "UNASSIGNED — clarify with team" rather than guessing.

If the transcript is under 500 words, it adds a note at the top of
the Notion page: "⚠ Short transcript — verify action items directly
with participants before relying on this list."

If no action items, decisions, or open questions are found, it
posts to Slack: "[Meeting Name]: No structured items extracted.
Transcript may be incomplete or conversational."
```

**Step 3.** Click **Generate** → review YAML → **Create agent**.

**Step 4.** Copy the agent ID. Hand to engineering for the transcript-input wiring.

## Iteration

**After launch:** iterate on the connectors, the system prompt, and tune accordingly.

Common tunes:
- **Owners not being assigned.** Transcripts often say "I'll do it" without naming the speaker. Add: *"Use the speaker's name from the transcript metadata — do not use first-person pronouns as owner names."*
- **Too many "follow-ups" that are really action items.** Tighten the distinction in the prompt.
- **Missing nuance from debate.** For high-stakes meetings, add a "Debate" section to capture the reasoning behind decisions.

## Guardrails to discuss with engineering

- **Transcript sensitivity.** HR, legal, and customer-call transcripts have different handling rules. Build channel-level routing — don't pipe everything to one Notion database.
- **Participant consent.** If you're piping external (customer, partner) calls through an AI that writes to a shared workspace, confirm this is disclosed.
- **Retention.** Decide up front how long transcripts sit in the session log.
