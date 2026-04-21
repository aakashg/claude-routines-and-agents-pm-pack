# Routine 3: Weekly User Sentiment Scan

**Every Monday at 7 AM. Scans Reddit, Product Hunt, G2, and X for posts about your product category. Posts ranked pain points to Slack before planning.**

Your escalated tickets tell you what the loudest users think. This tells you what the market is actually saying — in their own language.

## What it produces

> **User Sentiment Report — Week of [date]**
>
> **Top Pain Points**
> 1. "onboarding takes forever" (14 mentions) — *"spent my whole first day just trying to get the thing connected"*
> 2. "pricing jumps too aggressively" (9 mentions) — *"went from $29 to $199 overnight when we added the 6th seat"*
> 3. "no bulk actions" (6 mentions) — *"I'm clicking the same checkbox 80 times, there has to be a better way"*
>
> **Feature Requests This Week**
> 1. CSV export from dashboard (5 mentions)
>
> **Platforms scanned:** Reddit, Product Hunt, G2, X

## Connectors needed

- Slack only (this uses web browsing for everything else — Zapier can't do this)

## Setup

**Step 1.** Make sure Slack is connected.

**Step 2.** Go to [claude.ai/code/routines](https://claude.ai/code/routines) → **New Routine**.

- Name: `Weekly User Sentiment`
- Trigger: Schedule, weekly on Monday at 7:00 AM
- Connectors: **keep only Slack. Remove everything else.**
- Model: Sonnet 4.6

**Step 3.** Paste this into the description box:

```
You are doing weekly product discovery research.

Every time you run, do the following in order:

1. Search Reddit, Product Hunt, G2, and X (Twitter) for posts and
   reviews about [YOUR PRODUCT CATEGORY] from the last 7 days.
   Focus on posts with 10+ upvotes or 5+ replies. Exclude posts
   that are promotional, sponsored, or by company accounts.

2. Read the content of the top 30 most-engaged posts and reviews.
   Full text, not just titles.

3. Identify recurring pain point themes. A theme is a complaint or
   frustration that appears in 3 or more separate posts.
   Do not create a theme for a single user's unique situation.

4. For each theme, record:
   – Theme name (use the actual language users used, not cleaned-up
     product language)
   – Number of posts expressing this frustration
   – One direct quote that best represents the theme
   – Which platform it appeared on most

5. Rank themes by frequency, highest first.

6. Note any feature requests that appeared in 3+ posts.
   Same format: request name, count, best quote, platform.

7. Post to Slack channel [YOUR CHANNEL ID]:

   **User Sentiment Report — Week of [date]**

   **Top Pain Points**
   1. [Theme] ([count] mentions) — "[quote]"
   2. [Theme] ([count] mentions) — "[quote]"
   (all themes with 3+ mentions)

   **Feature Requests This Week**
   1. [Request] ([count] mentions)
   (all with 3+ mentions)

   **Platforms scanned:** Reddit, Product Hunt, G2, X

Do not write anything back to me. Execute these steps immediately.
```

**Step 4.** Click **Run Now**. Check the output.

- If results feel too broad, narrow the product category. Add a competitor name to focus on people already in your market.
- If the report comes back thin (under 5 themes), broaden the category.

## What to expect

- **The first report will feel uncomfortable.** You will find users complaining about things you thought were fixed. That's the point.
- **Week-to-week noise is real.** Single-week themes might be noise. Watch what appears in 3 out of 4 weeks — that's signal.

## Advanced: pipe the output into your product

The API trigger gives you a webhook URL. Share it with your engineer. They can call it from your product (e.g., in an internal admin panel) to refresh sentiment on demand — not just on the Monday schedule.
