# Sample Output: Support Ticket Pattern Report

**This is what posts to the #product-team Slack channel at 6 AM Monday. Company name and roadmap items anonymized.**

---

> 🤖 **Support Pattern Report — Week of Apr 21**
>
> | Theme | Count | On Roadmap? |
> |---|---|---|
> | SSO setup confusion | 23 | Yes (Q2) |
> | Dashboard performance (slow loads) | 18 | No |
> | CSV export missing from dashboard | 14 | No |
> | Mobile redesign feedback — negative | 11 | Unknown |
> | Billing page clarity | 9 | No |
> | API rate limit errors | 7 | Yes (Q3) |
> | Two-factor auth lockout | 4 | No |
>
> **Top 3 themes, in the customer's own words:**
>
> 1. **"Setting up SSO is impossible" (23 tickets)** — Recurring: the Okta group mapping step isn't documented, and the error message when it fails just says "configuration error."
>
> 2. **"The dashboard is slow" (18 tickets)** — Shows up after users add ~50+ workspaces. The phrase "takes forever to load" appears in 12 of the 18.
>
> 3. **"I need to export this as CSV" (14 tickets)** — Specific to the reports view, not the main dashboard. Users are screenshotting data to paste into sheets.
>
> Full ticket list available on request.

---

## What's good about this output

- **Customer language preserved.** Not "UX friction on authentication flow." It's "Setting up SSO is impossible."
- **The on-roadmap column forces a decision.** 18 tickets about dashboard perf with no roadmap item = a real conversation for Monday planning.
- **Top 3 gets a human-readable pattern, not just counts.** The summary tells you *what* in the SSO flow is broken, not just that SSO has tickets.

## What the noisy version looks like (week 1 before tuning)

Your first week's report might look like this:

> - UX issues (47 tickets) — various
> - Login problems (23 tickets) — various
> - Feature requests (19 tickets) — various
> - Bugs (18 tickets) — various

If you see this shape, the prompt is too permissive. Tighten "theme" to mean "complaint or frustration that appears in 3+ separate posts using similar language" — and exclude generic categories like "UX" or "bugs."
