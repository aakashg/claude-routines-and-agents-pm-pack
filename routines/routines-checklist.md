# Routines Verification Checklist

**Run through this after your first Run Now. Before you schedule anything.**

---

## Did the connectors actually fire?

- [ ] Open the run log. Every tool call shows up there.
- [ ] Confirm you see a call to each connector you expected (Gmail, Slack, Notion, etc.)
- [ ] If a connector is missing from the log but is in your prompt — it's probably an auth scope issue. Reconnect and grant full read access.

## Did the output land where you expected?

- [ ] Slack: the message actually appeared in the channel (not a DM to someone else, not failed silently)
- [ ] Notion: the page was updated, not a new page created each run (check the "last edited" timestamp)
- [ ] Gmail drafts, if any: the draft exists and is addressed correctly

## Is the output actually useful?

- [ ] Does the format match what you specified in the prompt?
- [ ] Are you reading it and getting something you couldn't have guessed? If yes → ship it. If no → the prompt is too generic.
- [ ] Is it the right length? Too long means you won't read it. Too short means it's missing something.

## Did you remove the connectors you don't need?

- [ ] Go back into the Routine. Count the connectors listed.
- [ ] Anything there that isn't in the prompt? Remove it. Claude can use any connected tool without asking during runs — don't give it more access than the task needs.

## Did the prompt end correctly?

- [ ] Last line reads: `Do not write anything back to me. Execute these steps immediately.`
- [ ] If missing, the Routine will narrate what it *would* do instead of doing it.

## If it's writing state to Notion:

- [ ] There's a clear instruction to **read** yesterday's Notion page at the start
- [ ] There's a clear instruction to **overwrite** the Notion page at the end
- [ ] The URL in the prompt is correct (paste it from the Notion share link, not the internal page name)

## Only then — schedule it.

Don't schedule before you've watched it work end-to-end. Silent failures burn your daily limit (Pro: 5 runs. Max: 15. Team/Enterprise: 25.)
