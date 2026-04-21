# Cowork Scheduled Tasks

**For work that needs your local files. Runs on your machine through the Claude Desktop app.**

---

## What Cowork is (vs. Routines, vs. Managed Agents)

| | **Cowork Scheduled Tasks** | **Routines** | **Managed Agents** |
|---|---|---|---|
| **Where it runs** | Your desktop (Claude app) | Anthropic's cloud | Anthropic Platform |
| **What it can touch** | Local files + connectors | Connectors + web only (no local files) | MCP + custom tools, per-user isolated |
| **Runs while laptop is closed?** | ❌ No | ✅ Yes | ✅ Yes |
| **Triggers** | Hourly, daily, weekly, weekdays, on-demand | Schedule + API webhook + GitHub | Per-user, API, long-running |
| **Permissions** | Asks before destructive actions | No prompts during run | Scoped per tool, logged per call |
| **Best for** | *"Save this markdown brief to ~/Documents every morning"* | *"Scan competitor pricing while I'm asleep, post to Slack"* | *"Every PM on the team queries the support-ticket agent for their area"* |
| **Available on** | Any paid plan, via Claude Desktop | Pro, Max, Team, Enterprise (on claude.ai/code/routines) | Enterprise/Platform (platform.claude.com) |

---

## When to pick Cowork over a Routine

Answer "yes" to any of these → use Cowork:

- **Does the work need to read files on your laptop?** PDFs in Downloads, meeting transcripts in Documents, Excel files in Desktop, etc. Routines can't see local files.
- **Do you want output as a local markdown/text file** you can grep later, commit to git, or drop into Obsidian/Bear/Notion-local? Routines can't write to local disk.
- **Is the "connector" you need actually a CLI or a local app?** Cowork can run shell commands via the Claude app.

If none of those apply, Routines is almost always the better choice — it runs while you sleep and doesn't require your laptop to be awake.

## When to pick a Routine over Cowork

- **Does it need to fire while your laptop is closed / you're on a flight / you're on vacation?** Routines run in the cloud.
- **Does the output need to land in Slack, Notion, Gmail?** Routines are already there.
- **Is it triggered by a webhook or a GitHub event?** Only Routines support those triggers.

## The honest take

Most PM use cases in this repo work better as Routines. The two in this folder are the cases where Cowork's local-file superpower genuinely matters.

---

## What's in this folder

- [`01-local-transcript-digest.md`](./01-local-transcript-digest.md) — Weekly scan of your local meeting transcripts folder. Produces one consolidated brief. This is the Cowork flagship — you probably have months of Zoom/Otter/Fireflies transcripts piling up locally right now.
- [`02-morning-brief-to-local-folder.md`](./02-morning-brief-to-local-folder.md) — The morning meeting brief Routine, but output is a markdown file on your desktop instead of a Slack DM. For PMs who live in Obsidian/Bear/local markdown workflows.

## Setup (applies to all Cowork tasks)

**Prerequisites:** Claude Desktop app installed (Mac/Windows). Any paid Claude plan.

**Step 1.** Open Claude Desktop.

**Step 2.** Settings → Scheduled Tasks → **New Scheduled Task**.

**Step 3.** Paste the prompt from the file you picked. Set the schedule. Click **Run Now** before scheduling — same rule as Routines.

**Step 4.** Grant Claude file system access when prompted. Point it at the specific folder the task needs (not your whole Documents folder — scope narrowly).

**Step 5.** Confirm the output landed where expected. Only then let the schedule run.

**The same five rules apply:**

1. End prompts with "Execute these steps immediately."
2. Remove unused connectors (Cowork also inherits your connected integrations).
3. Pick Sonnet 4.6, not Opus.
4. Define the output format explicitly.
5. Run Now before scheduling.

**The one difference:** Cowork won't run while your laptop is asleep, closed, or off. If you close your laptop before 7 AM on a Tuesday, the 7 AM task is skipped — it doesn't catch up. For anything mission-critical on a schedule, use a Routine.
