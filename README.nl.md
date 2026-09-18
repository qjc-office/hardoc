# HarDoc

![HarDoc-stripbanner](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc is een controle voor Claude Code- en Codex-harnassen die alleen leest. Het vindt dubbele of tegenstrijdige instructies waardoor de assistent de verkeerde skill kiest.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Installeren voor Claude Code

Voer deze twee opdrachten één keer uit:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Gebruiken in Claude Code

Open een nieuwe Claude Code-sessie en voer uit:

```text
/skill-governor audit .
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

HarDoc werkt alleen-lezen. Het verwijdert, schakelt uit, installeert of wijzigt geen harness-configuratie en repareert doctor-resultaten niet automatisch. Beoordeel voorstellen eerst.

Bekijk de [English README](README.md) voor de volledige uitleg en evaluatiestappen.
