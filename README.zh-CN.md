# HarDoc

![HarDoc 漫画横幅](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc 是面向 Claude Code 和 Codex 的只读 harness 检查工具。它会找出重复或冲突的指令，帮助避免助手选择错误的 skill。

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
```

## 在 Claude Code 中使用

打开新的 Claude Code 会话，然后运行：

```text
/skill-governor audit .
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

HarDoc 只读运行。它不会删除、禁用、安装或修改 harness 配置，也不会自动修复 doctor 结果。请先人工审阅建议。

完整说明和评估流程请查看 [English README](README.md)。
