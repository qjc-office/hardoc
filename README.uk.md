# HarDoc

![Комікс-банер HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc перевіряє harness Claude Code і Codex у режимі лише читання. Він знаходить дубльовані або суперечливі інструкції, через які помічник обирає неправильний skill.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Встановлення для Claude Code

Виконайте ці дві команди один раз:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Локальне встановлення в Codex

Щоб встановити skill безпосередньо в Codex, клонуйте репозиторій і створіть посилання у локальній папці skills:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## Використання у Claude Code

Відкрийте новий сеанс Claude Code і виконайте:

```text
/skill-governor audit .
```

## Використання з Codex

Якщо skill доступний у Codex, відкрийте новий сеанс і виконайте:

```text
$skill-governor audit .
```

## Що перевіряє HarDoc

HarDoc спочатку перевіряє каталог проєкту, потім версію CLI і намагається запустити native doctor кожного runtime.

- `claude doctor`: Перевіряє стан інсталяції Claude Code.
- `codex doctor`: Перевіряє стан інсталяції Codex.
- `audit`: Перевіряє skills, MCP, plugins, rules, hooks, agents і докази реального використання.

## Межі безпеки

HarDoc працює лише для читання. Він не видаляє, не вимикає, не встановлює і не змінює конфігурацію harness та не виправляє результати doctor автоматично. Перегляньте пропозиції перед змінами.

Повний посібник і оцінювання дивіться в [English README](README.md).
