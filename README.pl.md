# HarDoc

![Komiksowy baner HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc sprawdza twój harness Claude Code i Codex. Najpierw raportuje, a ustawienia zmienia dopiero po twojej zgodzie.

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
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Użycie w Claude Code

Otwórz nową sesję Claude Code i uruchom:

```text
/skill-governor audit .
```

Aby zareagować na raport, zobacz podgląd porządkowania:

```text
/trim --dry-run
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

HarDoc nie zmienia niczego bez twojej zgody. Umiejętność `skill-governor` tylko czyta. `trim` wprowadza zmianę dopiero po zatwierdzeniu podglądu, najpierw robi migawkę i wypisuje jedno polecenie cofające.

Pełny przewodnik i procedurę oceny znajdziesz w [English README](README.md).
