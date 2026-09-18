# HarDoc

![Bango la katuni la HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc hukagua harness ya Claude Code na Codex kwa kusoma pekee. Hupata maagizo yaliyorudiwa au yanayokinzana yanayoweza kumfanya msaidizi achague skill isiyo sahihi.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Sakinisha kwa Claude Code

Tekeleza amri hizi mbili mara moja:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Tumia katika Claude Code

Fungua kikao kipya cha Claude Code kisha utekeleze:

```text
/skill-governor audit .
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

HarDoc ni ya kusoma pekee. Haifuti, hailemazi, haisakinishi wala kubadilisha usanidi wa harness, na haisahihishi matokeo ya doctor kiotomatiki. Kagua mapendekezo kabla ya mabadiliko.

Tazama [English README](README.md) kwa mwongozo na tathmini kamili.
