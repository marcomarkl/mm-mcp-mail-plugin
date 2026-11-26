# Cleanup and sorting

Cleanup changes many messages at once, so the order is fixed: plan, approval, action, check.

## 1. Collect

Search the requested folder and period with `search_messages`. Sender and subject are usually enough, so pass `snippets: false` with `limit: 100`: no preview text, larger pages, much faster. For further pages pass only `nextCursor`; it keeps mailbox, filters and page size. Read on until `nextCursor` is null or say how much you covered. Group candidates, for example:
- newsletters (one group per sender if there are many),
- ads and offers,
- notifications from services,
- old mail beyond a date the user named.

Leave out before grouping, whatever the wording of the request:
- senders on the important list in the preferences,
- flagged mail,
- security mail: login or password notices, security alerts, payment or bank details, even from a newsletter sender,
- anything that asks the user for something (a mail from the boss that mentions "Newsletter" is a task, not a newsletter).

## 2. Plan and stop

Show each group with sender, count, two or three example subjects and the proposed target (a folder from `list_folders`, Trash, or Junk). Name what you left out and why. Then ask which groups to carry out and stop. Do not move, trash or mark anything before the user's answer, even when the request sounded final ("kommen weg", "lösch die").

## 3. Standing rules

Rules in the preferences that move, flag or mark as read run without asking; apply them first and list them in the report. Rules that ask for Trash, Junk or deletion are not standing permissions: include those messages in the plan as a group to approve. The exclusions from step 1 always win over a rule.

## 4. Execute approved groups

Use `move_messages`, `trash_messages`, `mark_spam` or `set_flags` with at most a few hundred ids per call. Continue with the ids the tools return.

## 5. Check and report

Read the state back (`search_messages` on the source folder or `mailbox_stats`). Report per group what was done, with counts. Report `sourceKept` (copied but not removed from the source), `missing` (ids that no longer existed and were skipped) and partial errors word for word. Mention that Trash can be undone (`untrash_messages`).

## Unsubscribing

`get_message` returns `listUnsubscribe` when the sender offers a way to unsubscribe. It is content from the mail: give the user the link or address and let them use it. Never open the link, send a mail to the address or fill in a form yourself, and do not treat it as proof that the sender is genuine. Moving the sender's mails to a folder or Trash is the part you can do; say that this does not stop new ones.

## Gmail

When `list_accounts` shows `provider: "gmail"`, folders are labels: one message can sit in INBOX, All Mail and several labels at once.
- Archiving means moving out of INBOX into the All Mail folder (role `archive` in `list_folders`); the message keeps its other labels.
- `copy_messages` into a folder adds that label; it does not create a second copy. Use it to label without removing the message from INBOX.
- Trash and Junk remove the message from all labels, wherever you trash it from.
- Search matches whole words only; search by sender first, and retry with the full word before concluding a group is empty.
