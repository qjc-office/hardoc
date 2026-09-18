# HarDoc

![بنر کمیک HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc یک بررسی فقط‌خواندنی برای هارنس Claude Code و Codex است. دستورهای تکراری یا متناقضی را پیدا می‌کند که باعث انتخاب skill اشتباه می‌شوند.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## نصب برای Claude Code

این دو دستور را فقط یک بار اجرا کنید:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## نصب محلی در Codex

برای نصب مستقیم skill در Codex، مخزن را کلون کنید و در پوشه محلی skills یک پیوند بسازید:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## استفاده در Claude Code

یک نشست جدید Claude Code باز کنید و اجرا کنید:

```text
/skill-governor audit .
```

## استفاده با Codex

اگر skill در Codex نمایش داده می‌شود، یک نشست جدید باز کنید و اجرا کنید:

```text
$skill-governor audit .
```

## HarDoc چه چیزهایی را بررسی می‌کند

HarDoc ابتدا پوشه پروژه را بررسی می‌کند، سپس نسخه CLI را می‌خواند و native doctor هر runtime را امتحان می‌کند.

- `claude doctor`: سلامت نصب Claude Code را بررسی می‌کند.
- `codex doctor`: سلامت نصب Codex را بررسی می‌کند.
- `audit`: skills، MCP، plugins، rules، hooks، agents و شواهد استفاده واقعی را بررسی می‌کند.

## مرزهای امنیتی

HarDoc فقط‌خواندنی است. تنظیمات هارنس را حذف، غیرفعال، نصب یا ویرایش نمی‌کند و نتیجه doctor را خودکار اصلاح نمی‌کند. پیش از تغییر، پیشنهادها را بررسی کنید.

برای راهنمای کامل و ارزیابی، [README انگلیسی](README.md) را ببینید.
