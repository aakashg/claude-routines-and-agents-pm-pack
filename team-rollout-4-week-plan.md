# Team Rollout — 4-Week Plan

**For Heads of Product or PM managers with 3-10 reports.** This is the concrete playbook for making Routines/Agents a team habit, not a novelty.

---

## Week 0 — Before you start (2 hours of your time)

- [ ] **Read the repo yourself.** Don't delegate the evaluation. If the playbook is bad, you catch it before your team does.
- [ ] **Get security approval** with [SECURITY.md](./SECURITY.md). Once, for the pattern. Not per-PM.
- [ ] **Pick the one Routine your team will standardize on in week 1.** Recommendation: `routines/02-morning-meeting-brief.md` — lowest-stakes, highest-daily-value.
- [ ] **Set up shared Slack channels.** `#pm-intel-meeting-briefs`, `#pm-intel-competitor-moves`, `#team-intel` for Managed Agent outputs.
- [ ] **Set up a shared Notion workspace.** One database per agent type.

## Week 1 — Everyone runs one Routine

**Goal:** Every PM on your team has one working Routine by Friday.

**Monday standup (10 min):**
- Announce the initiative. Share the repo link.
- Walk through the [QUICKSTART](./QUICKSTART.md) live. Show your AI Daily output from your own DM.
- Assign the standard Routine for the week.

**By Wednesday:**
- Each PM has completed [week-1-baseline.md](./measurement/week-1-baseline.md). Honest time estimates on the activities they're automating.
- Each PM has the standard Routine running and has hit Run Now successfully.

**Friday standup (15 min):**
- Round the room. Each PM shares: what worked, what broke, what surprised.
- Note common failure modes to the team doc (this becomes the local FAQ).

**Milestone:** 100% of team has one Routine running. Not "set up." Running, producing output.

## Week 2 — Tune and add a second

**Goal:** First Routine is tuned. Second Routine is running.

**Monday standup:**
- Team review: pull up last week's Slack outputs. What was useful? What was noise?
- Tune together: edit prompts live based on common noise patterns.

**By Friday:**
- Each PM has added a second Routine from the decision tree in README.
- Noise level from Routine 1 should be down 50%+ vs. week 1.

**Milestone:** Every PM running two Routines. First one tuned.

## Week 3 — Managed Agents for the team

**Goal:** One team-wide Managed Agent in production.

**Monday:**
- Pick ONE from the `/managed-agents/` folder. Recommendation: `managed-agents/01-support-ticket-patterns.md` or `managed-agents/04-okr-pulse.md` depending on your biggest blind spot.
- Engineer kickoff: hand them [engineer-handoff-brief.md](./managed-agents/engineer-handoff-brief.md) plus the agent file.
- You write the brief with brackets filled in. Engineer wires connectors and permissions.

**By Friday:**
- Agent is deployed in production.
- First weekly report has posted to a shared channel.

**Milestone:** Team has a shared Monday-morning report that didn't exist before.

## Week 4 — Review and decide

**Goal:** Data-driven decision on what to keep, tune, or kill.

**Monday standup (30 min, special agenda):**
- Each PM completes [week-4-review.md](./measurement/week-4-review.md).
- Present as a team: time saved, decisions changed, false positives, what broke.
- Group decision: which Routines/Agents become team standards? Which get killed?

**By Friday:**
- Team charter updated with "standard Routines" all PMs are expected to run.
- Shared repo fork of this pack, with your team's tuned prompts.

**Milestone:** Routines/Agents are a team practice, not an experiment.

---

## Ongoing rituals (month 2+)

| Frequency | Ritual | Time |
|---|---|---|
| **Daily** | Individual PMs read their Routine outputs as part of their morning routine | 5 min |
| **Weekly (Mondays)** | Team scans last week's Managed Agent outputs in standup | 15 min |
| **Monthly** | Review one Routine together. Retune or retire. | 30 min |
| **Quarterly** | Update OKR pulse agent's KR list. Review security approvals. Prune prompts. | 1 hour |

## Slower variant: 8-week rollout

If your org is more change-averse (regulated industry, distributed team, or PMs are already over-capacity), stretch this over 8 weeks:

| Week | Focus |
|---|---|
| 1-2 | You run it yourself. Build credibility with your own before/after. |
| 3-4 | Two volunteer PMs try it. Not mandatory. You coach them. |
| 5-6 | Expand to full team with week 1-2 of the fast plan. |
| 7-8 | Run the "week 3 Managed Agents" milestone. Skip the formal week-4 review — do it at the start of week 9. |

Slower is fine. The compounding still kicks in; you just start later.

## Handling pushback

Common objections and responses:

| Pushback | What's actually going on | Response |
|---|---|---|
| *"I don't have time for another tool."* | Valid. They mean "don't make me learn something I won't use." | Start with the 10-min QUICKSTART. If they don't find value in week 1, they opt out, no judgment. |
| *"Isn't this what Zapier does?"* | Genuine confusion — worth addressing. | Show them the user-sentiment Routine. Zapier can't scan Reddit and summarize themes. That's the concrete differentiator. |
| *"We should just use ChatGPT for this."* | Org loyalty or existing subscription. | Fine — but Routines run on schedule without you, and serve team-scale via Managed Agents. ChatGPT is on-demand only. Different tool for different jobs. |
| *"Security will never approve it."* | Sometimes right, sometimes a stall. | Send [SECURITY.md](./SECURITY.md) + [prompt-injection-mitigation.md](./prompt-injection-mitigation.md). Get pattern-level approval in week 0, not per-PM. |
| *"What if the AI hallucinates?"* | Real concern, usually surfaces on the ticket-pattern use case. | Point at the sample outputs. The 3+ mention threshold filters most hallucinations. Week-4 review catches the rest. |

If you get a pushback not on this list — add it. The doc gets more useful as it absorbs real objections.

## Common rollout failures (and how to avoid them)

| Failure | Why it happens | Fix |
|---|---|---|
| Only 2 of 5 PMs actually set it up | Optional = dropped | Make it mandatory in week 1, not optional |
| PMs turn it on, never read the output | Wrong destination or format | Route to shared channels, not DMs, so others nudge |
| Noise fatigue kills adoption | Week 1 wasn't tuned | Mandatory week-2 tuning session on the calendar |
| Security pushback mid-rollout | Approval sought per-PM | Get pattern approval in week 0 |
| Engineer complains about support burden | No handoff brief | Use the handoff brief; set explicit ownership |
| "It's a novelty" after month 2 | No measurement | The week-4 review forces the keep/kill decision |

---

## What to tell your leadership

After 4 weeks, you'll have:
- **Hours saved per week per PM** (baseline vs. week 4)
- **Specific decisions changed** by Routine outputs
- **Standard team Routines** that survived the keep/kill review
- **One shared Managed Agent** your team now depends on
- **A tuned repo fork** specific to your company

That's a concrete before/after that fits in a slide.
