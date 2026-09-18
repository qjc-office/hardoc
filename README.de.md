# HarDoc

![HarDoc Comic-Banner](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc prüft das Harness von Claude Code und Codex nur lesend. Es findet doppelte oder widersprüchliche Anweisungen, durch die der Assistent den falschen Skill auswählt.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Für Claude Code installieren

Führen Sie diese beiden Befehle einmal aus:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## In Claude Code verwenden

Öffnen Sie eine neue Claude-Code-Sitzung und führen Sie aus:

```text
/skill-governor audit .
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

HarDoc arbeitet nur lesend. Es löscht, deaktiviert, installiert oder ändert keine Harness-Konfiguration und repariert Doctor-Ergebnisse nicht automatisch. Prüfen Sie Vorschläge vor jeder Änderung.

Die vollständige Anleitung und Bewertung finden Sie im [English README](README.md).
