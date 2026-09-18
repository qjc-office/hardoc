# HarDoc

![Banner komik HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc adalah pemeriksaan read-only untuk harness Claude Code dan Codex. HarDoc menemukan instruksi duplikat atau bertentangan yang dapat membuat asisten memilih skill yang salah.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Instal untuk Claude Code

Jalankan dua perintah ini satu kali:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Instal lokal di Codex

Untuk memasang skill langsung di Codex, clone repositori lalu buat tautan di folder skills lokal Anda:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## Gunakan di Claude Code

Buka sesi Claude Code baru lalu jalankan:

```text
/skill-governor audit .
```

## Gunakan dengan Codex

Jika skill sudah terlihat di Codex, buka sesi baru lalu jalankan:

```text
$skill-governor audit .
```

## Yang diperiksa HarDoc

HarDoc memeriksa direktori proyek, versi CLI, lalu mencoba native doctor untuk setiap runtime.

- `claude doctor`: Memeriksa kesehatan instalasi Claude Code.
- `codex doctor`: Memeriksa kesehatan instalasi Codex.
- `audit`: Memeriksa skills, MCP, plugins, rules, hooks, agents, dan bukti penggunaan nyata.

## Batas keamanan

HarDoc bersifat read-only. HarDoc tidak menghapus, menonaktifkan, menginstal, atau mengubah konfigurasi harness dan tidak memperbaiki hasil doctor secara otomatis. Tinjau usulan sebelum mengubah apa pun.

Lihat [English README](README.md) untuk panduan lengkap dan evaluasi.
