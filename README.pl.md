# HarDoc

![Komiksowy baner HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc sprawdza w trybie tylko do odczytu harness Claude Code i Codex. Wykrywa powielone lub sprzeczne instrukcje, przez które asystent może wybrać niewłaściwy skill.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Instalacja dla Claude Code

Uruchom te dwie komendy tylko raz:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Instalacja lokalna w Codex

Aby zainstalować skill bezpośrednio w Codex, sklonuj repozytorium i utwórz dowiązanie w lokalnym katalogu skills:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## Użycie w Claude Code

Otwórz nową sesję Claude Code i uruchom:

```text
/skill-governor audit .
```

## Użycie z Codex

Jeśli skill jest widoczny w Codex, otwórz nową sesję i uruchom:

```text
$skill-governor audit .
```

## Co sprawdza HarDoc

HarDoc najpierw sprawdza katalog projektu, potem wersję CLI i próbuje uruchomić natywny doctor każdego runtime.

- `claude doctor`: Sprawdza stan instalacji Claude Code.
- `codex doctor`: Sprawdza stan instalacji Codex.
- `audit`: Sprawdza skills, MCP, plugins, rules, hooks, agents oraz dowody rzeczywistego użycia.

## Granice bezpieczeństwa

HarDoc działa tylko do odczytu. Nie usuwa, nie wyłącza, nie instaluje ani nie zmienia konfiguracji harness i nie naprawia automatycznie wyników doctor. Przejrzyj propozycje przed zmianą.

Pełny przewodnik i procedurę oceny znajdziesz w [English README](README.md).
