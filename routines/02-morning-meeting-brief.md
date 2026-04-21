# Routine 2: Morning Meeting Brief

**Weekdays at 7:30 AM. Reads your calendar, pulls relevant email history per meeting, writes a brief to your Slack DM.**

This is the Routine I run every single day. I walk into every conversation with context my peers are still manually assembling.

## What it produces

One paragraph per meeting, in your Slack DM before you open your laptop:

> **Product Review with [VP Eng], [Design Lead] — 10:00 AM**
> Participants: Maria K., Devon T.
> Context: Last conversation Apr 14 was about the pricing experiment results. Devon flagged that the control conversion looked suspicious; you said you'd dig into the segment-level data. Maria asked for the deck a day before the meeting. Open ask from her: whether to include the cohort-2 results or wait. You haven't replied. Lead with that.

## Connectors needed

- Gmail
- Google Calendar
- Slack

## Setup

**Step 1.** Connect Gmail, Google Calendar, and Slack at [claude.ai](https://claude.ai) → Customize → Connectors → `+`.

- For Gmail and Calendar, grant **full read access** during OAuth. The #1 cause of empty briefs is narrow permissions.
- For Slack: get your personal DM channel ID. Message yourself, click your own name in the thread, the ID is at the bottom of the popup.

**Step 2.** Go to [claude.ai/code/routines](https://claude.ai/code/routines) → **New Routine**.

- Name: `Morning Meeting Brief`
- Trigger: Schedule, weekdays at 7:30 AM
- Connectors: keep Gmail, Google Calendar, Slack — remove everything else
- Model: Sonnet 4.6

**Step 3.** Paste this into the description box:

```
You are preparing a morning briefing.

Every time you run, do the following in order:

1. Read my Google Calendar for today. List all meetings that have
   2 or more participants besides me.

2. For each of those meetings:
   a. Identify the other participants by name and email.
   b. Search my Gmail for the last 10 email threads that include
      any of those participants, from the last 45 days.
   c. Read those threads.
   d. Write one paragraph covering:
      – What we last discussed or worked on together
      – Any open asks or unresolved questions from either side
      – Anything I should be prepared to address today

3. Format as:

   **[Meeting Title] — [Time]**
   Participants: [Names]
   Context: [Your paragraph]

   Repeat for each meeting.

4. Post to my Slack DM at channel [YOUR PERSONAL CHANNEL ID].
   If I have no meetings with 2+ participants today, post:
   "No multi-participant meetings today."

Do not write anything back to me. Execute these steps immediately.
```

**Step 4.** Click **Run Now**. Check the Slack output. Only let the schedule run after confirming it works.

## What to expect

- **Day 1:** you'll be suspicious of how good this is. That's normal.
- **By Friday of week 1:** you'll notice you're more prepared than your peers and stop rereading threads manually.
- **Failure mode:** empty brief. Almost always Gmail permissions. Reconnect and grant full read access.

## Tuning

**If the briefs feel generic**, add product-specific context:

```
When summarizing meetings with engineers, prioritize open PRs, design specs, and API decisions.
When summarizing meetings with sales, prioritize deal status, objections, and pipeline asks.
```

**If you're new at your company or working with recent hires**, change the lookback from 45 days to 14 days:

```
b. Search my Gmail for the last 10 email threads that include
   any of those participants, from the last 14 days.
```

And add this fallback for sparse histories:

```
If there are fewer than 2 email threads with a participant,
write: "Context: Limited email history. Prepare cold —
review their role and the meeting title to set context
at the top of the meeting."
```

Otherwise you'll get empty paragraphs for meetings with recent contacts, which is worse than no brief at all.

**The more specific, the better the signal.**
