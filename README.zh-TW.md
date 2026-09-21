# HarDoc

![HarDoc 漫畫橫幅](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc 會檢查你的 Claude Code 與 Codex 框架設定。它先提出報告，只有在你同意之後才會變更設定。

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## 在 Claude Code 中安裝

只需執行以下兩個指令一次：

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## 在 Codex 中本機安裝

若要直接在 Codex 中安裝這個 skill，請複製儲存庫，並在本機 skills 資料夾建立連結：

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## 在 Claude Code 中使用

開啟新的 Claude Code 工作階段，然後執行：

```text
/skill-governor audit .
```

若要依報告動手整理，先查看預覽：

```text
/trim --dry-run
```

## 在 Codex 中使用

如果 Codex 已顯示此 skill，請開啟新工作階段並執行：

```text
$skill-governor audit .
```

## HarDoc 會檢查什麼

HarDoc 先驗證專案目錄，再檢查 CLI 版本，並嘗試執行對應執行環境的原生 doctor。

- `claude doctor`: 檢查 Claude Code 安裝健康狀況。
- `codex doctor`: 檢查 Codex 安裝健康狀況。
- `audit`: 檢查 skills、MCP、plugins、rules、hooks、agents 與實際呼叫證據。

## 安全界線

未經你同意，HarDoc 不會變更任何內容。`skill-governor` 技能唯讀。`trim` 技能只在你確認預覽之後才套用變更，事先建立快照，並列出一行還原指令。

完整說明與評估流程請查看 [English README](README.md)。
