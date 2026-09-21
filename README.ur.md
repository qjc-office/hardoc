# HarDoc

![HarDoc کامک بینر](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc آپ کے Claude Code اور Codex ہارنس کی جانچ کرتا ہے۔ یہ پہلے رپورٹ دیتا ہے اور ترتیبات صرف آپ کی منظوری کے بعد بدلتا ہے۔

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Claude Code کے لیے انسٹال کریں

یہ دونوں کمانڈز ایک بار چلائیں:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Codex میں مقامی انسٹالیشن

Skill کو Codex میں براہِ راست انسٹال کرنے کے لیے repository کلون کریں اور اپنے مقامی skills فولڈر میں لنک بنائیں:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Claude Code میں استعمال

نئی Claude Code نشست کھولیں اور چلائیں:

```text
/skill-governor audit .
```

رپورٹ پر عمل کرنے کے لیے صفائی کا پیش منظر دیکھیں:

```text
/trim --dry-run
```

## Codex کے ساتھ استعمال

اگر skill Codex میں نظر آتی ہے تو نئی نشست کھول کر چلائیں:

```text
$skill-governor audit .
```

## HarDoc کیا جانچتا ہے

HarDoc پہلے project directory، پھر CLI version جانچتا ہے اور ہر runtime کا native doctor چلانے کی کوشش کرتا ہے۔

- `claude doctor`: Claude Code installation کی صحت جانچتا ہے۔
- `codex doctor`: Codex installation کی صحت جانچتا ہے۔
- `audit`: skills، MCP، plugins، rules، hooks، agents اور حقیقی استعمال کے ثبوت جانچتا ہے۔

## حفاظتی حدود

آپ کی منظوری کے بغیر HarDoc کچھ نہیں بدلتا۔ `skill-governor` مہارت صرف پڑھتی ہے۔ `trim` مہارت تبدیلی تبھی لاگو کرتی ہے جب آپ پیش منظر منظور کریں؛ وہ پہلے سنیپ شاٹ لیتی ہے اور واپس جانے کے لیے ایک کمانڈ دکھاتی ہے۔

مکمل رہنما اور evaluation کے لیے [English README](README.md) دیکھیں۔
