# HarDoc

![HarDoc çizgi roman bannerı](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc, Claude Code ve Codex koşumunuzu denetler. Önce rapor verir ve ayarları ancak siz onayladıktan sonra değiştirir.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Claude Code için kurulum

Bu iki komutu bir kez çalıştırın:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Codex’e yerel kurulum

Skill’i Codex’e doğrudan kurmak için depoyu klonlayın ve yerel skills klasörünüzde bir bağlantı oluşturun:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Claude Code ile kullanma

Yeni bir Claude Code oturumu açıp çalıştırın:

```text
/skill-governor audit .
```

Rapora göre harekete geçmek için temizliğin önizlemesine bakın:

```text
/trim --dry-run
```

## Codex ile kullanma

Skill Codex’te görünüyorsa yeni bir oturum açıp çalıştırın:

```text
$skill-governor audit .
```

## HarDoc neyi denetler

HarDoc önce proje dizinini, sonra CLI sürümünü kontrol eder ve her runtime’ın native doctor komutunu denemeye çalışır.

- `claude doctor`: Claude Code kurulumunun durumunu denetler.
- `codex doctor`: Codex kurulumunun durumunu denetler.
- `audit`: Skills, MCP, plugins, rules, hooks, agents ve gerçek kullanım kanıtlarını denetler.

## Güvenlik sınırları

HarDoc sizin onayınız olmadan hiçbir şeyi değiştirmez. `skill-governor` becerisi yalnızca okur. `trim` becerisi, bir önizlemeyi onayladıktan sonra değişikliği uygular; önce anlık görüntü alır ve geri almak için tek bir komut yazdırır.

Tam kılavuz ve değerlendirme için [English README](README.md) sayfasına bakın.
