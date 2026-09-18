# HarDoc

![HarDocs serietidningsbanner](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc granskar Claude Code- och Codex-harnessen i skrivskyddat läge. Det hittar dubbla eller motstridiga instruktioner som kan få assistenten att välja fel skill.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Installera för Claude Code

Kör dessa två kommandon en gång:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Använd i Claude Code

Öppna en ny Claude Code-session och kör:

```text
/skill-governor audit .
```

## Använd med Codex

Om skillen visas i Codex öppnar du en ny session och kör:

```text
$skill-governor audit .
```

## Det här kontrollerar HarDoc

HarDoc kontrollerar först projektmappen, sedan CLI-versionen och försöker köra den inbyggda doctorn för varje runtime.

- `claude doctor`: Kontrollerar hälsan för Claude Code-installationen.
- `codex doctor`: Kontrollerar hälsan för Codex-installationen.
- `audit`: Kontrollerar skills, MCP, plugins, rules, hooks, agents och bevis på faktisk användning.

## Säkerhetsgränser

HarDoc är skrivskyddat. Det tar inte bort, inaktiverar, installerar eller ändrar harness-konfiguration och rättar inte doctor-resultat automatiskt. Granska förslag innan du ändrar något.

Se [English README](README.md) för fullständig guide och utvärdering.
