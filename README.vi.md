# HarDoc

![Banner truyện tranh HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc kiểm tra harness của Claude Code và Codex ở chế độ chỉ đọc. Công cụ tìm các chỉ dẫn trùng lặp hoặc xung đột khiến trợ lý chọn sai skill.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Cài đặt cho Claude Code

Chạy hai lệnh sau một lần:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Dùng trong Claude Code

Mở một phiên Claude Code mới rồi chạy:

```text
/skill-governor audit .
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

HarDoc chỉ đọc. Công cụ không xóa, vô hiệu hóa, cài đặt hoặc sửa cấu hình harness và không tự động sửa kết quả doctor. Hãy xem lại đề xuất trước khi thay đổi.

Xem [English README](README.md) để đọc hướng dẫn và quy trình đánh giá đầy đủ.
