# Mailzugang (privat)

Plugin mit dem Konnektor **Mailzugang** und dem Skill **mail-workflows**. Nur für freigeschaltete
Personen; Zugriff auf dieses Repo gibt es auf Einladung. Gebaut aus dem Repo `mcp-mail`
(`scripts/plugin-release.sh`), hier nichts von Hand ändern.

## claude.ai und Claude Desktop

1. Einstellungen → Customize → Plugins → Add → Add marketplace, `marcomarkl/mailzugang-plugin` eintragen. Beim ersten
   Mal das GitHub-Konto verbinden und der Claude-GitHub-App Zugriff auf dieses Repo geben.
2. Beim Marketplace „Sync automatically“ einschalten, dann hält sich das Plugin selbst aktuell.
3. Plugin „mailzugang“ installieren, im Reiter „Connectors“ des Plugins Mailzugang verbinden und
   mit Mailadresse und Code anmelden.
4. Einen früher von Hand angelegten Konnektor „Mailzugang“ und einen hochgeladenen Skill
   „mail-workflows“ danach entfernen, sonst gibt es beides doppelt.

## Claude Code

```bash
gh auth login && gh auth setup-git
claude plugin marketplace add marcomarkl/mailzugang-plugin
claude plugin install mailzugang@mailzugang
```

Automatische Updates unter `/plugin` → Marketplaces → mailzugang einschalten (bei eigenen
Marketplaces standardmäßig aus). Den Konnektor unter `/mcp` anmelden.
