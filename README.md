# mm-mcp-mail (privat)

Plugin **mm-mcp-mail** mit Konnektor und Skill, beide unter demselben Namen. Nur für freigeschaltete
Personen; Zugriff auf dieses Repo gibt es auf Einladung. Gebaut aus dem Repo `mcp-mail`
(`scripts/plugin-release.sh`), hier nichts von Hand ändern.

## claude.ai und Claude Desktop

1. Einstellungen → Customize → Plugins → Add → Add marketplace, `marcomarkl/mm-mcp-mail-plugin` eintragen. Beim ersten
   Mal das GitHub-Konto verbinden und der Claude-GitHub-App Zugriff auf dieses Repo geben.
2. Beim Marketplace „Sync automatically“ einschalten, dann hält sich das Plugin selbst aktuell.
3. Plugin „mm-mcp-mail“ installieren, im Reiter „Connectors“ des Plugins mm-mcp-mail verbinden und
   mit Mailadresse und Code anmelden.
4. Einen früher von Hand angelegten Konnektor und einen einzeln hochgeladenen Skill danach
   entfernen, sonst gibt es beides doppelt.

## Claude Code

```bash
gh auth login && gh auth setup-git
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
