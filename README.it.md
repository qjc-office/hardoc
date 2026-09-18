# HarDoc

![Banner a fumetti di HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc controlla in sola lettura l’harness di Claude Code e Codex. Trova istruzioni duplicate o in conflitto che possono far scegliere all’assistente lo skill sbagliato.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Installare per Claude Code

Esegui questi due comandi una sola volta:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Usare in Claude Code

Apri una nuova sessione Claude Code ed esegui:

```text
/skill-governor audit .
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

HarDoc è in sola lettura. Non elimina, disattiva, installa o modifica la configurazione dell’harness e non corregge automaticamente i risultati doctor. Esamina le proposte prima di applicare modifiche.

Per la guida completa e la valutazione, consulta il [README in inglese](README.md).
