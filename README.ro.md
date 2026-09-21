# HarDoc

![Banner de benzi desenate HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc verifică harness-ul tău Claude Code și Codex. Raportează mai întâi și schimbă setări doar după ce aprobi.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Instalare pentru Claude Code

Rulează o singură dată aceste două comenzi:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Instalare locală în Codex

Pentru a instala skill-ul direct în Codex, clonează repository-ul și creează o legătură în folderul local de skills:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Folosire în Claude Code

Deschide o sesiune nouă Claude Code și rulează:

```text
/skill-governor audit .
```

Pentru a acționa pe baza raportului, vezi o previzualizare a curățării:

```text
/trim --dry-run
```

## Folosire cu Codex

Dacă skill-ul este vizibil în Codex, deschide o sesiune nouă și rulează:

```text
$skill-governor audit .
```

## Ce verifică HarDoc

HarDoc verifică mai întâi directorul proiectului, apoi versiunea CLI și încearcă doctor-ul nativ al fiecărui runtime.

- `claude doctor`: Verifică starea instalării Claude Code.
- `codex doctor`: Verifică starea instalării Codex.
- `audit`: Verifică skills, MCP, plugins, rules, hooks, agents și dovezile folosirii reale.

## Limite de siguranță

HarDoc nu schimbă nimic fără aprobarea ta. Abilitatea `skill-governor` este doar pentru citire. `trim` aplică o schimbare doar după ce aprobi o previzualizare, face întâi un instantaneu și afișează o singură comandă pentru revenire.

Pentru ghidul complet și evaluare, vezi [English README](README.md).
