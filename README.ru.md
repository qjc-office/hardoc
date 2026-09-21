# HarDoc

![Комикс-баннер HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc проверяет ваш harness Claude Code и Codex. Сначала он сообщает о находках и меняет настройки только после вашего одобрения.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Установка для Claude Code

Один раз выполните две команды:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Локальная установка в Codex

Чтобы установить skill напрямую в Codex, клонируйте репозиторий и создайте ссылку в локальной папке skills:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Использование в Claude Code

Откройте новый сеанс Claude Code и выполните:

```text
/skill-governor audit .
```

Чтобы действовать по отчёту, посмотрите предварительный список очистки:

```text
/trim --dry-run
```

## Использование с Codex

Если skill доступен в Codex, откройте новый сеанс и выполните:

```text
$skill-governor audit .
```

## Что проверяет HarDoc

HarDoc сначала проверяет каталог проекта, затем версию CLI и пытается запустить native doctor каждого runtime.

- `claude doctor`: Проверяет состояние установки Claude Code.
- `codex doctor`: Проверяет состояние установки Codex.
- `audit`: Проверяет skills, MCP, plugins, rules, hooks, agents и доказательства реального использования.

## Границы безопасности

HarDoc ничего не меняет без вашего согласия. Навык `skill-governor` работает только на чтение. Навык `trim` применяет изменение лишь после того, как вы одобрите предпросмотр, сначала делает снимок и печатает одну команду для отката.

Полное руководство и процедуру оценки смотрите в [English README](README.md).
