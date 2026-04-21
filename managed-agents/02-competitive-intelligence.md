# Managed Agent 2: Team-Wide Competitive Intelligence

**Sunday night at 10 PM. Visits competitor websites, changelogs, blogs, job postings, and G2 reviews. Writes a full Notion report. Posts the single most important move to Slack Monday morning.**

Walk into Monday planning knowing exactly what moved in your competitive landscape over the weekend.

## What it produces

**A Notion page** titled "Competitive Intelligence — Week of [date]":

```
## Competitor 1
Positioning changes: [bullets]
Shipped last 30 days: [bullets]
Strategic signals: [bullets]
G2 praise themes: [bullets]
G2 complaint themes: [bullets]

(repeats per competitor)

## Synthesis
Biggest threat to our positioning: [one paragraph]
Best gap to exploit: [one paragraph]
What to watch next week: [one paragraph]
```

**Plus a one-paragraph Slack summary** to a shared channel on Monday morning with a Notion page link and the single most important move from the week.

## Who builds this

Engineer-wired. Needs Notion MCP, Slack MCP, and web browsing — the latter two are built in, Notion you'll connect.

## Setup

**Step 1.** Go to [platform.claude.com](https://platform.claude.com) → Managed Agents → Quickstart.

**Step 2.** Paste this into "Describe your agent":

```
An agent that runs competitive intelligence research for [COMPANY],
a [ONE LINE: what your product does].

Every Sunday at 10 PM, it visits the public websites, changelogs,
blogs, product pages, and job posting pages of [COMPETITOR 1],
[COMPETITOR 2], and [COMPETITOR 3]. For each competitor it notes
positioning changes, features shipped in the last 30 days, strategic
announcements, and new hiring patterns that signal expansion
(e.g. enterprise sales hires, new geo openings).

It then reads the 10 most recent G2 reviews per competitor and pulls
out recurring praise themes and recurring complaints.

It writes a Notion page in [NOTION DATABASE OR PARENT PAGE URL]
titled "Competitive Intelligence — Week of [date]" with this structure:

  ## [Competitor 1]
  Positioning changes: [bullets]
  Shipped last 30 days: [bullets]
  Strategic signals: [bullets]
  G2 praise themes: [bullets]
  G2 complaint themes: [bullets]

  (repeat per competitor)

  ## Synthesis
  Biggest threat to our positioning: [one paragraph]
  Best gap to exploit: [one paragraph]
  What to watch next week: [one paragraph]

It posts a one-paragraph Slack summary to [CHANNEL ID] with the
Notion page link and the single most important move from the week.

If a competitor page fails to load, it names the failing URL in
the Notion page under that competitor and continues with the rest.
If fewer than 2 competitors return usable data, it posts to Slack:
"Competitive scan incomplete — [X] of [Y] sources failed. Manual
review needed."
```

**Step 3.** Click **Generate** → review YAML → **Create agent**.

**Step 4.** Copy the agent ID. Hand to engineering with the handoff brief.

## Iteration

**After first run:** Expect gaps where competitor pages were hard to read (JS-heavy, gated, CAPTCHA'd). Note which URLs consistently fail. Give engineering a list of alternatives — the competitor's changelog, pricing blog, or G2 page usually works when the main marketing site doesn't.

**After three weeks:** the report stabilizes. You'll know which competitors are moving fast vs. stagnating.

## Guardrails to discuss with engineering

- **Rate limiting.** Hitting competitor sites weekly is fine. Don't let this fire hourly during iteration.
- **User-agent.** Use a descriptive user-agent string, not spoofed. Competitor security teams can and do block.
- **Don't paraphrase into misrepresentation.** The agent should quote competitor copy, not reinterpret it into claims they didn't make.
