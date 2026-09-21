# HarDoc

![Комікс-банер HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc перевіряє ваш harness Claude Code і Codex. Спершу він звітує, а налаштування змінює лише після вашого схвалення.

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
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Використання у Claude Code

Відкрийте новий сеанс Claude Code і виконайте:

```text
/skill-governor audit .
```

Щоб діяти за звітом, перегляньте попередній список очищення:

```text
/trim --dry-run
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

HarDoc нічого не змінює без вашого схвалення. Навичка `skill-governor` лише читає. Навичка `trim` застосовує зміну тільки після того, як ви схвалите попередній перегляд, спершу робить знімок і друкує одну команду для повернення.

Повний посібник і оцінювання дивіться в [English README](README.md).
