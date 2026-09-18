# HarDoc

![Комикс-баннер HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc проверяет harness Claude Code и Codex в режиме только чтения. Он находит повторяющиеся или конфликтующие инструкции, из-за которых помощник выбирает неправильный skill.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Установка для Claude Code

Один раз выполните две команды:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Использование в Claude Code

Откройте новый сеанс Claude Code и выполните:

```text
/skill-governor audit .
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

HarDoc работает только на чтение. Он не удаляет, не отключает, не устанавливает и не изменяет настройки harness, а также не исправляет результаты doctor автоматически. Проверьте предложения перед изменением.

Полное руководство и процедуру оценки смотрите в [English README](README.md).
