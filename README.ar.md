# HarDoc

![شعار HarDoc المصور](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc أداة فحص للقراءة فقط لبيئة Claude Code وCodex. تكتشف الأدوات والتعليمات المتكررة أو المتعارضة التي تجعل المساعد يختار المهارة الخطأ.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## التثبيت في Claude Code

شغّل الأمرين التاليين مرة واحدة:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## تثبيت Codex محليًا

لتثبيت المهارة مباشرةً في Codex، انسخ المستودع وأنشئ رابطًا في مجلد المهارات المحلي:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## التشغيل في Claude Code

افتح جلسة Claude Code جديدة ثم شغّل:

```text
/skill-governor audit .
```

## التشغيل في Codex

إذا كانت المهارة ظاهرة في Codex، افتح جلسة جديدة ثم شغّل:

```text
$skill-governor audit .
```

## ما الذي يفحصه HarDoc

يفحص HarDoc مجلد المشروع أولاً، ثم يتحقق من إصدار CLI ويحاول تشغيل doctor الأصلي لكل بيئة.

- `claude doctor`: يفحص صحة تثبيت Claude Code.
- `codex doctor`: يفحص صحة تثبيت Codex.
- `audit`: يسجل المهارات وMCP والإضافات والقواعد والخطافات والوكلاء والأدلة الفعلية.

## حدود الأمان

HarDoc للقراءة فقط. لا يحذف أو يعطّل أو يثبت أو يعدّل إعدادات البيئة ولا يصلح نتائج doctor تلقائياً. راجع الاقتراحات قبل أي تغيير.

للتفاصيل الكاملة وشرح التقييم، راجع [README الإنجليزي](README.md).
