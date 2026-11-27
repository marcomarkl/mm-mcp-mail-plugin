# mm-mcp-mail

Plugin **mm-mcp-mail** mit Konnektor und Skill, beide unter demselben Namen. Das Repo ist öffentlich,
den Konnektor nutzen können aber nur freigeschaltete Personen (Anmeldung mit Mailadresse und Code).
Gebaut aus dem Repo `mcp-mail` (`scripts/plugin-release.sh`), hier nichts von Hand ändern.

## Was der Konnektor kann

Claude arbeitet nur mit den Postfächern, die Sie selbst auf der Kontoseite verbunden haben.

**Lesen**

- Postfächer mit Bezeichnung, Adresse, Absendername, Senderegel, verbleibenden Sendungen dieser
  Stunde, Grenze für Anhänge, Signatur und Ihren gespeicherten Vorgaben (nicht: Zusatzadressen,
  bekannte Empfänger, Server und Benutzername)
- Ordner mit Anzahl und ungelesenen Mails, Speicherbelegung
- Suche nach Absender, Empfänger, Betreff, Text, Datum und Markierungen. Je Treffer gibt es eine
  Vorschau der ersten 160 Zeichen, bis 50 Treffer je Seite (ohne Vorschau 100). Der Volltext
  reicht ohne Datum 365 Tage zurück.
- ganze Mails als Text, bis 50.000 Zeichen je Abruf und weiterlesbar. Externe Inhalte werden nie
  geladen, Mails bleiben ungelesen. Auf Wunsch gibt es Kopfzeilen wie Received und
  Authentication-Results.
- Unterhaltungen bis 30 Mails
- Anhänge bis 8 MB: Bilder, Textdateien und PDF mit Inhalt, andere Formate nur mit Name, Typ
  und Größe
- Kalendereinladungen und Entwürfe

**Ordnen**

- Ordner anlegen, umbenennen, leere Ordner löschen
- verschieben, kopieren, markieren, als Spam einstufen, in den Papierkorb und zurück
- endgültig löschen nur aus dem Papierkorb

**Schreiben und senden**

- Entwürfe anlegen, ändern und löschen. Antworten und Weiterleitungen als Entwurf behalten Zitat
  und Verlauf.
- senden, antworten, weiterleiten, Einladungen beantworten. Das gilt immer nach der Senderegel
  des Postfachs: nur Entwürfe, nur an bekannte Empfänger oder direkt, dazu ein Sendelimit je
  Stunde. Dieselbe Mail geht nicht zweimal kurz nacheinander hinaus, und nach einem unklaren
  Versand sendet Claude nicht erneut.
- Die Signatur hängt der Server an: die Textfassung an jede Mail, die HTML-Fassung an
  formatierte Mails. Kalenderantworten tragen keine Signatur.
- Auf Ihre Bitte oder nach Ihren Vorgaben lässt Claude die Signatur bei einzelnen Mails weg und
  sagt das vor dem Senden.
- Anhänge mitschicken, zusammen bis 10 MB, bei kleinerer Grenze des Mailanbieters entsprechend
  weniger

**Sonst**

- Ihre Vorgaben speichern (Stil, wichtige Absender, Ordner, stehende Regeln zum Verschieben und
  Markieren), nur auf Ihre Bitte. Vorgaben erlauben nie das Senden.
- Probleme mit dem Konnektor an den Betreiber melden, ohne Mailinhalte, Namen oder Adressen

**Nicht möglich**

- Postfach-Passwörter: Sie liegen verschlüsselt auf dem Server und gehen nie an Claude.
- Postfächer anderer Personen.
- Senderegel, Sendelimit, bekannte Empfänger, Signatur und Zugangsdaten ändern: Das geht nur auf
  der Kontoseite.
- Regeln, die im Hintergrund laufen, wenn Sie nicht mit Claude arbeiten.

Was Claude abruft, steht danach in Ihrer Unterhaltung mit Claude.

## claude.ai und Claude Desktop

1. Einstellungen → Customize → Plugins → Add → Add marketplace, `marcomarkl/mm-mcp-mail-plugin` eintragen.
2. Beim Marketplace „Sync automatically“ einschalten, dann hält sich das Plugin selbst aktuell.
3. Plugin „mm-mcp-mail“ installieren, im Reiter „Connectors“ des Plugins mm-mcp-mail verbinden und
   mit Mailadresse und Code anmelden.
4. Einen früher von Hand angelegten Konnektor und einen einzeln hochgeladenen Skill danach
   entfernen, sonst gibt es beides doppelt.

## Claude Code

```bash
claude plugin marketplace add marcomarkl/mm-mcp-mail-plugin
claude plugin install mm-mcp-mail@mm-mcp-mail
```

Automatische Updates unter `/plugin` → Marketplaces → mm-mcp-mail einschalten (bei eigenen
Marketplaces standardmäßig aus). Den Konnektor unter `/mcp` anmelden.

## Umstieg von „mailzugang“ (bis 0.13.1)

Plugin, Marketplace und Skill hießen früher `mailzugang` und `mail-workflows`. Das alte Plugin
aktualisiert sich nicht auf den neuen Namen, deshalb einmal von Hand umsteigen:

1. Altes Plugin `mailzugang` und den Marketplace `mailzugang` entfernen
   (Claude Code: `claude plugin uninstall mailzugang@mailzugang`, dann
   `claude plugin marketplace remove mailzugang`).
2. Marketplace und Plugin wie oben neu einrichten und den Konnektor neu anmelden. Ihre Postfächer
   und Einstellungen bleiben am Server erhalten.
3. Einen einzeln installierten Skill `mail-workflows` löschen (in claude.ai unter Skills, in
   Claude Code den Ordner `~/.claude/skills/mail-workflows`).

Einen von Hand angelegten Konnektor müssen Sie nicht neu anlegen: Die Adresse ist gleich geblieben,
der Name dort ist nur eine Beschriftung.
