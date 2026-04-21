# Week 4 Review — What Changed

**Fill this out after four full weeks of running. Compare against your week-1 baseline.**

---

## Did you actually read the output?

For each Routine / Agent you turned on:

| Name | Ran | Read | Acted on |
|---|---|---|---|
| ___ | ___/28 | ___/28 | ___/28 |

**"Read" = you actually looked at it. "Acted on" = it changed a decision you made.**

If "Read" is under 50% of "Ran" → the destination or format is wrong. Tune it.
If "Acted on" is under 20% of "Read" → the prompt is producing noise. Either the signal threshold is too low (3 mentions is too lax) or the categories are too broad.

## Time saved (vs. week 1 baseline)

| Activity | Week 1 (mins/wk) | Week 4 (mins/wk) | Delta |
|---|---|---|---|
| Competitor pricing checks | ___ | ___ | ___ |
| Prep before meetings | ___ | ___ | ___ |
| Scanning Reddit/G2/Product Hunt | ___ | ___ | ___ |
| Support ticket pattern hunting | ___ | ___ | ___ |
| Meeting notes / action items | ___ | ___ | ___ |
| OKR status roll-ups | ___ | ___ | ___ |
| **Total** | **___** | **___** | **___** |

## Decisions actually changed

List specific decisions you made differently in weeks 1-4 because of a Routine / Agent output:

1. **Decision:** ___
   **Output that changed it:** ___
   **What the decision would've been without it:** ___

2. ___

3. ___

If this list is empty after 4 weeks — the agent is a novelty, not a tool. Either retune or turn it off.

## "Caught early" wins

Things you found out earlier than you otherwise would have:

- ___
- ___
- ___

For each: how many days earlier than business-as-usual?

## False positives / noise

What did the Routine alert you to that turned out to not matter?

- ___
- ___
- ___

Pattern these. If 80% of false positives share a shape ("minor copy changes on competitor pricing pages"), tighten the prompt to filter them out.

## What broke

- Connector auth that expired: ___
- URLs that consistently failed to load: ___
- Silent failures you caught only by checking the run log: ___
- Times the output format drifted: ___

## What you're going to do in weeks 5-8

Check one:

- [ ] **Keep it running as-is.** Working well. Move on to turning on a second one.
- [ ] **Tune the prompt.** Specific changes: ___
- [ ] **Turn it off.** Reason: ___
- [ ] **Escalate to a Managed Agent.** Team needs it, not just me.

## What you'd tell another PM considering this

Three sentences. Be honest. If it's not worth it, say so.

___

___

___

---

## Template: sharing findings with your team or leadership

Use this if you need to write up the 4-week result for a skip-level, a team update, or a quarterly review. Copy, fill in, cut as needed.

```
Subject: 4-week review — Claude Routines + Agents pilot

Tl;dr — [kept / expanded / killed] after 4 weeks. Net [hours saved/week]
across [N] PMs.

What we ran
- [Routine/Agent name] — [frequency]
- [Routine/Agent name] — [frequency]

What changed in decisions (not in time saved — in decisions)
1. [specific decision changed + agent output that changed it]
2. [another]
3. [another]

What broke
- [connector/permissions/format issue] — [what we did about it]

What surprised us
- [the orphaned initiative / the ticket pattern nobody saw / the
   competitor move sales already missed]

What we're doing next
- Keep: [list]
- Tune: [list + specific prompt changes]
- Kill: [list + reason]
- Expand: [next PMs or next use cases]

Cost: $[X]/week. Under our $[budget] threshold, so no finance
conversation needed. / Over threshold — see attached cost doc.

Security posture: reviewed with [name] on [date]. Pattern-level
approval covers: [list agents]. Out of scope: [list].
```

---

*If you learned something surprising, send it to the newsletter. This is the kind of thing that helps the next person avoid a wasted month.*
