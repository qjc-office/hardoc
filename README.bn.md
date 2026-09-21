# HarDoc

![HarDoc কমিক ব্যানার](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc আপনার Claude Code ও Codex হারনেস পরীক্ষা করে। এটি আগে রিপোর্ট দেয়, আর আপনার অনুমোদনের পরেই কোনো সেটিং বদলায়।

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
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Claude Code-এ ব্যবহার

একটি নতুন Claude Code সেশন খুলে চালান:

```text
/skill-governor audit .
```

রিপোর্ট অনুযায়ী কাজ করতে, পরিষ্কার করার প্রিভিউ দেখুন:

```text
/trim --dry-run
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

আপনার অনুমোদন ছাড়া HarDoc কিছুই বদলায় না। `skill-governor` স্কিলটি কেবল পড়ে। `trim` স্কিলটি প্রিভিউ দেখিয়ে আপনার অনুমোদন পেলে তবেই বদলায়, আগে স্ন্যাপশট নেয়, আর ফেরত যাওয়ার একটি কমান্ড দেখায়।

সম্পূর্ণ বিবরণ ও evaluation-এর জন্য [English README](README.md) দেখুন।
