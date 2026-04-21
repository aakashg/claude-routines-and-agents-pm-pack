# Cowork Task 2: Morning Brief to Local Markdown

**Weekdays at 7:30 AM. Reads your calendar, pulls email history per meeting, saves a briefing as a markdown file to `~/Documents/briefs/`.**

This is the same morning meeting brief as `routines/02-morning-meeting-brief.md`, but output lands as a local markdown file instead of a Slack DM. For PMs who live in Obsidian, Bear, Logseq, or any local-markdown workflow.

**Why this is Cowork, not a Routine:** you want the brief as a file you can commit to git, pipe into Obsidian, or grep from Terminal. Routines can't write to local disk. Cowork can.

## What it produces

A markdown file at `~/Documents/briefs/daily-YYYY-MM-DD.md`:

```
# Morning Brief — Tuesday, Apr 21, 2026

## Product Review — 10:00 AM
Participants: Maria K., Devon T.
Context: Last conversation Apr 14 was about the pricing experiment
results. Devon flagged that control conversion looked suspicious;
you said you'd dig into the segment-level data. Maria asked for
the deck a day before the meeting. Open ask from her: whether to
include cohort-2 results or wait. You haven't replied. Lead with
that.

## Quarterly Planning Sync — 11:30 AM
Participants: Priya R., James L.
Context: Priya forwarded you a note last Friday about the
enterprise pipeline; she wants your take on whether we should
prioritize the SSO initiative or the audit log one in Q2. James
has been pushing audit log based on two active deals. Priya hasn't
weighed in yet. Come with a clear recommendation, not options.

## Design Review — 2:00 PM
Participants: Alex W., Sarah C.
...
```

Same content as the Slack version, different destination.

## Setup

**Step 1.** Open Claude Desktop → Settings → Scheduled Tasks → **New Scheduled Task**.

**Step 2.** Configure:
- Name: `Morning Meeting Brief (local)`
- Schedule: Weekdays at 7:30 AM
- Model: Sonnet 4.6

**Step 3.** Make sure Gmail and Google Calendar are connected to Claude. Grant full read access during OAuth.

**Step 4.** Paste this prompt:

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

   ## [Meeting Title] — [Time]
   Participants: [Names]
   Context: [Your paragraph]

   Repeat for each meeting.

4. Save the full briefing to ~/Documents/briefs/daily-[YYYY-MM-DD].md
   with a top-level header: "# Morning Brief — [Day, Date]"

5. If ~/Documents/briefs/ doesn't exist, create it.

6. If I have no meetings with 2+ participants today, write a file
   with just: "# Morning Brief — [Day, Date]\n\nNo multi-participant
   meetings today."

Do not write anything back to me. Execute these steps immediately.
```

**Step 5.** Grant Claude access to `~/Documents/briefs/` when prompted.

**Step 6.** Click **Run Now**. Open the file in your editor of choice. Confirm it's useful.

## Integration with Obsidian / Bear / Logseq

Point Claude at your vault instead of `~/Documents/briefs/`:

**On macOS:**
- **Obsidian (iCloud vault):** `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/[VaultName]/Daily/`
- **Obsidian (local vault):** `~/Documents/Obsidian/[VaultName]/Daily/`
- **Bear:** Bear doesn't use a file folder — skip this variant or export manually
- **Logseq:** `~/Logseq/[graph-name]/journals/`

**On Windows:**
- **Obsidian (local vault):** `C:\Users\[you]\Documents\Obsidian\[VaultName]\Daily\`
- **Obsidian (OneDrive vault):** `C:\Users\[you]\OneDrive\Obsidian\[VaultName]\Daily\`
- **Logseq:** `C:\Users\[you]\Logseq\[graph-name]\journals\`

**Use forward slashes in the prompt** even on Windows — Claude Desktop handles path normalization.

Then the brief auto-appears in your daily note without any sync step.

**Optional:** add frontmatter to the output so Obsidian/Logseq treats it correctly. Add this to the prompt after "top-level header":

```
Include YAML frontmatter at the very top of the file:
---
date: [YYYY-MM-DD]
type: morning-brief
tags: [daily-note, brief]
---
```

## Cowork vs. Routine for this use case

| | **Cowork** (local file) | **Routine** (Slack DM) |
|---|---|---|
| Runs while laptop is closed | ❌ No | ✅ Yes |
| Works on vacation / flights | ❌ No | ✅ Yes |
| Output grep-able from terminal | ✅ Yes | ❌ No |
| Output auto-syncs into Obsidian | ✅ Yes | ❌ No |
| You can read it on your phone at breakfast | ❌ No | ✅ Yes |

**Honest recommendation:** most PMs should use the Routine version. Slack on your phone at 7:35 AM is better than a markdown file you have to open your laptop for. Use this Cowork variant only if your workflow genuinely lives in local markdown.

## When it breaks

Same failure modes as the Routine version (empty Gmail results, permissions issues), plus:

- **File written but empty.** Check that Calendar and Gmail connectors are connected *to Claude Desktop*, not just to claude.ai. Cowork uses the Desktop-side auth, which is sometimes separate.
- **Task skipped on Mondays.** You closed your laptop Sunday night. Consider Caffeinate (`caffeinate -d -u` on Mac) or migrating this specific use case back to a Routine.
