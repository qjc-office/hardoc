# HarDoc

![Banner truyện tranh HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc kiểm tra harness Claude Code và Codex của bạn. Nó báo cáo trước, và chỉ thay đổi thiết lập sau khi bạn chấp thuận.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Cài đặt cho Claude Code

Chạy hai lệnh sau một lần:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Cài đặt cục bộ trong Codex

Để cài skill trực tiếp vào Codex, hãy clone repository và tạo liên kết trong thư mục skills cục bộ của bạn:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Dùng trong Claude Code

Mở một phiên Claude Code mới rồi chạy:

```text
/skill-governor audit .
```

Để hành động theo báo cáo, hãy xem bản xem trước của việc dọn dẹp:

```text
/trim --dry-run
```

## Dùng với Codex

Nếu skill đã hiển thị trong Codex, hãy mở phiên mới rồi chạy:

```text
$skill-governor audit .
```

## HarDoc kiểm tra gì

HarDoc kiểm tra thư mục dự án trước, sau đó kiểm tra phiên bản CLI và thử chạy native doctor của từng runtime.

- `claude doctor`: Kiểm tra tình trạng cài đặt Claude Code.
- `codex doctor`: Kiểm tra tình trạng cài đặt Codex.
- `audit`: Kiểm tra skills, MCP, plugins, rules, hooks, agents và bằng chứng sử dụng thực tế.

## Giới hạn an toàn

HarDoc không thay đổi gì nếu bạn chưa chấp thuận. Kỹ năng `skill-governor` chỉ đọc. Kỹ năng `trim` chỉ áp dụng thay đổi sau khi bạn duyệt bản xem trước, chụp lại ảnh sao lưu trước, rồi in ra một lệnh duy nhất để hoàn tác.

Xem [English README](README.md) để đọc hướng dẫn và quy trình đánh giá đầy đủ.
