# HarDoc

![Bannière illustrée HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc est un contrôle en lecture seule du harness de Claude Code et Codex. Il repère les instructions dupliquées ou contradictoires qui font choisir le mauvais skill à l’assistant.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Installer pour Claude Code

Exécutez ces deux commandes une seule fois :

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Installer localement dans Codex

Pour installer directement la skill dans Codex, clonez le dépôt et créez un lien dans votre dossier local de skills :

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## Utiliser dans Claude Code

Ouvrez une nouvelle session Claude Code puis exécutez :

```text
/skill-governor audit .
```

## Utiliser avec Codex

Si le skill est visible dans Codex, ouvrez une nouvelle session puis exécutez :

```text
$skill-governor audit .
```

## Ce que vérifie HarDoc

HarDoc vérifie d’abord le dossier du projet, puis la version du CLI et tente le doctor natif de chaque runtime.

- `claude doctor`: Vérifie la santé de l’installation Claude Code.
- `codex doctor`: Vérifie la santé de l’installation Codex.
- `audit`: Analyse les skills, MCP, plugins, rules, hooks, agents et les preuves d’utilisation réelle.

## Limites de sécurité

HarDoc est en lecture seule. Il ne supprime, désactive, installe ni ne modifie la configuration du harness et ne corrige pas automatiquement les résultats de doctor. Examinez les propositions avant tout changement.

Consultez le [README en anglais](README.md) pour le guide complet et l’évaluation.
