# HarDoc

![Banner de cómic de HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc revisa tu harness de Claude Code y Codex. Primero informa y solo cambia ajustes después de que los apruebes.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Instalar para Claude Code

Ejecuta estos dos comandos una sola vez:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Instalar localmente en Codex

Para instalar la skill directamente en Codex, clona el repositorio y crea un enlace en tu carpeta local de skills:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Usar en Claude Code

Abre una sesión nueva de Claude Code y ejecuta:

```text
/skill-governor audit .
```

Para actuar sobre el informe, mira una vista previa de la limpieza:

```text
/trim --dry-run
```

## Usar con Codex

Si el skill aparece en Codex, abre una sesión nueva y ejecuta:

```text
$skill-governor audit .
```

## Qué comprueba HarDoc

HarDoc comprueba primero el directorio del proyecto, después la versión de la CLI e intenta ejecutar el doctor nativo de cada runtime.

- `claude doctor`: Comprueba el estado de la instalación de Claude Code.
- `codex doctor`: Comprueba el estado de la instalación de Codex.
- `audit`: Comprueba skills, MCP, plugins, rules, hooks, agents y pruebas de uso real.

## Límites de seguridad

HarDoc no cambia nada sin tu aprobación. La habilidad `skill-governor` es de solo lectura. `trim` aplica un cambio solo después de que apruebes una vista previa, toma antes una instantánea e imprime un único comando para deshacerlo.

Consulta el [README en inglés](README.md) para la guía completa y la evaluación.
