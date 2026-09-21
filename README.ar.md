# HarDoc

![شعار HarDoc المصور](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

يفحص HarDoc بنية Claude Code و Codex. يعرض تقريرًا أولًا، ولا يغيّر أي إعداد إلا بعد موافقتك.

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
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## التشغيل في Claude Code

افتح جلسة Claude Code جديدة ثم شغّل:

```text
/skill-governor audit .
```

للتصرّف بناءً على التقرير، اعرض معاينة للتنظيف:

```text
/trim --dry-run
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

لا يغيّر HarDoc شيئًا دون موافقتك. مهارة `skill-governor` للقراءة فقط. أما `trim` فتطبّق التغيير بعد موافقتك على معاينة فقط، وتأخذ نسخة احتياطية أولًا، ثم تطبع أمرًا واحدًا للتراجع.

للتفاصيل الكاملة وشرح التقييم، راجع [README الإنجليزي](README.md).
