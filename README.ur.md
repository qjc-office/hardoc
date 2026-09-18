# HarDoc

![HarDoc کامک بینر](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc، Claude Code اور Codex harness کی read-only جانچ ہے۔ یہ دہرائی گئی یا متضاد ہدایات تلاش کرتا ہے جن سے معاون غلط skill منتخب کر سکتا ہے۔

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
```

## Claude Code میں استعمال

نئی Claude Code نشست کھولیں اور چلائیں:

```text
/skill-governor audit .
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

HarDoc صرف پڑھتا ہے۔ یہ harness configuration کو حذف، غیر فعال، انسٹال یا تبدیل نہیں کرتا اور doctor نتائج خودکار طور پر درست نہیں کرتا۔ تبدیلی سے پہلے تجاویز کا جائزہ لیں۔

مکمل رہنما اور evaluation کے لیے [English README](README.md) دیکھیں۔
