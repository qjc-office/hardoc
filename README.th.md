# HarDoc

![แบนเนอร์การ์ตูน HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc ตรวจฮาร์เนสของ Claude Code และ Codex ของคุณ โดยรายงานก่อน และจะเปลี่ยนการตั้งค่าเมื่อคุณอนุมัติแล้วเท่านั้น

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## ติดตั้งสำหรับ Claude Code

เรียกใช้คำสั่งสองบรรทัดนี้เพียงครั้งเดียว:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## ติดตั้งใน Codex แบบโลคัล

หากต้องการติดตั้ง skill ลงใน Codex โดยตรง ให้โคลน repository แล้วสร้างลิงก์ในโฟลเดอร์ skills ภายในเครื่องของคุณ:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## ใช้งานใน Claude Code

เปิดเซสชัน Claude Code ใหม่ แล้วเรียกใช้:

```text
/skill-governor audit .
```

หากต้องการลงมือตามรายงาน ให้ดูตัวอย่างการจัดระเบียบก่อน:

```text
/trim --dry-run
```

## ใช้งานกับ Codex

หากมี skill แสดงใน Codex ให้เปิดเซสชันใหม่แล้วเรียกใช้:

```text
$skill-governor audit .
```

## HarDoc ตรวจสอบอะไร

HarDoc ตรวจสอบโฟลเดอร์โครงการก่อน จากนั้นตรวจสอบเวอร์ชัน CLI และลองใช้ native doctor ของแต่ละ runtime

- `claude doctor`: ตรวจสอบสุขภาพการติดตั้ง Claude Code
- `codex doctor`: ตรวจสอบสุขภาพการติดตั้ง Codex
- `audit`: ตรวจสอบ skills, MCP, plugins, rules, hooks, agents และหลักฐานการใช้งานจริง

## ขอบเขตความปลอดภัย

HarDoc จะไม่เปลี่ยนอะไรโดยไม่ได้รับอนุมัติจากคุณ สกิล `skill-governor` อ่านอย่างเดียว ส่วน `trim` จะเปลี่ยนก็ต่อเมื่อคุณอนุมัติตัวอย่างที่แสดงไว้ โดยสำรองไฟล์ก่อน แล้วแสดงคำสั่งเดียวสำหรับย้อนกลับ

ดู [English README](README.md) สำหรับคู่มือและการประเมินฉบับเต็ม
