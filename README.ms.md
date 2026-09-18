# HarDoc

![Sepanduk komik HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc ialah pemeriksaan baca sahaja untuk harness Claude Code dan Codex. Ia mencari arahan pendua atau bercanggah yang menyebabkan pembantu memilih skill yang salah.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Pasang untuk Claude Code

Jalankan dua arahan ini sekali sahaja:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Pasang secara setempat dalam Codex

Untuk memasang skill terus ke Codex, klon repositori dan buat pautan dalam folder skills setempat anda:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## Guna dalam Claude Code

Buka sesi Claude Code baharu dan jalankan:

```text
/skill-governor audit .
```

## Guna dengan Codex

Jika skill kelihatan dalam Codex, buka sesi baharu dan jalankan:

```text
$skill-governor audit .
```

## Perkara yang diperiksa HarDoc

HarDoc menyemak direktori projek, versi CLI, kemudian cuba menjalankan native doctor bagi setiap runtime.

- `claude doctor`: Menyemak kesihatan pemasangan Claude Code.
- `codex doctor`: Menyemak kesihatan pemasangan Codex.
- `audit`: Menyemak skills, MCP, plugins, rules, hooks, agents dan bukti penggunaan sebenar.

## Had keselamatan

HarDoc beroperasi secara baca sahaja. Ia tidak memadam, melumpuhkan, memasang atau mengubah konfigurasi harness dan tidak membaiki keputusan doctor secara automatik. Semak cadangan dahulu.

Lihat [English README](README.md) untuk panduan dan penilaian lengkap.
