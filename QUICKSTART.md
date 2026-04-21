# 10-Minute First Win

**No Notion. No engineer. No OAuth beyond Slack. If you have a paid Claude plan, you can run this right now.**

---

## The goal

By the end of 10 minutes, you'll have a Routine that posts a daily "what shipped in AI yesterday" digest to your Slack DM. You'll use it to understand how Routines work end-to-end, before wiring anything complex.

## Setup

**Step 1 (2 min).** Connect Slack at [claude.ai](https://claude.ai) → Customize → Connectors → `+` → Slack. Grant access.

**Step 2 (1 min).** Get your personal DM channel ID:
1. In Slack, click your own name in the sidebar
2. Click your name at the top of the DM
3. Scroll to the bottom of the popup — the ID starts with `D`

**Step 3 (2 min).** Go to [claude.ai/code/routines](https://claude.ai/code/routines) → **New Routine**.

- Name: `AI News Daily`
- Trigger: Schedule → daily at 8:00 AM
- Connectors: **keep only Slack**, remove everything else
- Model: Sonnet 4.6

**Step 4 (3 min).** Paste this prompt (replace `D06MYSLACKDM` with your DM ID):

```
Every morning, browse the following sources for AI news
published in the last 24 hours:

- The Anthropic blog (anthropic.com/news)
- The OpenAI blog (openai.com/blog)
- The Google DeepMind blog (deepmind.google/discover/blog)
- The Hacker News front page, filtered for AI posts
- X.com (Twitter) posts from @sama, @karpathy, @AnthropicAI

Summarize in this format:

**AI Daily — [Date]**

**What shipped**
- [Company]: [what they shipped]. Why it matters: [one line]
(3-5 items)

**What people are talking about**
- [Topic]: [one-line summary]
(2-3 items)

**Worth reading today**
- [Link title] — [source]
(1-2 items)

Post to my Slack DM at channel D06MYSLACKDM.

If there's nothing meaningful (i.e. no new launches or major
posts), post: "Quiet news day. Nothing worth your time."

Do not write anything back to me. Execute these steps immediately.
```

**Step 5 (2 min).** Click **Run Now** (top-right corner of the Routine detail page, next to the Active/Paused toggle). Watch your Slack DM.

When the message appears — you now understand the core loop. Prompt → connectors → schedule → output.

## What you just learned

1. **Prompts are procedures, not questions.** Notice you wrote "Every morning, browse..." not "Can you check the news?"
2. **The "Execute these steps immediately" line is load-bearing.** Without it, the Routine narrates instead of running.
3. **The output format is explicit.** Claude didn't invent the structure. You did.
4. **Run Now before scheduling.** You verified it before letting the schedule loop.

## Next

Now that you understand the loop, pick a real use case from the repo:

- **Saves you 20 min/day reading threads before meetings** → `routines/02-morning-meeting-brief.md`
- **Surfaces competitor moves before sales does** → `routines/01-competitor-pricing.md`
- **Tells you what Reddit actually thinks about your category** → `routines/03-weekly-user-sentiment.md`

Each one is 15-30 minutes of real setup. You know enough now to do it.
