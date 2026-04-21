# Sample Output: Competitor Pricing Monitor

**Two outputs — the "no change" day and the "something moved" day.**

---

## The quiet day (95% of days look like this)

> 🤖 Competitor check complete. No changes. Apr 21, 2026

That's the entire message. Good. You read it in 1 second, you know there's nothing to do.

---

## The day something moved

> 🤖 **Competitor check — Apr 21, 2026**
>
> **Vercel:** Pro plan increased from $20/user/mo to $25/user/mo. Enterprise plan now includes "Priority SLA" as default (previously add-on). No visible end-date on promotional pricing.
>
> **Netlify:** No changes.
>
> **Render:** Added a new "Team Plus" tier at $40/user/mo between Team ($20) and Organization (Custom). Positioned as "mid-market" with dedicated support.

And in Notion, the full "Competitor Pricing Log" page is now overwritten with today's table:

```
Last checked: Tuesday, April 21, 2026 — 09:14 UTC
---
## Vercel
| Plan Name  | Price        | Key Features                                              |
|------------|--------------|-----------------------------------------------------------|
| Hobby      | Free         | 100GB bandwidth, 6000 build minutes/mo, Serverless Functions, Preview URLs |
| Pro        | $25/user/mo  | 1TB bandwidth, 24000 build minutes, Team collaboration, Web Analytics      |
| Enterprise | Custom       | SSO/SAML, SLA, Advanced security, Custom contracts, Priority support       |
Promotions: None currently visible.
---
## Netlify
| Plan Name  | Price       | Key Features                                              |
|------------|-------------|-----------------------------------------------------------|
| Starter    | Free        | 100GB bandwidth, 300 build minutes/mo, 1 member            |
| Pro        | $19/user/mo | 1TB bandwidth, 25000 build minutes, Password protection    |
| Enterprise | Custom      | SAML SSO, Custom SLA, Advanced roles, Priority support     |
Promotions: None currently visible.
---
## Render
| Plan Name    | Price       | Key Features                                        |
|--------------|-------------|-----------------------------------------------------|
| Free         | $0          | Static sites, limited compute, spins down on inactivity |
| Individual   | $7/mo       | Always-on services, 512MB RAM, shared CPU              |
| Team         | $20/user/mo | Team collaboration, private services, more compute     |
| Team Plus    | $40/user/mo | Dedicated support, mid-market features                 |
| Organization | Custom      | SSO, audit logs, dedicated support                     |
Promotions: None currently visible.
```

## Why this format works

- **The Slack message is short enough to read on your phone** while walking to standup. Under 150 words.
- **The Notion page has everything**. When your sales team asks "wait what are the Render prices right now?" you forward the Notion link.
- **The "No changes" message is deliberately boring.** If it weren't, you'd stop reading it — and then miss the one day it actually changed.
