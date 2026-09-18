# HarDoc

![Banner de cómic de HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc revisa el harness de Claude Code y Codex en modo de solo lectura. Encuentra instrucciones duplicadas o contradictorias que pueden hacer que el asistente elija el skill equivocado.

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
```

## Usar en Claude Code

Abre una sesión nueva de Claude Code y ejecuta:

```text
/skill-governor audit .
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

HarDoc funciona solo en modo lectura. No elimina, desactiva, instala ni modifica la configuración del harness y no corrige automáticamente los resultados de doctor. Revisa las propuestas antes de cambiar nada.

Consulta el [README en inglés](README.md) para la guía completa y la evaluación.
