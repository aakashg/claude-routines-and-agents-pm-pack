# Cowork Task 1: Local Transcript Digest

**Weekly on Monday at 7 AM. Scans your local meeting transcripts folder. Produces one consolidated brief with action items, decisions, and open threads from the week. Saves to `~/Documents/briefs/`.**

This is the Cowork flagship. If you use Zoom / Otter / Fireflies / Granola, you've got a folder of transcripts piling up that you haven't re-read. This turns that pile into one weekly briefing.

**Why this is Cowork, not a Routine:** your transcripts live on your laptop. Routines can't read them. Cowork can.

## What it produces

A markdown file at `~/Documents/briefs/weekly-brief-YYYY-MM-DD.md`:

```
# Weekly Brief — Week of Apr 21, 2026

## Meetings analyzed
- Product Review (Apr 15) — 52 min
- 1:1 with Maria (Apr 16) — 28 min
- Design Sync (Apr 17) — 41 min
- Customer Call: Acme Corp (Apr 18) — 45 min
- Sprint Retro (Apr 18) — 60 min

## Action items I committed to
- [ ] Segment-level pricing data pull — Due: Apr 22 (from Product Review)
- [ ] Review Alex's revised onboarding mocks — Due: Apr 21 (from Design Sync)
- [ ] Send Acme the Q3 roadmap slide — Due: Apr 25 (from Customer Call)

## Decisions made
- Ship cohort-2 pricing test results in next week's review (not hold for cohort-3)
- Kill the first-run checklist initiative — replace with guided tour
- Move mobile redesign out of Q2 to Q3

## Open questions (raised but not resolved)
- "Do we tell Acme about the API v3 deprecation now or at renewal?" — raised by me, Apr 18
- "Is the SSO initiative actually a Q2 commitment or a stretch?" — raised by Maria, Apr 16

## Threads worth revisiting
- The pricing test conversation (Apr 15) — Devon flagged a segmenting concern I haven't followed up on
- Maria's career trajectory comment in 1:1 (Apr 16) — bring to next 1:1
```

## Setup

**Step 1.** Open Claude Desktop → Settings → Scheduled Tasks → **New Scheduled Task**.

**Step 2.** Configure:
- Name: `Weekly Transcript Digest`
- Schedule: Weekly, Monday at 7:00 AM
- Model: Sonnet 4.6

**Step 3.** Paste this prompt (adjust the folder path to wherever your transcripts actually live — common options: `~/Documents/Transcripts/`, `~/Documents/Otter/`, `~/Library/Application Support/zoom.us/recordings/`, etc.):

```
You are producing a weekly meeting digest.

Every time you run, do the following in order:

1. Read all files in ~/Documents/Transcripts/ modified in the
   last 7 days. Include .txt, .vtt, .srt, .md, and .docx formats.
   If the folder doesn't exist or is empty, write a brief stating
   "No transcripts found this week" and stop.

2. For each transcript, identify:
   - Meeting name (from filename or the first line of the
     transcript)
   - Date (from file metadata or the transcript header)
   - Approximate duration (from the transcript if available,
     otherwise skip)

3. Across all transcripts from this week, extract:
   - Action items I (the primary speaker / owner of this laptop)
     committed to. Include the item, the due date if mentioned,
     and which meeting it came from.
   - Decisions the group(s) reached — one sentence each, with
     the meeting source.
   - Open questions that were raised but not resolved, with who
     raised them and which meeting.
   - Threads worth revisiting — unresolved tensions, follow-ups
     I promised but haven't done, or moments where someone said
     something I should come back to.

4. Write a markdown file to ~/Documents/briefs/weekly-brief-
   [YYYY-MM-DD].md with this structure:

   # Weekly Brief — Week of [date]

   ## Meetings analyzed
   (bulleted list: meeting name, date, duration)

   ## Action items I committed to
   - [ ] [action] — Due: [date if known] (from [meeting])

   ## Decisions made
   - [one-sentence decision] (from [meeting])

   ## Open questions (raised but not resolved)
   - "[question]" — raised by [person], [date]

   ## Threads worth revisiting
   - [brief note] (from [meeting])

5. If the ~/Documents/briefs/ folder doesn't exist, create it.

6. Do not delete or modify any original transcript files.

Do not write anything back to me. Execute these steps immediately.
```

**Step 4.** Grant Claude access to `~/Documents/Transcripts/` and `~/Documents/briefs/` when prompted. Scope narrowly — don't grant whole-Documents access unless you need to.

**Step 5.** Click **Run Now**. Wait 1-2 minutes (transcript parsing takes longer than web work). Open `~/Documents/briefs/` and verify the markdown file is there and readable.

## What to expect

- **Week 1:** the first run may over-include. Transcripts often conflate "Maria mentioned maybe doing X" with "Maria committed to doing X." Tune by adding: *"Only list action items where the owner explicitly said 'I will,' 'I'll,' or 'I'm going to.' Do not infer commitments from 'maybe' or 'could.'"*
- **Week 2-3:** the pattern stabilizes. You'll notice action items you'd completely forgotten.
- **Ongoing:** 10 minutes of reading on Monday morning replaces ~45 minutes of scattered thread re-reading.

## If your transcripts live in the cloud, not on your laptop

If you use Google Drive / Dropbox / iCloud for transcript storage, two options:

**Option A (recommended):** enable the desktop sync client. Google Drive, Dropbox, and iCloud all have desktop apps that mirror cloud folders locally. Point Claude at the synced folder (e.g. `~/Google Drive/My Drive/Transcripts/` or `~/Library/Mobile Documents/com~apple~CloudDocs/Transcripts/`).

- ✅ Works with Cowork — the files appear as local files
- ✅ Keeps cloud source of truth
- ⚠ Requires the sync client to be running

**Option B:** skip Cowork entirely and use the Managed Agent version ([`managed-agents/03-meeting-transcript-backlog.md`](../managed-agents/03-meeting-transcript-backlog.md)) with a Google Drive MCP connector. Works for teams, not solo PMs.

## File size guidance

- **Under 100KB per transcript** (typical 30-60 min meeting): no issues
- **100KB-1MB**: works, but slower. Expect 2-3 min runs instead of under a minute.
- **Over 1MB**: often means audio files got in alongside transcripts, or you have multi-hour workshop transcripts. Add a filter to the prompt: `Only read files under 500KB — skip larger files and note them as "skipped: too large" in the output.`

If the task times out or errors, file size is the most common cause.

## When it breaks

- **No output file.** Almost always a permissions issue. Re-prompt and grant access when Claude asks.
- **Transcript format not recognized.** Add the specific format to the prompt (`Include .txt, .vtt, .srt, .md, .docx, and .json`).
- **Hallucinated action items.** Tune with the "explicitly said 'I will'" guardrail above.
- **Task didn't run at 7 AM Monday.** Your laptop was asleep. Cowork won't catch up on missed runs. Either keep your laptop awake Sunday night, or migrate this task to a Routine + a Notion-based alternative (less ideal — Routines can't read local transcripts).

## Variant: Daily, not weekly

Change the schedule to "daily, weekday mornings at 7:30 AM" and the lookback from `last 7 days` to `last 24 hours`. You get a briefing the morning after each meeting day.

Tradeoff: daily can feel repetitive on light meeting days. Weekly consolidates better.
