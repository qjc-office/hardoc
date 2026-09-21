# HarDoc

![HarDocs serietidningsbanner](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc granskar din Claude Code- och Codex-harness. Den rapporterar först och ändrar inställningar först efter ditt godkännande.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Installera för Claude Code

Kör dessa två kommandon en gång:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Installera lokalt i Codex

Installera skillen direkt i Codex genom att klona repositoryt och skapa en länk i din lokala skills-mapp:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Använd i Claude Code

Öppna en ny Claude Code-session och kör:

```text
/skill-governor audit .
```

För att agera på rapporten, se en förhandsvisning av rensningen:

```text
/trim --dry-run
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

HarDoc ändrar ingenting utan ditt godkännande. Färdigheten `skill-governor` är skrivskyddad. `trim` tillämpar en ändring först när du godkänt en förhandsvisning, tar först en ögonblicksbild och skriver ut ett enda kommando för att ångra.

Se [English README](README.md) för fullständig guide och utvärdering.
