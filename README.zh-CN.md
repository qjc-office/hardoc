# HarDoc

![HarDoc 漫画横幅](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc 检查你的 Claude Code 与 Codex 框架配置。它先给出报告，只有在你同意之后才会更改设置。

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## 在 Claude Code 中安装

只需运行一次下面两条命令：

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## 在 Codex 中本地安装

要直接在 Codex 中安装该 skill，请克隆仓库，并在本地 skills 文件夹中创建链接：

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## 在 Claude Code 中使用

打开新的 Claude Code 会话，然后运行：

```text
/skill-governor audit .
```

要按报告动手整理，先查看预览：

```text
/trim --dry-run
```

## 在 Codex 中使用

如果 Codex 已显示该 skill，请打开新会话并运行：

```text
$skill-governor audit .
```

## HarDoc 检查什么

HarDoc 先验证项目目录，再检查 CLI 版本，并尝试运行对应运行时的原生 doctor。

- `claude doctor`: 检查 Claude Code 安装健康状况。
- `codex doctor`: 检查 Codex 安装健康状况。
- `audit`: 检查 skills、MCP、plugins、rules、hooks、agents 以及实际调用证据。

## 安全边界

未经你同意，HarDoc 不会更改任何内容。`skill-governor` 技能只读。`trim` 技能只在你确认预览之后才应用更改，事先做好快照，并给出一条撤销命令。

完整说明和评估流程请查看 [English README](README.md)。
