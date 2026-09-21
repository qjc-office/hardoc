# HarDoc

![Banner a fumetti di HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc controlla il tuo harness di Claude Code e Codex. Prima riporta, e modifica le impostazioni solo dopo la tua approvazione.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Installare per Claude Code

Esegui questi due comandi una sola volta:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Installazione locale in Codex

Per installare direttamente la skill in Codex, clona il repository e crea un collegamento nella cartella skills locale:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Usare in Claude Code

Apri una nuova sessione Claude Code ed esegui:

```text
/skill-governor audit .
```

Per agire sul rapporto, guarda un'anteprima della pulizia:

```text
/trim --dry-run
```

## Usare con Codex

Se lo skill è visibile in Codex, apri una nuova sessione ed esegui:

```text
$skill-governor audit .
```

## Cosa controlla HarDoc

HarDoc verifica prima la cartella del progetto, poi la versione CLI e prova il doctor nativo di ogni runtime.

- `claude doctor`: Controlla lo stato dell’installazione di Claude Code.
- `codex doctor`: Controlla lo stato dell’installazione di Codex.
- `audit`: Controlla skills, MCP, plugins, rules, hooks, agents e le prove dell’uso reale.

## Limiti di sicurezza

HarDoc non cambia nulla senza la tua approvazione. La skill `skill-governor` è di sola lettura. `trim` applica una modifica solo dopo che hai approvato un'anteprima, crea prima uno snapshot e stampa un singolo comando per annullarla.

Per la guida completa e la valutazione, consulta il [README in inglese](README.md).
