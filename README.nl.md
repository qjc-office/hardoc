# HarDoc

![HarDoc-stripbanner](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc controleert je Claude Code- en Codex-harness. Het rapporteert eerst en wijzigt instellingen pas nadat jij akkoord gaat.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Installeren voor Claude Code

Voer deze twee opdrachten één keer uit:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Lokaal installeren in Codex

Installeer de skill rechtstreeks in Codex door de repository te klonen en een koppeling in uw lokale skills-map te maken:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Gebruiken in Claude Code

Open een nieuwe Claude Code-sessie en voer uit:

```text
/skill-governor audit .
```

Om op het rapport te handelen, bekijk je eerst een voorbeeld van de opschoning:

```text
/trim --dry-run
```

## Gebruiken met Codex

Als de skill in Codex beschikbaar is, open dan een nieuwe sessie en voer uit:

```text
$skill-governor audit .
```

## Wat HarDoc controleert

HarDoc controleert eerst de projectmap, controleert daarna de CLI-versie en probeert de native doctor van elke runtime uit te voeren.

- `claude doctor`: Controleert de gezondheid van de Claude Code-installatie.
- `codex doctor`: Controleert de gezondheid van de Codex-installatie.
- `audit`: Controleert skills, MCP, plugins, rules, hooks, agents en bewijs van werkelijk gebruik.

## Veiligheidsgrenzen

HarDoc verandert niets zonder jouw akkoord. De skill `skill-governor` is alleen-lezen. `trim` past een wijziging pas toe nadat je een voorbeeld hebt goedgekeurd, maakt eerst een snapshot en toont één commando om het ongedaan te maken.

Bekijk de [English README](README.md) voor de volledige uitleg en evaluatiestappen.
