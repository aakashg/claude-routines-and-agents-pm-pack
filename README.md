# Claude Routines + Managed Agents — PM Pack

Companion repo for [Inside Anthropic's New Automation Layer: 7 Workflows PMs Can Run This Week](https://www.news.aakashg.com/p/claude-automation-pms).

Nine production-ready prompts across three surfaces (Cowork Scheduled Tasks, Routines, Managed Agents), sample outputs, engineer handoff brief, security doc, and a measurement framework. Copy, paste, ship.

---

## 🎯 Start here

**New to this? Run the [10-minute first win](./QUICKSTART.md) first.** It gets you to a working Routine with zero Notion setup, no engineer, and no complex OAuth. You'll understand the core loop before investing 30 minutes in a real use case.

**Already know how Routines work?** Use the decision tree below.

---

## Decision tree — which one do I build first?

```
What's your biggest blind spot right now?

├─ "I walk into meetings cold"
│     → routines/02-morning-meeting-brief.md  (personal, 20 min setup)
│
├─ "Sales finds out about competitor pricing before I do"
│     → routines/01-competitor-pricing.md  (personal, 15 min setup)
│
├─ "I have months of meeting transcripts I never re-read"
│     → cowork-tasks/01-local-transcript-digest.md  (personal, local files)
│
├─ "I want my morning brief as a markdown file, not Slack"
│     → cowork-tasks/02-morning-brief-to-local-folder.md  (personal, Obsidian-friendly)
│
├─ "I'm prioritizing off loudest tickets, not most common"
│     ├─ Solo PM, no eng capacity?
│     │     → routines/03-weekly-user-sentiment.md  (personal, public data only)
│     └─ Have an engineer?
│           → managed-agents/01-support-ticket-patterns.md  (team, ~1 day eng wiring)
│
├─ "Action items die after meetings"
│     → managed-agents/03-meeting-transcript-backlog.md  (team, ~1 day eng wiring)
│
├─ "OKRs reviewed once a quarter, guessed at in between"
│     → managed-agents/04-okr-pulse.md  (team, ~1 day eng wiring)
│
└─ "Competitors quietly ship things I miss"
      └─ Solo → routines/01-competitor-pricing.md
         Team → managed-agents/02-competitive-intelligence.md
```

**Pick one. Not three. Not all nine. Run it for a week. Then add the next.**

## Three surfaces, one decision

Anthropic shipped three ways to run AI on a schedule. Use this to pick:

| Surface | Where it runs | What it can touch | Laptop closed? | Best for |
|---|---|---|---|---|
| **Cowork Scheduled Tasks** | Your desktop | Local files + connectors | ❌ Must be awake | *"Save markdown briefs to ~/Documents/briefs"* |
| **Claude Routines** | Anthropic's cloud | Connectors + web (no local files) | ✅ Yes | *"Post to Slack DM while I'm asleep"* |
| **Managed Agents** | Anthropic's platform | MCP tools, per-user isolated | ✅ Yes | *"Every PM queries the support-ticket agent"* |

**Three questions to pick:**
1. Does the work need your **local files**? → Cowork.
2. Does it need to fire while you're **asleep, on a flight, or off your machine**? → Routine.
3. Does it need to serve **more than just you**, with per-user context? → Managed Agent.

---

## What's in here

```
├── QUICKSTART.md                      # 10-min first win — no Notion, no eng
├── README.md                          # This file
├── SECURITY.md                        # Send this to your security team
├── TRADEOFFS.md                       # Honest — what costs, what breaks
├── prompt-injection-mitigation.md     # Defense in depth for user-content agents
├── team-rollout-4-week-plan.md        # For PM managers rolling out to a team
├── appendix-connector-ids.md          # One canonical "getting IDs" reference
│
├── cowork-tasks/                      # For YOUR work with LOCAL files
│   ├── README.md                      # When to pick Cowork over Routines
│   ├── 01-local-transcript-digest.md  # Scan ~/Documents/Transcripts/ weekly
│   └── 02-morning-brief-to-local-folder.md  # Morning brief as markdown file
│
├── routines/                          # For YOUR work — no engineer, runs in cloud
│   ├── 01-competitor-pricing.md
│   ├── 02-morning-meeting-brief.md
│   ├── 03-weekly-user-sentiment.md
│   └── routines-checklist.md          # Verify after Run Now, before scheduling
│
├── managed-agents/                    # For your TEAM — engineer wires the last mile
│   ├── 01-support-ticket-patterns.md
│   ├── 02-competitive-intelligence.md
│   ├── 03-meeting-transcript-backlog.md
│   ├── 04-okr-pulse.md
│   └── engineer-handoff-brief.md      # Hand this to your eng team
│
├── sample-outputs/                    # What real outputs actually look like
│   ├── morning-meeting-brief.md
│   ├── support-ticket-patterns.md
│   ├── competitor-pricing-change.md
│   ├── okr-pulse.md
│   └── agent-config.example.yaml
│
└── measurement/
    ├── week-1-baseline.md             # What to measure before
    └── week-4-review.md               # What changed
```

---

## 60-second setup (for Cowork Scheduled Tasks)

If you want local file access and are fine with your laptop needing to be awake:

1. Install Claude Desktop ([claude.ai/download](https://claude.ai/download))
2. Settings → Scheduled Tasks → **New Scheduled Task**
3. Copy a prompt from `/cowork-tasks` into the task description
4. Grant file system access when prompted — **scope narrowly** (one folder, not all of Documents)
5. Click **Run Now** before scheduling
6. Confirm the output file landed. Then let the schedule run.

**Gotcha:** Cowork won't run while your laptop is asleep or closed. Missed runs don't catch up. For anything mission-critical on a schedule, use a Routine instead.

## 60-second setup (for Routines)

If you have a paid Claude plan (Pro, Max, Team, Enterprise):

1. [claude.ai](https://claude.ai) → Customize → Connectors → `+` → connect Slack, Gmail, Google Calendar, Notion (as needed)
2. [claude.ai/code/routines](https://claude.ai/code/routines) → **New Routine**
3. Copy a prompt from `/routines` into the description box
4. Pick a trigger (Schedule / Webhook / GitHub)
5. **Remove unused connectors** (important — Claude can use any connected tool without asking)
6. Click **Run Now** before scheduling — always
7. Once it works end-to-end, let the schedule take over

**Connector IDs:** see [appendix-connector-ids.md](./appendix-connector-ids.md) — one canonical reference.

## 60-second setup (for Managed Agents)

1. [platform.claude.com](https://platform.claude.com) → Managed Agents → Quickstart
2. Copy a prompt from `/managed-agents` into "Describe your agent"
3. **Generate** → review the YAML ([example](./sample-outputs/agent-config.example.yaml)) → **Create agent**
4. Copy the agent ID, hand to your engineer with [engineer-handoff-brief.md](./managed-agents/engineer-handoff-brief.md)

---

## The five rules (skip at your peril)

1. **End every prompt with "Execute these steps immediately."** Otherwise the Routine narrates instead of running.
2. **Remove unused connectors.** By default every Routine can read/write everything you've connected.
3. **Pick Sonnet 4.6, not Opus,** for monitoring tasks. Opus is slower and overkill.
4. **Define the output format explicitly.** Otherwise structure drifts run to run.
5. **Always Run Now before scheduling.** Silent failures burn your daily limit.

## Plan limits

| Plan | Runs/day | Min trigger interval |
|---|---|---|
| Pro | 5 | 1 hour |
| Max | 15 | 1 hour |
| Team | 25 | 1 hour |
| Enterprise | 25 | 1 hour |

## The stateless problem

Each Routine run starts completely fresh. No memory of yesterday.

**Fix:** write today's findings to Notion at the *end* of each run. Read that page at the *start* of the next. Every prompt in this repo handles this. Don't remove those steps.

---

## For teams: rolling this out across a PM org

If you manage PMs or want to standardize this across a product team, **read [team-rollout-4-week-plan.md](./team-rollout-4-week-plan.md)**. It's the concrete week-by-week playbook.

Short version:

1. **Shared channel naming.** `#pm-intel-[name]` for personal Routines, `#team-intel` for Managed Agents.
2. **Shared Notion workspace.** One database per agent type — not one per PM.
3. **Weekly review ritual.** 15 min at Monday standup: scan last week's outputs together.
4. **Shared prompt library.** Fork this repo. PRs when PMs tune something that works.
5. **Budget as a line item.** ~$5/week per PM + $20-50/week for shared Managed Agents.
6. **Security review once, not per-PM.** Use [SECURITY.md](./SECURITY.md) + [prompt-injection-mitigation.md](./prompt-injection-mitigation.md).

---

## For security teams

Start with [SECURITY.md](./SECURITY.md). One-page data flow summary, sensitivity tiers per agent, compliance notes.

## For engineers

Start with [managed-agents/engineer-handoff-brief.md](./managed-agents/engineer-handoff-brief.md). The six things you need from the PM, pricing math, security checklist, and sample YAML.

## For solo PMs (no eng support)

You can run everything in `/routines/` and `/cowork-tasks/` today, no eng needed. The four in `/managed-agents/` require an engineer. That's not a soft requirement — they need MCP connections to your company's ticketing/PM tools, which require creds and wiring.

---

## Honest expectations (read before starting)

- **Week 1 reports will be noisy.** Tune after a week, not after a day.
- **~1-2% of runs fail silently.** Check run logs when output looks weird.
- **Costs are small** (~$5/week for all seven at typical volume — see [TRADEOFFS.md](./TRADEOFFS.md)).
- **This isn't zero-error data work.** Judgment tasks only. Don't pipe to compliance audits.

---

## License & feedback

MIT. Fork freely. If a prompt works well after tuning, PR it back.

Questions? Reply to the newsletter.
