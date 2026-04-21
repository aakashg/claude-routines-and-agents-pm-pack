# Appendix: Getting Your Connector IDs

**One canonical reference. Every prompt that needs a channel ID, page URL, or database ID points here.**

---

## Slack channel ID

**For a public or private channel (desktop app OR web):**
1. Open Slack
2. Click the channel name at the top of the channel header
3. In the popup, click the **About** tab (may default to it)
4. Scroll to the bottom of the About section
5. Copy the Channel ID — starts with `C` (e.g. `C06PRODUCT1`)

**Alternative (works on web only):** look at the URL — `https://app.slack.com/client/T.../C06PRODUCT1` — the part after the last `/` that starts with `C` is the channel ID.

**For your personal DM (where Routines will post just to you):**
1. In Slack, click your own name in the sidebar (Messages → your name)
2. Click your name at the top of the DM
3. Scroll to the bottom of the popup
4. Copy the ID — starts with `D` (e.g. `D06MYSLACKDM`)

**For a DM with a specific coworker (not recommended — use channels):**
Same as personal DM, but open the DM with them first.

---

## Notion page URL

1. Open the Notion page you want Claude to write to
2. Click **Share** in the top right → **Copy link**
3. Paste the URL

**What a page URL looks like:**
```
https://www.notion.so/yourspace/Competitor-Pricing-Log-abc123def456
```
The 32-character hex string at the end is the page ID.

**What a database URL looks like** (note the `?v=` parameter, which page URLs don't have):
```
https://www.notion.so/yourspace/Meeting-Notes-DB-abc123def456?v=xyz789
```

**Use a page URL** when: the Routine overwrites the same page on each run (competitor pricing, OKR state).
**Use a database URL** when: the Managed Agent creates a new page per run (meeting transcripts, weekly reports).

---

## Gmail — no ID needed

Connect it once in Claude. Grant **full read access** during OAuth. The #1 cause of empty morning briefs is narrow Gmail permissions.

---

## Google Calendar — no ID needed

Connect it once. Grant read access. The Routine reads your primary calendar by default. To read a shared team calendar, add the email address of that calendar to the prompt.

---

## GitHub repo (for GitHub-triggered Routines)

1. Open the repo on github.com
2. The repo identifier is `owner/repo` — visible at the top of the page
3. Paste that into the repository picker in the Routine config

---

## Linear / Jira / Asana (for OKR pulse agent)

These use MCP connections wired by your engineer. Give your engineer the URL or ID of:
- Linear: the team ID (settings → teams) or a project URL
- Jira: the project key (e.g. `PROD`) or a filter URL
- Asana: the workspace ID or a project URL

---

## Webhook URL (for API-triggered Routines)

When you select the **API** trigger, Claude generates a URL and token on the Routine detail page. Copy both. Share with your engineer if they're calling it from your product.

Example:
```
curl -X POST https://hooks.routines.dev/pr-triage \
  -H "Authorization: Bearer rt_live_abc123..."
```

Rotate the token if it leaks. The Routine page has a "Regenerate" button.
