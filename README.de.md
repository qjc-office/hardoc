# HarDoc

![HarDoc Comic-Banner](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc prüft deine Claude-Code- und Codex-Harness. Es berichtet zuerst und ändert Einstellungen erst, nachdem du zugestimmt hast.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Für Claude Code installieren

Führen Sie diese beiden Befehle einmal aus:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Lokal in Codex installieren

Um das Skill direkt in Codex zu installieren, klonen Sie das Repository und verknüpfen Sie es mit Ihrem lokalen Skills-Ordner:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## In Claude Code verwenden

Öffnen Sie eine neue Claude-Code-Sitzung und führen Sie aus:

```text
/skill-governor audit .
```

Um auf den Bericht zu reagieren, sieh dir eine Vorschau der Bereinigung an:

```text
/trim --dry-run
```

## Mit Codex verwenden

Wenn der Skill in Codex sichtbar ist, öffnen Sie eine neue Sitzung und führen Sie aus:

```text
$skill-governor audit .
```

## Was HarDoc prüft

HarDoc prüft zuerst das Projektverzeichnis, dann die CLI-Version und versucht den nativen Doctor des jeweiligen Laufzeitsystems.

- `claude doctor`: Prüft den Zustand der Claude-Code-Installation.
- `codex doctor`: Prüft den Zustand der Codex-Installation.
- `audit`: Prüft Skills, MCP, Plugins, Regeln, Hooks, Agents und Belege für die tatsächliche Nutzung.

## Sicherheitsgrenzen

HarDoc ändert nichts ohne deine Zustimmung. `skill-governor` ist schreibgeschützt. `trim` wendet eine Änderung erst an, nachdem du eine Vorschau bestätigt hast, legt vorher einen Snapshot an und gibt einen einzelnen Befehl zum Zurücksetzen aus.

Die vollständige Anleitung und Bewertung finden Sie im [English README](README.md).
