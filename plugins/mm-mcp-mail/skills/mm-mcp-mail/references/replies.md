# Replies and drafts

## Where the text goes

The user works in their mail app, so drafts belong in the mailbox, not only in the chat:
- reply to a mail: `reply` with `draft: true` (keeps quote and threading),
- forward: `forward` with `draft: true`,
- new mail: `create_draft`,
- change an existing draft: `update_draft`, then use the returned id.

Several replies: one draft per mail, each saved on its own, then one short report listing recipient and subject per draft. Never send a batch. Only when the user explicitly asks for text in the chat (to copy it elsewhere) skip the drafts.

Do not add a signature: the server appends the mailbox signature (`signature` in `list_accounts`): `text` to every mail, `formatted` additionally to the HTML part of mails with `markdown: true`. Do not repeat a closing line or name the applicable signature already contains; if the applicable one is null (plain mail with `text` null, or `signature` null), nothing is appended, so end with the closing and name the preferences ask for. Do not paste the original mail: `reply` quotes it. Use `markdown: true` only when the text needs formatting.

## Content

- Answer what was asked, first sentence first. One question, one answer; length like the thread.
- Invent nothing: no prices, dates, availability or commitments that are not in the mailbox or the conversation. Use a visible placeholder like [Preis] or say that the user needs to fill it in, and mention that in your report.
- Decide nothing for the user: unless the user said what to answer, do not confirm, accept, decline or promise. Write a draft that can be sent as is and commits to nothing ("vielen Dank, ich prüfe die Lieferung und melde mich bis …" only if a date is known, otherwise "… und melde mich"). Use a placeholder like [bestätigen oder ablehnen] only where the answer itself is the decision, at most one or two per draft, and list these open decisions in your report.
- Language and form of address follow the original mail unless the preferences say otherwise: German stays German, du stays du, Sie stays Sie. A colleague writing "Hallo Lena" with du gets du.

## Style

1. Preferences (`list_accounts`) win.
2. Otherwise look at 3 to 5 mails the user sent to the same person or domain (`search_messages` in the sent folder with `to`). Take greeting, length, closing and tone from them, not their content.
3. Without either: plain and friendly, and say that no style sample was found.

If the user corrects a draft ("kürzer", "immer mit Beste Grüße"), offer to save that in the preferences and do it only after a yes (`update_preferences`).

## German letter conventions

- Greeting with comma, then lower case: "Sehr geehrte Frau Kern," / "Hallo Tom," then a blank line, then "vielen Dank für …".
- Closing without comma, on its own line, name below: "Beste Grüße" / "Lena Hofer", unless the signature already contains them.
- Formal: "Sehr geehrte Frau …" / "Sehr geehrter Herr …"; unknown recipient: "Sehr geehrte Damen und Herren,".
- Du-form greetings: "Hallo …," or "Hi …,"; closing "Liebe Grüße" or "LG" only if the user writes that way.
