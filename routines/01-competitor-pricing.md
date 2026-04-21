# Routine 1: Competitor Pricing Monitor

**Daily at 8 AM. Checks competitor pricing pages. Posts only what changed to Slack.**

Use this when you keep finding out about competitor pricing changes on sales calls — after your team has already fumbled the objection.

## What it produces

- **Nothing changed:** one-line Slack message. `"Competitor check complete. No changes. [Date]"`
- **Something changed:** short Slack alert with exactly what moved. Full pricing snapshot written to your Notion log.

## Connectors needed

- Slack
- Notion

**Remove the rest** (Gmail, Calendar, Drive) when you create the Routine. Otherwise Claude has write access to things this task doesn't need.

## Setup

**Step 1.** Connect Slack and Notion at [claude.ai](https://claude.ai) → Customize → Connectors → `+`.

For Slack: copy your channel ID. Click the channel name in Slack, scroll to the bottom of the popup — the ID starts with `C`.

**Step 2.** Create an empty Notion page called "Competitor Pricing Log." Copy its URL.

**Step 3.** Go to [claude.ai/code/routines](https://claude.ai/code/routines) → **New Routine**.

- Name: `Competitor Pricing Monitor`
- Trigger: Schedule, daily at 8:00 AM
- Connectors: keep Slack and Notion, remove the rest
- Model: Sonnet 4.6 (not Opus — slower and overkill for this)

**Step 4.** Paste this prompt, filling in the brackets:

```
Every morning at [TIME], browse the pricing pages of
[COMPETITOR 1], [COMPETITOR 2], and [COMPETITOR 3].

Extract all plan names, prices, features, and promotions
visible on each page.

Compare against yesterday's findings stored in a Notion
page at [NOTION PAGE URL].

If nothing changed, post one line to Slack channel
[CHANNEL ID]: "Competitor check complete. No changes. [Date]"

If something changed, post exactly what changed as:
[Competitor]: [What changed]. Under 150 words.

Overwrite the Notion page with today's full findings as
a table: Plan Name | Price | Key Features. Add a
"Last checked: [Date]" timestamp at the top.

Do not write anything back to me. Execute these steps immediately.
```

**Step 5.** Click **Run Now** from the Routine page. Watch it. Confirm it read the pages, wrote to Notion, posted to Slack. Only let the schedule run after end-to-end verification.

## What to expect

- **Week 1 noise you'll see and should ignore:**
  - Day 1: "changes detected" because there's no prior Notion state to compare against. Expected.
  - Day 2-3: promotional banner rotations ("Save 20% this week!") flagged as changes. Real but ephemeral.
  - Day 3-4: minor marketing copy changes ("Build faster" → "Ship faster"). Noise.
  - Formatting differences (whitespace, bullet style). Noise.
- **After ~4 days** the comparison stabilizes to real changes only.
- **Ongoing:** 1-2 real alerts per month for most categories. Most days you'll see "No changes."

**If noise persists past week 1**, tighten the prompt: "Flag only changes to plan names, prices, or core feature lists. Ignore promotional banners, layout changes, and marketing copy revisions."

## When it breaks

- **Page fails to load.** JavaScript-heavy pricing pages, login walls, and CAPTCHAs cause read failures. The Routine names the failing URL in the Slack message. Swap it for the competitor's changelog, pricing blog, or G2 page.
- **No Slack output at all.** Open the run log on the Routine page. It shows exactly which step failed and why. Faster than re-reading the prompt.
- **Routine narrates instead of running.** You skipped "Execute these steps immediately." at the end. Add it back.
