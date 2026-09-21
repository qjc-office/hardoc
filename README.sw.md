# HarDoc

![Bango la katuni la HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc hukagua harness yako ya Claude Code na Codex. Huripoti kwanza, na hubadilisha mipangilio baada tu ya wewe kuidhinisha.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Sakinisha kwa Claude Code

Tekeleza amri hizi mbili mara moja:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Sakinisha ndani ya Codex

Ili kusakinisha skill moja kwa moja katika Codex, kloni hazina na uunde kiungo kwenye folda yako ya skills ya ndani:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Tumia katika Claude Code

Fungua kikao kipya cha Claude Code kisha utekeleze:

```text
/skill-governor audit .
```

Ili kutekeleza yaliyo kwenye ripoti, tazama muhtasari wa usafishaji kwanza:

```text
/trim --dry-run
```

## Tumia na Codex

Ikiwa skill inaonekana katika Codex, fungua kikao kipya kisha utekeleze:

```text
$skill-governor audit .
```

## HarDoc hukagua nini

HarDoc hukagua saraka ya mradi kwanza, kisha toleo la CLI, na hujaribu native doctor ya kila runtime.

- `claude doctor`: Hukagua afya ya usakinishaji wa Claude Code.
- `codex doctor`: Hukagua afya ya usakinishaji wa Codex.
- `audit`: Hukagua skills, MCP, plugins, rules, hooks, agents na ushahidi wa matumizi halisi.

## Mipaka ya usalama

HarDoc haibadilishi chochote bila idhini yako. Ujuzi wa `skill-governor` ni wa kusoma tu. `trim` hutekeleza mabadiliko baada tu ya wewe kuidhinisha muhtasari, huchukua nakala kwanza, na huonyesha amri moja ya kurudisha kila kitu.

Tazama [English README](README.md) kwa mwongozo na tathmini kamili.
