# HarDoc

![Banner de quadrinhos do HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

O HarDoc verifica o seu harness do Claude Code e do Codex. Ele relata primeiro e só altera configurações depois da sua aprovação.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Instalar para Claude Code

Execute estes dois comandos uma vez:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Instalar localmente no Codex

Para instalar a skill diretamente no Codex, clone o repositório e crie um link na sua pasta local de skills:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Usar no Claude Code

Abra uma nova sessão do Claude Code e execute:

```text
/skill-governor audit .
```

Para agir sobre o relatório, veja uma prévia da limpeza:

```text
/trim --dry-run
```

## Usar com Codex

Se o skill aparecer no Codex, abra uma nova sessão e execute:

```text
$skill-governor audit .
```

## O que o HarDoc verifica

O HarDoc verifica primeiro o diretório do projeto, depois a versão da CLI e tenta executar o doctor nativo de cada runtime.

- `claude doctor`: Verifica a saúde da instalação do Claude Code.
- `codex doctor`: Verifica a saúde da instalação do Codex.
- `audit`: Verifica skills, MCP, plugins, rules, hooks, agents e evidências de uso real.

## Limites de segurança

O HarDoc não muda nada sem a sua aprovação. A skill `skill-governor` é somente leitura. A `trim` aplica uma mudança apenas depois que você aprova uma prévia, faz antes um snapshot e imprime um único comando para desfazer.

Veja o [README em inglês](README.md) para o guia completo e a avaliação.
