# HarDoc

![HarDoc কমিক ব্যানার](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc হলো Claude Code ও Codex হ্যারনেসের একটি read-only পরীক্ষা। এটি এমন পুনরাবৃত্ত বা পরস্পরবিরোধী নির্দেশনা খুঁজে বের করে যা সহকারীকে ভুল skill বেছে নিতে বাধ্য করে।

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Claude Code-এ ইনস্টল করুন

একবার নিচের দুটি কমান্ড চালান:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Codex-এ লোকাল ইনস্টল

Codex-এ skill সরাসরি ইনস্টল করতে রিপোজিটরি ক্লোন করে আপনার লোকাল skills ফোল্ডারে একটি লিংক তৈরি করুন:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## Claude Code-এ ব্যবহার

একটি নতুন Claude Code সেশন খুলে চালান:

```text
/skill-governor audit .
```

## Codex-এ ব্যবহার

Codex-এ skill দেখা গেলে নতুন সেশন খুলে চালান:

```text
$skill-governor audit .
```

## HarDoc কী পরীক্ষা করে

HarDoc আগে project directory যাচাই করে, তারপর CLI version দেখে এবং প্রতিটি runtime-এর native doctor চালানোর চেষ্টা করে।

- `claude doctor`: Claude Code ইনস্টলেশনের স্বাস্থ্য পরীক্ষা করে।
- `codex doctor`: Codex ইনস্টলেশনের স্বাস্থ্য পরীক্ষা করে।
- `audit`: skills, MCP, plugins, rules, hooks, agents এবং বাস্তব ব্যবহারের প্রমাণ দেখে।

## নিরাপত্তা সীমা

HarDoc read-only। এটি কিছু মুছে, নিষ্ক্রিয়, ইনস্টল বা harness configuration পরিবর্তন করে না এবং doctor ফলাফল নিজে ঠিক করে না। পরিবর্তনের আগে প্রস্তাব পর্যালোচনা করুন।

সম্পূর্ণ বিবরণ ও evaluation-এর জন্য [English README](README.md) দেখুন।
