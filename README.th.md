# HarDoc

![แบนเนอร์การ์ตูน HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc ตรวจสอบ harness ของ Claude Code และ Codex แบบอ่านอย่างเดียว ช่วยค้นหาคำสั่งที่ซ้ำหรือขัดแย้งกันจนทำให้ผู้ช่วยเลือก skill ผิด

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
```

## ใช้งานใน Claude Code

เปิดเซสชัน Claude Code ใหม่ แล้วเรียกใช้:

```text
/skill-governor audit .
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

HarDoc ทำงานแบบอ่านอย่างเดียว ไม่ลบ ปิดใช้งาน ติดตั้ง หรือแก้ไขการตั้งค่า harness และไม่แก้ผลลัพธ์ doctor อัตโนมัติ โปรดตรวจสอบข้อเสนอก่อนเปลี่ยนแปลง

ดู [English README](README.md) สำหรับคู่มือและการประเมินฉบับเต็ม
