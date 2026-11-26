# Triage and daily overview

## Window

Default: everything received in the last 48 hours, plus unanswered mail from the last 14 days that still asks something of the user. A different window in the user's preferences or request wins. Search INBOX; use `folder: "*"` only when the user asks for everything. For further pages pass only `nextCursor`. On Gmail (`provider: "gmail"` in `list_accounts`) search matches whole words only: a word fragment finds nothing, so retry with the full word.

## Reading budget

Sort by sender, subject and snippet from `search_messages` first. Open full texts (`get_message`, `get_thread` for history) only for mails that may need the user, and for anything that looks like fraud. If `bodyTruncated` is true and the rest matters, read on with `get_message` and `offset` (the result names `bodyOffset` and `bodyTotalChars`). About 20 full texts per run is the limit; beyond that give counts per group and offer to read on. Do not claim the inbox is done if pages or folders were not read.

## Groups

1. **Braucht Sie**: someone expects an answer, decision or action. Order by the consequence of missing it (lost order, surcharge, a deadline today), not by arrival time. Put security alerts (new login, password changed) at the very top with a one-line hint what to check. For each item give who, what is expected, and the deadline or amount if the mail states one.
2. **Zur Kenntnis**: useful information without action (deliveries, confirmations, invoices to pay later with amount and due date).
3. **Kann warten oder weg**: newsletters, ads, notifications, summarised as counts per sender type, not one by one.

Senders on the important list always land in group 1 or 2, never in 3.

## Fraud signals

Mark separately and say why, when a mail:
- asks to pay to new or changed bank details,
- asks for codes, passwords or logins,
- comes from a sender domain that differs from earlier mails of the same company (compare with `get_thread` or a search for the company name),
- creates time pressure around money.

Advise to verify through a known contact before acting. Never reply to such a mail on your own.

## After the overview

Offer the obvious next steps (draft replies, cleanup of group 3) as a question. Do not act on them before the user answers.
