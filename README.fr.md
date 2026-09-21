# HarDoc

![Bannière illustrée HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc examine votre harness Claude Code et Codex. Il rapporte d'abord et ne modifie un réglage qu'après votre accord.

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
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Utiliser dans Claude Code

Ouvrez une nouvelle session Claude Code puis exécutez :

```text
/skill-governor audit .
```

Pour agir sur le rapport, affichez un aperçu du nettoyage :

```text
/trim --dry-run
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

HarDoc ne change rien sans votre accord. La compétence `skill-governor` est en lecture seule. `trim` n'applique un changement qu'après votre validation d'un aperçu, prend d'abord un instantané et affiche une seule commande pour revenir en arrière.

Consultez le [README en anglais](README.md) pour le guide complet et l’évaluation.
